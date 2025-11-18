Projet: Un mini jeux ou l'on devrais résoudre une série d'énigme ou quizz sur un sujet personnalisé pour faire avancer nos personnages. 

https://www.citizencode.net/blog-actualites/mini-projet-creer-un-quizz-interactif-avec-python

# Importe le module 'random' pour mélanger les questions (optionnel, mais sympa)
import random

# Définition des questions (dictionnaire)
# Structure: "Question": ["Option A", "Option B", "Option C", "Bonne Réponse"]
questions = {
    "Quelle est la capitale de la France ?": ["Paris", "Londres", "Rome", "Paris"],
    "Quel est le plus grand océan du monde ?": ["Atlantique", "Pacifique", "Indien", "Pacifique"],
    "Combien de côtés a un triangle ?": ["Deux", "Trois", "Quatre", "Trois"],
    "Qui a peint La Joconde ?": ["Van Gogh", "Picasso", "Léonard de Vinci", "Léonard de Vinci"],
    "Quel est l'élément chimique de l'eau ?": ["O2", "CO2", "H2O", "H2O"],
    "Quel animal est connu pour sa poche ?": ["Chien", "Kangourou", "Chat", "Kangourou"],
    "Combien de jours y a-t-il dans une année bissextile ?": ["365", "366", "367", "366"],
    "Quel est le plus grand continent ?": ["Europe", "Afrique", "Asie", "Asie"],
    "Dans quel pays se trouve le Mont Everest ?": ["Chine", "Népal", "Inde", "Népal"],
    "Quel est le nombre atomique de l'oxygène ?": ["6", "8", "10", "8"]
}

def lancer_quiz():
    """Lance le quiz, pose les questions et calcule le score."""
    score = 0
    
    # Convertir les questions en liste pour pouvoir les mélanger
    liste_questions = list(questions.items())
    # Mélange aléatoire des questions
    random.shuffle(liste_questions) 
    
    print("✨ **Bienvenue dans le Quiz !** ✨\n")
    print(f"Vous avez {len(questions)} questions.\n")

    for i, (question_texte, details) in enumerate(liste_questions):
        # Détacher les options de la bonne réponse
        options = details[:-1]
        bonne_reponse = details[-1]
        
        print("-" * 30)
        print(f"**Question {i + 1} : {question_texte}**")
        
        # Afficher les options
        options_dict = {
            "A": options[0],
            "B": options[1],
            "C": options[2]
        }
        
        for cle, valeur in options_dict.items():
            print(f"   {cle}. {valeur}")
            
        # Demander la réponse de l'utilisateur
        while True:
            reponse_utilisateur = input("Votre réponse (A, B ou C) : ").strip().upper()
            if reponse_utilisateur in options_dict:
                break
            print("❌ Choix invalide. Veuillez entrer A, B ou C.")

        # Vérifier la réponse
        choix_utilisateur = options_dict[reponse_utilisateur]
        if choix_utilisateur == bonne_reponse:
            print("✅ **Bonne réponse !**")
            score += 1
        else:
            print(f"❌ **Mauvaise réponse.** La bonne réponse était : {bonne_reponse}")
    
    # Afficher le résultat final
    print("\n" + "=" * 30)
    print("🎉 **QUIZ TERMINÉ !** 🎉")
    print(f"Votre score final est de **{score}** sur **{len(questions)}**.")
    
    if score >= len(questions) * 0.8:
        print("Félicitations ! Excellent travail !")
    elif score >= len(questions) * 0.5:
        print("Pas mal du tout ! Continuez à vous entraîner.")
    else:
        print("Vous ferez mieux la prochaine fois. Ne baissez pas les bras !")
    print("=" * 30)

# Appel de la fonction pour lancer le jeu
if __name__ == "__main__":
    lancer_quiz()
