## Questions Préparatoires

  1. Expliquer le code suivant  (addition.py):

```python
def add(x, y):
#Cette fonction prend 2 variables en arguments, les additionent et retourne un message pour afficher le nom du module ou #l'operation a lieu, puis retroune le resultat de l'addition
  z=x+y

  print('add() executed under the scope: ', __name__)

  return z

if __name__ == '__main__': #on verifie qu'on a pas importé un module
#on recupere deux variables
  x=input('Enter the first number to add: ')

  y=input('Enter the second number to add: ')
#on appelle la fonction pour additioner
  result = add(int(x),int(y))
# on realise un affichage
  print(x, '+', y,'=', result)

  print('Code executed under the scope: ', __name__)
```

# Questions
Pour chaque question, indiquez vos sites choisis pour reference (où le prompt de l'outil d'IA utilisé)

  1. A quoi sert requirments.txt ?
    Il sert a transmettre les informations pour installer, configurer, initialiser... Pour pouvoir utiliser correctement l'application ou fichier.

  1. A quoi ressemble un module en python ?
     
      Un module python est composé de code python, il peut contenir des variables, des fonctions... qui peuvent être importé dans d'autre fichier python.
     
  1. A quoi ressemble un package ?
     
      un package est un ensemble de module python dans un repertoire. Il possède un nom et un fichier d'initialisation.
     
  1. Créer un code python utilisant sous forme de module addition.py
     
      ```
        python
          import addition
          a=5
          b=2
          print(addition.add(a,b))
      ```

  1. A quoi sert pip ?
     
      pip est un gestionnaire de package. C'est-à-dire qu'il peut permettre leurs instalattions, leurs mises à jours, leurs désinstallation...

  1. A quoi sert PYTHONPATH ?
      PYTHONPATH est une varirable d'environnement qui contient le chemin d'accès aux modules pour pouvoir les importer.

  1. Où sont stockés les paquets installé par pip ?
     
      Sans le -user les paquets installé par pip sont installés dans le répertoire globale de python bibliothèque
     
  1. A quoi sert pip install –user ?
     
      Il permet de stocker les paquets dans un répertoire personnel.
     
  1. A quoi sert venv ?
     
      Il sert a créer des environnements virtuels isolés. Cela permet de travailler sur différents projets sans que les modules interfères
     
  1. Comment utiliser venv ?
     
     Pour pouvoir utiliser venv il faut:
     Commecner par la créer avec la commande:
     
         python3 venv nom_de_la_venv
     Une fois la venv crée, il faut l'activer :
     
         source chemin_vers_votre_env/bin/activate
     Puis pouvoir la désactiver à la fin:

         deactivate

  1. A quoi sert docker ?
     
      Un docker est un conteneur, il sert à executer une application dans un environnment isolé, avec seulement les ressources nécessaires pour éxecuter l'application
     
  1. Comment utiliser docker ?

Site utilisé:

  https://openclassrooms.com/
  
  https://chat.openai.com/


## Exercice 0

1. A quoi sert git config , Quelles sont les informtions minimales à renseigner. Est ce bien fait sur votre ordinateur ?
   
    git config permet de configurer les paramètres de git. Les informations minimales sont: le nom et le mail
   
1. Quelles sont les commandes de bases git ? a quoi servent elles ?
   
     git clone  / pour pouvoir clone le github ou gitlab localement
     git checkout -b nom_de_la_branche / creer une branche
     git add / pour ajouter des modifications
     git commit / pour enregistrer les modifications
     git push / pour push les modifcation
     
# TP 1 Degironde Alix

## I. Objectif
L'objectif de ce TP est d'apprendre à utiliser git. Pour cela, on va réaliser un calculateur permettant les opérations basiques (addition, soustraction, division et multiplication) entre 2 nombres complexes représentés sous la forme de tuple

## II. Organisation du projet
Selon l'exercice, des fichiers différents seront présents. Mais des fichiers essentiels tels que le README.md sont présents. On va pouvoir retrouver les fichiers contenant les scripts nécessaires, des fichiers de test, puis ils seront réunis dans des packages, un possédant les fonctions et permmetant leur utilisation, et un de test. Et enfin, ils seront zippés.
Le but étant d'apprendre, j'ai pris la décision de laisser les marques d'apprentissages, par exemple après une erreur des fichiers .vscode sont présent dans les premiers exercices.  

#### Package calculator
C'est dans ce package qu'est définie le script SimpleComplexCalculator.py qui est un script contenat une classe permettant l'execution des fonctions, fonctions contenut dans le script function_calculator.py.

