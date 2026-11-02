Exercice 1 : Tests unitaires
Trouver un bug dans une livraison
Une boutique facture 25 DH de livraison pour un panier inférieur à 300 DH. À partir de 300 DH inclus, la livraison est gratuite. Un montant négatif déclenche ValueError. Les entrées de cet exercice sont des nombres.
Créer app/livraison.py. Le code contient volontairement un bug :
def frais_livraison(montant):
    if montant < 0:
        raise ValueError("Montant negatif")
    if montant > 300:
        return 0
    return 25
Créer tests/test_livraison.py et commencer avec ce test :
from app.livraison import frais_livraison

def test_livraison_panier_ordinaire():
    # Arrange
    montant = 120
    # Act
    resultat = frais_livraison(montant)
    # Assert
    assert resultat == 25
Ajouter trois tests pour les montants 299, 300 et 301 DH. Déterminer les résultats attendus à partir de la règle, avant d’exécuter.
Exécuter les tests. Dans le message d’échec, repérer la valeur attendue et la valeur obtenue.
Corriger uniquement la condition fautive, puis relancer les tests.
Ajouter un test pour un panier de 0 DH. Garder le test qui a révélé le bug : il servira de test de non-régression.
Important !!! : tous les tests passent après correction. Aucun test ne doit être supprimé ou modifié pour masquer le bug.
Question : pourquoi tester uniquement 120 et 500 DH aurait-il laissé passer cette erreur ?
