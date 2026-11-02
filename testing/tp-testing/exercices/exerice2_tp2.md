Exercice 2 : Nettoyer un texte avant son analyse
Ajouter au fichier pytest.ini sur tp_tests.py pour ignorer les tests de l’exercice 1 avec:
[pytest]
addopts = --ignore=tests/test_demarrage.py --ignore=tests/test_livraison.py


Un prétraitement NLP supprime les espaces aux extrémités, passe le texte en minuscules et remplace les espaces multiples par un seul espace. Toute entrée non textuelle doit déclencher TypeError.
Créer app/texte.py :
def nettoyer_texte(texte):
    if not isinstance(texte, str):
        raise TypeError("Texte attendu")
    return " ".join(texte.lower().split())
Exemples attendus :
“  BONJOUR   monde  “ → “bonjour monde“
“ déjà propre “ → “déjà propre“
Une chaîne vide ou composée uniquement d’espaces → une chaîne vide.
Créer tests/test_texte.py. Écrire un test pour le premier exemple.
Transformer ce test en test paramétré avec @pytest.mark.parametrize("entree, attendu", [...]). Ajouter les deux autres exemples et un texte avec un seul mot en majuscules.
Avec pytest.raises(TypeError), vérifier les entrées 123 et None. Ne pas remplacer ce contrôle par un simple try/except qui laisserait passer le test sans exception.
Exécuter uniquement ce fichier, puis toute la suite. Observer le nombre de cas de test exécutés.
Aide : importer pytest et nettoyer_texte. Dans le test paramétré, utiliser entree et attendu comme paramètres de la fonction de test.
Rappel de syntaxe, à adapter :
@pytest.mark.parametrize("entree, attendu", [
    # Ajouter ici les couples (entrée, résultat attendu)
])
def test_nettoyer_texte(entree, attendu):
    assert nettoyer_texte(entree) == attendu
vérifier que nettoyer un texte déjà nettoyé ne change plus le résultat. Proposer un nom explicite pour ce test.
