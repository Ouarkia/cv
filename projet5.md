# Présentation de la Version 5: Expérience Utilisateur et Gestion de l'État


## Objectif de la Version 5

La Version 5 vise à améliorer l'expérience utilisateur et la jouabilité en introduisant deux fonctionnalités clés :

La randomisation des questions pour garantir que chaque partie est unique.

La persistance des données (historique des scores) en utilisant le stockage local du navigateur (localStorage).

De plus, cette version met à jour la structure interne du code pour faciliter les développements futurs.

## Nouveautés et Améliorations Clés
Utilisation de IA Gemini: Prompt utilisé-> "génère moi le code pour ajouter l'option historique des scores à mon quizz ainsi que celui pour rendre les questions aléatoire lors du quizz".

1. Jouabilité Améliorée: Mélange des Questions
Variables de Questions Séparées: Deux tableaux de questions sont désormais utilisés :

allQuestions: Stocke la liste complète et non modifiée des questions chargées depuis le CSV.

questions: Reçoit une copie de allQuestions à chaque début de partie.

Fonction shuffleArray(): Introduction d'une fonction d'utilité implémentant l'Algorithme de Fisher-Yates pour mélanger les éléments du tableau questions.

Nouvelles Parties Uniques: Le mélange est effectué au début de startQuiz(), garantissant que les questions ne se suivent jamais dans le même ordre entre les parties.

2. Persistance des Données: Historique des Scores
Stockage Local (localStorage): Le quiz utilise maintenant le localStorage du navigateur pour sauvegarder l'historique des résultats.

Historique Visuel: Un nouveau conteneur (#history-display) a été ajouté à l'interface pour afficher les 5 derniers scores, y compris la date de la tentative.

Fonctions de Gestion:

loadScoreHistory(): Récupère les scores enregistrés.

saveAndDisplayScoreHistory(): Est appelée à la fin de chaque partie (showResult()) pour enregistrer le nouveau score et mettre à jour la liste affichée à l'utilisateur.

3. Optimisation et Amélioration du Code
Réutilisation des Questions: La fonction loadQuestions() n'est appelée qu'une seule fois au chargement initial du quiz pour récupérer les données du CSV. Les parties suivantes lancées via le bouton "Rejouer" appellent directement startQuiz(), qui utilise le tableau allQuestions déjà chargé et mélangé. Ceci rend l'expérience de "Rejouer" beaucoup plus rapide, car il n'y a pas besoin de refaire un appel réseau au Google Sheet.

Organisation: Les nouvelles fonctions d'utilité (shuffleArray, loadScoreHistory, saveAndDisplayScoreHistory) ont été clairement séparées dans une nouvelle section de la logique JavaScript.

Structure du Code et Composants Techniques
HTML: Ajout du conteneur d'historique des scores:

HTML

<div id="history-display">
    <h3>Historique des 5 derniers scores:</h3>
    <ul id="score-history-list">
        <li>Aucun score enregistré.</li>
    </ul>
</div>

CSS: Nouveaux styles pour #history-display pour contenir et rendre lisible la liste des scores.

JavaScript:

Nouvelles variables d'état: allQuestions, questions, HISTORY_KEY.

Ajout des fonctions shuffleArray, loadScoreHistory, et saveAndDisplayScoreHistory.

Mise à jour de startQuiz() pour mélanger les questions au début de la partie.

Mise à jour de showResult() pour enregistrer le score final.

## Prochaines Étapes / Axes d'Amélioration (V6)
La fonctionnalité du quiz est maintenant très complète. 

historique de score + affichage questions aléatoire 



## Diagramme Mermaid:
graph TD
    A[Démarrage du script] --> B(Appel: loadQuestions);
    
    B --> C(Chargement CSV via PapaParse);
    C --Succès--> D(Stocker dans allQuestions);
    D --Succès--> D1(Appel: startQuiz);
    C --Échec--> E(Afficher Erreur / Arrêt);

    D1 --> F1(Copier allQuestions dans questions);
    F1 --> F2(Appel: shuffleArray - Mélanger questions); /* 🔀 NOUVEAU: Mélange */
    F2 --> G{Initialiser Score=0, Index=0};
    G --> G1(Appel: saveAndDisplayScoreHistory); /* 💾 NOUVEAU: Charger Historique */
    G1 --> H(Appel: showQuestion);
    
    H --> I(Appel: resetState - Nettoyer/Arrêter Timer);
    I --> J(Appel: startTimer);
    J --> K(Afficher Question & Boutons);
    
    K --> L{Interaction de l'utilisateur};
    L --Choix de réponse--> M(Appel: selectAnswer - Arrêter Timer);
    L --Temps Écoulé (Timer 0s)--> N(Appel: handleTimeOut - Arrêter Timer);
    
    M --> O{Mise à jour Score/Marqueurs};
    N --> P{Afficher Bonne Réponse / Audio Incorrect};
    
    O --> Q(Afficher bouton 'Suivant');
    P --> Q;
    
    Q --> R{Clic sur 'Suivant'};
    R --> S(Appel: handleNextButton);
    
    S --> T{Question Suivante?};
    T --Oui--> U(Incrémenter Index);
    U --> H; /* Retour à showQuestion */
    T --Non--> V(Appel: showResult);
    
    V --> V1(Appel: saveAndDisplayScoreHistory); /* 🏆 NOUVEAU: Sauvegarder Score */
    V1 --> W(Afficher Résultat Final);
    W --> X(Bouton 'Rejouer 🔁');

    X --> D1; /* Clic 'Rejouer' relance startQuiz avec les questions déjà chargées (allQuestions) */


















