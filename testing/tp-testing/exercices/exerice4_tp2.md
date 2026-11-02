Exercice 4 : Isolation des dépendances
Tester une décision sans exécuter le modèle
Une fonction de modération reçoit un modèle. Le modèle retourne la classe « spam » ou « normal » ; la fonction transforme cette classe en décision. On teste cette transformation, pas la précision d’un modèle.
Créer app/moderation.py :
def decider(modele, message):
    classe = modele.predict(message)
    if classe == "spam":
        return "bloquer"
    return "autoriser"
Créer tests/test_moderation.py. Pour préparer un faux modèle :
from unittest.mock import Mock
from app.moderation import decider

# À placer dans le test :
modele = Mock()
modele.predict.return_value = "spam"
Écrire un test qui appelle decider(modele, "Offre miracle") et vérifie la décision « bloquer ».
Dans ce même test, vérifier modele.predict.assert_called_once_with("Offre miracle").
Écrire un second test indépendant où le modèle retourne « normal » : la décision doit être « autoriser ». Créer un nouveau Mock dans ce test.
Expliquer ce que ces tests permettent de vérifier et ce qu’ils ne permettent pas de conclure sur un vrai modèle.
Point de contrôle : aucun chargement de modèle ni accès réseau. Le faux modèle est transmis directement en argument à la fonction.
Bonus : configurer modele.predict.side_effect = RuntimeError("Modele indisponible") et vérifier avec pytest.raises que decider propage cette erreur.
