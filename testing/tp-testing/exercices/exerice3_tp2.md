Exercice 3 : Fixtures et tests d’intégration
Le service Reservation utilise un Stock en mémoire. Une réservation réussie diminue la quantité ; une réservation refusée ne change rien. Une quantité demandée nulle ou négative déclenche ValueError.
Créer app/reservation.py :
class Stock:
    def __init__(self, quantite):
        self.quantite = quantite

    def retirer(self, quantite):
        if quantite <= 0:
            raise ValueError("Quantité positive requise")
        if quantite > self.quantite:
            return False
        self.quantite -= quantite
        return True

class Reservation:
    def __init__(self, stock):
        self.stock = stock

    def reserver(self, quantite):
        if self.stock.retirer(quantite):
            return "confirmee"
        return "refusee"
Créer tests/test_reservation.py. Importer pytest, Stock et Reservation. Définir une fixture stock qui retourne un nouveau Stock(5).
Tester une réservation de 2 unités via Reservation(stock) : vérifier le statut « confirmee » et le stock restant égal à 3.
Dans un autre test, demander 6 unités : vérifier « refusee » et un stock toujours égal à 5.
Tester une réservation de 5 unités : statut confirmé et stock à 0. Chaque test doit utiliser la fixture.
Relancer les tests dans un ordre différent. Expliquer pourquoi leurs résultats restent identiques.
Point de contrôle : utiliser les vrais objets Stock et Reservation, sans mock. Une fixture @pytest.fixture est recréée par défaut pour chaque test ; ne pas stocker un objet mutable partagé au niveau du module.
tester une quantité de 0 avec pytest.raises et vérifier que le stock reste intact. Pourquoi ces tests vérifient-ils une intégration ?
