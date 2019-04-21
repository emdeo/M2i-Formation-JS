# README (explications)
### Créer une page web demandant les nom, prénom, taille, poids et genre d'un utilisateur, puis affichant son indice de masse corporelle.

## Table des matières
1. [Ressources / raccourcis](#ressources)
2. [En-tête (head)](#head)
3. [Corps (body)](#body)
4. [Insérer un bouton](#bouton)
5. [Script et fonctions](#script)
6. [Sources et fichiers JS](#sources)
7. [Construction d'objets](#objet)

## <a name="ressources">Ressources / raccourcis</a>

Consultez le site de <a href="https://www.w3schools.com/html/tryit.asp?filename=tryhtml_default" target="_top">W3Schools</a> pour tester votre code en ligne en temps réel.

Brève encyclopédie du HTML sur <a href="https://fr.wikibooks.org/wiki/Le_langage_HTML" target="_blank">WikiBooks</a>.

<table align="center">
    <thead>
        <td colspan="2" align="center">Raccourcis sur <em>Visual Studio Code</em> :</td>
    </thead>
    <tbody>
        <tr>
            <td>Formater code</td>
            <td>CTR + SHIFT + F</td>
        </tr>
        <tr>
            <td>Commenter code</td>
            <td>CTR + :</td>
        </tr>
    </tbody>
</table>

## <a name="head">En-tête (head)</a>

Contient les infos générales de la page. Le **title** est obligatoire.

Si l'on veut afficher des caractères spéciaux, il faut également importer les normes UTF-8 dans la balise **meta** (qui sert à donner des infos sur la page aux serveurs et aux navigateurs).

La balise **link** crée un lien avec le fichier **index.css**, qui importe tous les fichiers que nous avons créés pour styliser notre page.

    <head>
        <title>Mon 1er projet JavaScript</title>
        <meta charset="UTF-8" />
        <link rel="stylesheet" type="text/css" href="./assets/stylesheets/index.css" />
    </head>

## <a name="body">Corps (body)</a>

Créer un formulaire qui permettra d'entrer le nom de l'utilisateur.

    <body>
        <form>
            ...
        </form>
    </body>

La balise **table** permet de créer un tableau avec un nombre de lignes et de colonnes définis a posteriori. Le paramètre **border** définit le type d'encadrement du tableau (ligne fine, effet 3D...).

    <table border="1">
        <tr>
            <td>...</td>
            <td>...</td>
        </tr>
        <tr>
            <td>...</td>
            <td>...</td>
        </tr>
    </table>

La balise **tr** permet de **créer une ligne**. La balise **td** permet de **créer une colonne**. Le code ci-dessous crée 1 ligne contenant 2 colonnes (afficher le mot "Taille" puis éditer la valeur de taille).

L'utilisateur peut entrer du texte ou des valeurs grâce à la balise **input**, qui peut prendre plusieurs types (**text**, **button**...). Elle possède plusieurs paramètres :


<table>
    <tbody>
        <tr>
            <td><strong>id</strong></td>
            <td>Permet d'identifer une balise de manière unique</td>
        </tr>
        <tr>
            <td><strong>placeholder</strong></td>
            <td>Affiche un message temporaire dans la zone d'entrée de texte</td>
        </tr>
        <tr>
            <td><strong>required</strong></td>
            <td>N'est pas nécessaire, on l'utilise pour indiquer si une entrée est obligatoire (encadre la zone d'entrée en rouge)</td>
        </tr>
    </tbody>
</table>


    <tr>
        <td>
           Taille
        </td>
        <td>
            <input type="text" id="txtTaille" placeholder="Votre taille" required/>
        </td>
    </tr>

Demander le genre de l'utilisateur : on n'utilise pas de **input** d'un type particulier ! On a recours à la balise **select** pour proposer plusieurs options à l'utilisateur. La valeur de ce **select** dépendra du choix de l'utilisateur.

    <tr>
        <td>Genre</td>
        <td>Vous êtes...</td>
        <td>
            <select id="lstGenre">
                <option value="feminin">une fille</option>
                <option value="masculin">un garçon</option>
            </select>
        </td>
    </tr>

## <a name="bouton">Insérer un bouton</a>

On souhaite afficher, entre deux séries de lignes, un bouton "Calculer IMC".

Ce bouton exécutera une fonction définie dans les balises **script** ou dans le fichier **sources.js** (voir plus bas) chaque fois qu'il sera cliqué (paramètre **onclick="MaFonction()"**) :

    <input type="button" id="cmdCalculer" onclick="Traitement()" value="Calculer IMC">

Afin d'améliorer l'affichage, les paramètres **colspan="2"** et **align="center"** de la balise **td** servent à spécifier l'emplacement du bouton par rapport aux colonnes que nous avons créées.

    <tr>
        <td colspan="2" align="center">
            <input type="button" id="cmdCalculer" onclick="MaFonction()" value="Calculer IMC">
        </td>
    </tr>

## <a name="script">Script et fonctions</a>

La balise **script** permet de créer des variables et des fonctions *propres au fichier* (= on ne peut pas les utiliser depuis un autre fichier .html). On l'ajoute à la toute fin du **body**.

    <script>
        var nb = 12
    </script>

L'expression **document.getElementById()** permet de récupérer un élément de mon fichier pour son **id**.

    <script>
        document.getElementById("txtIMC")
    </script>

On peut afficher le contenu de cet élément à l'intérieur d'un autre élément :

    <script>
        var nb
        document.getElementById("txtIMC").value = nb
    </script>

Ecrire une fonction calculant et affichant l'IMC :

    <script>
        function Traitement() {
            var poids = document.getElementById("txtPoids").value
            var taille = document.getElementById("txtTaille").value
            document.getElementById("txtIMC").value = poids / (taille**2)
        }
    </script>

Une fonction peut en appeler une autre :

    <script>
        function IMC(p,t) {
            return p/(t**2);
        }
        
        function Traitement() {
            var poids = document.getElementById("txtPoids").value;
            var taille = document.getElementById("txtTaille").value;
            
            document.getElementById("txtMin").value = 19*(taille**2);
            document.getElementById("txtIMC").value = IMC(poids,taille);
        }
    </script>

JavaScript est capable d'importer des classes pré-enregistrées (par ex. **Math** et sa méthode **round**). La fonction ci-dessous renvoie une valeur arrondie au centième :

    function arrondi(n) {
        return Math.round(n*100)/100;
    }

On peut créer des *fonctions anonymes*. L'exemple ci-dessous crée une variable fourre-tout nommée **somme**, à laquelle on *affecte* ensuite une fonction :

    var x = 10
    var y = 5
    var somme = function(x,y) { return x + y }
    alert(somme) // affiche "function(x,y) { return x + y }"
    alert(typeof (somme)) // affiche "function"
    alert(somme()) // affiche "NaN"
    alert(somme(2, 5)) // affiche "7"

Une fonction peut également prendre une autre fonction *en paramètre*. Cela permet d'utiliser plusieurs fonctions différentes sur les mêmes paramètres.

    function MaFonction(a,b,f){
        return(f(a,b))
    }

Contrairement aux fonctions *bien déclarées* telles que **MaFonction()**, les fonctions anonymes comme **somme()** ne peuvent pas être appelées avant qu'on ait affecté une fonction à la variable en question.

En d'autres termes, on peut utiliser la fonction **MaFonction()** avant de l'avoir déclarée, mais on ne peut pas utiliser la fonction **somme()** avant de l'avoir déclarée.

## <a name="sources">Sources et fichiers JS</a>

Les fonctions que nous avons créées entre les balises **script** peuvent être stockées dans un fichier JavaScript (= extension **.js**). On peut donc remplacer le contenu de nos balises **script** par :

    <script src="./sources.js"></script>

La norme dit qu'un fichier JS stockant des fonction s'appelle "**sources.js**" Pas besoin de préciser le lien vers ce fichier dans la balise **head**.

Le fichier **source.js** contient la fonction **Traitement()** qui est appelée dans **index.html** (balise **input** de type **button**). Cette fonction s'exécute en 3 étapes :

1 - lire et enregistrer les valeurs entrées par l'utilisateur

2 - enregistrer les caractéristiques de l'utilisateur dans un objet de classe <strong>Personne</strong>

3 - afficher les caractéristiques de l'utilisateur (dans le tableau <strong>ET</strong> dans un message d'alerte)


    function Traitement() {
        var nom = document.getElementById("txtNom").value
        var prenom = document.getElementById("txtPrenom").value
        var poids = document.getElementById("txtPoids").value
        var taille = document.getElementById("txtTaille").value
        var genre = document.getElementById("lstGenre").value

        var p = new Personne(nom, prenom, taille, poids, genre)

        p.Affiche()
    }

## <a name="objet">Construction d'objets</a>

On peut définir n'importe quel constructeur de classe à partir d'une fonction qui crée automatiquement les attributs et les méthodes de cette classe :

    function Point(x, y) {
        // les attributs X et Y sont automatiquement créés, on les initialise avec x et y
        this.X = x
        this.Y = y

        this.Affiche = function(){
            alert("("+this.X+", "+this.Y+")")
        }
    }

Quand la classe est définie, on peut en créer une instance (= objet) à partir d'une variable :

    var p = new Point(6,14)
    p.Affiche()
