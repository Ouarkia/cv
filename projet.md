# Présentation de la Version 0 : 

## ->Le Projet Quizz Interactif
Le Concept du ProjetLe projet a pour objectif de créer un mini-jeu de type quizz interactif basé sur les technologies web fondamentales : HTML, CSS et JavaScript.

L'idée est de proposer une expérience ludique et accessible, où l'utilisateur doit résoudre une série de questions sur un sujet donné.
Pour cette version initiale, le thème choisi est la Culture Générale, afin de garantir un divertissement et une accessibilité optimaux pour le plus grand nombre.



## Démarche de Création: 
La réalisation de cette première version fonctionnelle a suivi une approche d'apprentissage et de prototypage rapide :
Recherche et Inspiration: 

Consultation de ressources en ligne pour comprendre les meilleures pratiques de création de quizz interactif (par exemple : https://www.citizencode.net/blog-actualites/mini-projet-creer-un-quizz-interactif-avec-python).

Prototypage par IA (Test Gemini): Utilisation d'un modèle d'IA générative pour accélérer le développement initial.

Prompt utilisé: "Un mini jeux ou l'on devrais résoudre une série d'énigme ou quizz sur un sujet personnalisé."

Résultat: L'IA a généré la première structure de code HTML/CSS/JavaScript, qui sert de base fonctionnelle solide pour le développement et l'amélioration future du projet.


## Architecture et Logique du Code (Version 0)

La version 0 se compose d'un seul fichier index.html intégrant les trois langages :ComposantRôleDescriptionHTML (<body>)StructureDéfinit le conteneur du quizz (quiz-container), l'affichage de la question (question-text), les boutons de réponse (answer-buttons) et le bouton de navigation (next-button).CSS (<style>)Style/DesignAssure une mise en page centrée, des couleurs claires et un retour visuel clair lors de la sélection d'une réponse (couleurs verte/rouge).JavaScript (<script>)Logique/InteractionGère le déroulement du jeu, le suivi du score, l'affichage des questions, la vérification des réponses et l'affichage du résultat final.




## Diagramme de flux testprojet: 
graph TD
    A[Démarrage: Chargement de la page] --> B(Appel: startQuiz);
    
    B --> C{Initialisation des variables};
    C --> D(Appel: showQuestion);
    
    D --> E(Réinitialisation: resetState);
    E --> F(Afficher Question et Réponses);
    
    F --> G{Clic sur un bouton de Réponse};
    G --answered=true--> G;
    G --answered=false--> H(Appel: selectAnswer);

    H --> I{La réponse est-elle Correcte ?};
    I --Oui--> J(Incrémenter Score);
    J --> K(Marquer Réponse et Afficher Correct/Incorrect);
    I --Non--> K;

    K --> L(Désactiver Clics & Afficher bouton Suivant);
    
    L --> M{Clic sur le bouton Suivant};
    
    M --> N{Reste-t-il des Questions?};
    N --Oui--> O(Incrémenter Index);
    O --> D; /* Retour à showQuestion */
    N --Non--> P(Appel: showResult);
    
    P --> Q(Afficher le Score Final);
    P --> R(Afficher bouton Rejouer);

    R --> B; /* Retour à startQuiz pour relancer */