Par exemple voici l'utlisation de la méthode addition :  
```
python
class SimpleComplexCalculator:
    """Class representant une calculatrice complexe"""

    def __init__(self, a, b):
        self.val1 = a
        self.val2 = b

    def add(self):
        """Addition de deux nombres complexe sous la forme d'un tuple de taille 2.

        Parameters
        ----------
        self

        Returns
        -------
        tuple
            L'addition des deux tuples grâce à la fonction addition de du module calculator.py.
        """
        return function_calculator.addition(self.val1, self.val2)
```

et la méthode addition: 
``` python
def addition(a, b):
    """Addition de deux nombres complexe sous la forme d'un tuple de taille 2.

    Parameters
    ----------
    nombre1 : tuple
        Le premier nombre est un tuple contenant 2 entiers.
    nombre2 : tuple
        Le premier nombre est un tuple contenant 2 entiers

    Returns
    -------
    tuple
        L'addition des deux tuples.
    """
    if isinstance(a, tuple) and isinstance(b, tuple) and len(a) == 2 and len(b) == 2:
        if all(isinstance(x, int) for x in a) and all(isinstance(x, int) for x in b):
            return (a[0] + b[0], a[1] + b[1])
    return "Error"

```


#### Package_Test
On réalise les test de notre package calculator dans ce package. On va donc pouvoir tester que les calculs se réalisent bien, mais surtout tester que des erreurs telles qu'un mauvais type de variable soient traités et ne fassent pas planter notre package. A l'aide de différent module (unittest..) et des logs, on a réalisé une classe dans dans le script TestComplexCalculator.py, cette classe contient plusieur fonctions permettant la vérification des fonctions, une pour vérifier qu'on ne divise pas par 0 dans la division et d'autre pour les types de variables.
Voici par exemple le test de la fonction pour la vérification de l'addition:
``` python
def test_addition(self):
        """Fonction de test de l'addition de calculator"""
        result = self.c.add()
        self.assertEqual(result, (4, 6))

```

## III. Utilisation des packages
Pour pouvoir utliser les packages ou script dans les exercices voici les étapes à suivre :

#### 1. Importer les dossiers 
Pour pouvoir importer les fichiers des gitlab voici la commande à executer 

    git clone <URL_du_dépôt>

Vous pouvez ensuite appeler les scripts d'un package à l'extérieur de celui-ci à l'aide de la commande suivant à executer à la racine du dossier :

    export PYTHONPATH=$PYTHONPATH:'.'

#### 2. Installation des modules
Pour installer des modules, il faut commencer par utiliser une venv, son utilisation est d'écrit dans la question préliminaire 10. Ensuite pour un installer, on utilise la commande:

      pip install <nom_du_module>

Par exemple, on utlisera lors d'un exercice on utilisera pylint, on l'installe avec :

    pip install pylint 

#### 3. Utiliser les scritpts 
Pour pouvoir utliser les scripts il faut utiliser la commande :

    python3 <chemin_du_script_>/<nom_du_script>
Par exemple pour executer le test il faut utiliser : 

    python3 test/TestComplexCalculator.py


## IV. Autres Dépôts du projet
Chaque aspect du projet a été traité indépendemment sous la forme de projets Gitlab indépendants. Pour plus d'information sur un aspect précis vous pouvez lire le README de l'exerice correspondant, les liens :  

- Exercice 1 (création des méthodes pour les quatre opérations) : https://gitlab.com/admco_degironde/admco_exo1_degironde
- Exercice 2 (création d'une classe contenant ces méthodes) : https://gitlab.com/admco_degironde/admco_exo2_degironde
- Exercice 3 (règles de codage PEP8) : https://gitlab.com/admco_degironde/admco_exo3_degironde
- Exercice 4 (Création Packages Calculator et Test) : https://gitlab.com/admco_degironde/admco_exo4_degironde
- Exercice 5 (Amélioration classe Test) : https://gitlab.com/admco_degironde/admco_exo5_degironde
- Exercice 6 (Ajout des test avec unittest) : https://gitlab.com/admco_degironde/admco_exo6_degironde
- Exercice 7 (Ajout des logs aux tests) : https://gitlab.com/admco_degironde/admco_exo7_degironde
- Exercice 8 (Création d'un version zippé) : https://gitlab.com/admco_degironde/admco_exo8_degironde


## V. Ressources
énoncé TP : https://github.com/fabricejumel/SUJET_4ETI_AdmCO_20232024/

PEP8 :  
https://python.sdv.univ-paris-diderot.fr/15_bonnes_pratiques/

Black : https://pypi.org/project/black/
 
Pylint : https://pypi.org/project/pylint/

TestPypi : https://packaging.python.org/en/latest/tutorials/packaging-projects/#packaging-your-project

Inspiration README.md : https://gitlab.com/fabricejumel/rendufinal_bouyssoux/

