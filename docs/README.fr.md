# ITI 1121 - Lab 10

## Submission

Lire le [junit instructions](JUNIT.en.md) au besoin pour aider
avec les tests du lab.

Lire le [guides de soumission](SUBMISSION.fr.md) avec attention.
Les erreurs de soumission vont affecté votre évaluation.

Soumettez les réponses aux

* OrderedStructure.java
* OrderedList.java

# Première partie.

## Objectifs d'apprentissage

* **Concevoir**  une liste doublement chaînée possédant aussi un noeud factice.
* **Modifier** l'implémentation d'une liste chaînée afin d'y ajouter des méthodes.
* **Résoudre** des problèmes exigeant une bonne compréhension des interfaces.


## Tableau circulaire

Les files sont un type abstrait de données reposants sur le principe du premier arrivé premier servi (Fisrt In First Out - **FIFO**). Leur implémentation à l'aide d'un tableau utilise une technique que l'on nomme tableau circulaire. Dans un tableau circulaire, on réutilise les cellules du début du tableau lorsque l'arrière de la file atteint la fin du tableau et que le tableau n'est pas rempli. Cette implémentation d'une file a une variable d'instance qui désigne l'avant de la file (head/front) et une pour l'arrière (tail/rear).

Lorsque l’on ajoute un élément en utilisant **enqueue()**, on ajoute un élément à la position **arrière (tail)** et on incrémente le pointeur **tail (rear)**. Lorsque l’on enlève un élément en utilisant **dequeue()**, on enlève et retourne l’élément a la position **avant (head)** et incrémente le pointeur **head (front)**

Voici une représentation graphique d’un tableau circulaire. Nous pouvons soit la représenter comme un tableau ou le dernier élément est lié au premier, ou encore comme un tableau circulaire.

![Image circular_queue](lab10_circular_queue.png)
**Figure 1 :**  Représentation visuelle des tableaux circulaires.

## Les listes simplement et doublement chaînées

**Rappel**: Comme vu en classe, il existe plusieurs implémentations d'une liste avec des éléments chaînés. Nous vous avons notamment présenté les listes **simplement** et **doublement** chaînées en classe. Ces implémentations, bien que semblables possèdent des différences notables.

D'un côté, les **listes simplement chaînées** relient chaque élément à leur prochain, et ce, jusqu'au dernier élément qui aura pour suivant (next) **null**.

D'un autre côté, les **listes doublement chaînées** permettent l'implémentation plus rapide de certaines méthodes grâce au lien qui relie chaque élément à son précédent. Le dernier élément aura, telle la liste simplement chaînée, un prochain (next) **null**, tout le comme le premier élément qui a un précédent (prev) **null**.

Il y a aussi possibilité d'implémenter une liste simplement ou doublement chaînée avec un **noeud factice**, c'est-à-dire un noeud qui n'aura aucune valeur (**null**) et qui sera placé au début de la liste. Ce dernier permet de simplifier l'implémentation de méthodes en réduisant le nombre de cas spéciaux et rend aussi la liste **circulaire** puisque le premier élément de la liste aura ce noeud en élément précédent et le dernier élément l'aura en élément suivant.

## Testez votre compréhension des différentes implémentations.

### Question 1.0 :

Décrivez la figure suivante. Notamment, s'agit-il d'une liste simplement ou doublement chaînée? Comment s'appelle la technique utilisée (un noeud ...)?

![Image An empty list](lab9_img1_dummy_list-00-00.png)

**Figure 1 :** Une liste vide.

<details><summary>Réponse</summary>
<p>
Il s'agit d'une liste doublement chaînée avec noeud factice.
</p>
</details>


### Question 1.1 :

Vrai ou faux? Il est possible de parcourir une liste simplement chaînée dans les deux directions efficacement.

<details><summary>Réponse</summary>
<p>
Faux, nous avons besoin d'une liste doublement chaînée!
</p>
</details>


### Question 1.2 :

Que devons-nous utiliser pour faciliter l'ajout d'un élément à la fin d'une liste?

<details><summary>Réponse</summary>
<p>
Une référence vers l’élément arrière!
</p>
</details>


### Question 1.3 :

Vrai ou faux? Une liste circulaire possédant un noeud factice a plusieurs cas particuliers.

<details><summary>Réponse</summary>
<p>
Faux. Au contraire, le noeud factice réduit significativement le nombre de cas particuliers à traiter!
</p>
</details>

### Question 1.4 :

Dans quel contexte l'utilisation de l'implémentation d'une liste à base de tableaux est-elle avantageuse à celle d'une liste à base d'éléments simplement chaînés? Nommez 2 méthodes.

<details><summary>Réponse</summary>
<p>
La méthode <b>void removeLast()</b> et <b>E get(int pos)</b>. Pouvez-vous expliquer pourquoi les temps d'exécution sont lents (varient) pour une liste à base d'éléments chaînés?
</p>
</details>


### Question 1.5 :

Avons-nous besoin d'une variable de référence <b>tail</b> dans le cas d'une liste circulaire doublement chaînée?

<details><summary>Réponse</summary>
<p>
Non! En effet, que pouvons-nous plutôt utiliser pour accéder l'arrière de la liste? <b>head.prev</b>
</p>
</details>

### Question 1.6 :

Vrai ou faux? Pour implémenter une liste chaînée, nous pouvons tout simplement utiliser un tableau dynamique.

<details><summary>Réponse</summary>
<p>
Faux. Ne mélangez pas les concepts! Une liste peut être implémenté par un tableau ou par des éléments (simplement et doublement) chaînés.
</p>
</details>

### Question 1.7 :

Voici le constructeur de la classe imbriquée Node d'une List. Identifiez si la liste est simplement ou doublement chaînée.

```java
//constructor
private Node(T value, Node next) {
  this.value = value;
  this.next = next;
}
```
<details><summary>Réponse</summary>
<p>
Il s'agit d'une classe <b>simplement chaînée</b> comme le constructeur n'a pas de paramètre pour prev, soit le Node précédent.
</p>
</details>


### Question 1.8 :

Qu'est-ce que le bout de code suivant effectue dans une liste circulaire doublement chaînée? Considérez que la variable current a été préalablement déclarée.
```java
current = head.prev;
while (current != head) {
  current = current.prev;
}
```
<details><summary>Réponse</summary>
<p>
Il traverse la liste du dernier au premier élément.
</p>
</details>

# Deuxième partie.

## OrderedStructure

Vous êtes maintenant prêt à appliquer vos connaissances. Consultez les notes du cours concernant l'implémentation d'une liste doublement chaînée au besoin. Référez-vous aux images en [appendice](#appendice) afin de mieux visualiser votre liste. N'hésitez pas à faire vos propre dessins lorsque vous écrivez votre implémentation!

Pour ce laboratoire, vous devez créer une implémentation de l'interface **OrderedStructure** à l'aide de noeuds **doublement chaînés** et d'un **noeud factice**. L'interface OrderedStructure déclare les méthodes suivantes:
```java
public interface OrderedStructure {
  int size() ;
  boolean add(Comparable element) throws IllegalArgumentException;
  Object get(int pos) throws IndexOutOfBoundsException;
  void remove(int pos) throws IndexOutOfBoundsException;
}
```
Les classes implémentant cette interface doivent sauvegarder les éléments **en ordre croissant** les éléments. L'ordre de ces derniers est défini par l'implémentation de la méthode **compareTo(Object other)** que déclare l'interface **Comparable**. Les classes **Integer** et **String** implémentent toutes les deux cette interface et peuvent donc servir pour vos tests.

**IMPORTANT :** puisque l'objectif principal du laboratoire est de bien maîtriser les concepts liés à l'implémentation des listes chaînées, par souci de simplicité, **nous n'utiliserons pas le concept de type générique («generics»)**. Ainsi,

1.  Le compilateur produira quelques avertissements
2.  Mais surtout, les utilisateurs de la méthode get devront forcer une conversion de type puisque la valeur de retour est de type Object.


## OrderedList

1.  Créez une classe **OrderedList** qui réalisera l'interface **OrderedStructure**. L'implémentation de OrderedList doit utiliser des noeuds doublement chaînés, ainsi qu'un noeud factice. La classe doit posséder une référence **head** vers le noeud factice. De plus, votre implémentation **doit lancer toutes les exceptions nécessaires**. Voici les fichiers à partir desquels vous pouvez commencer votre travail :

* OrderedStructure.java
* OrderedList.java
* [Documentation](http://www.site.uottawa.ca/%7Eturcotte/teaching/iti-1521/lectures/l09/doc/OrderedStructure.html)

Nous allons développer cette implémentation étape par étape, de haut en bas. C'est-à-dire que nous allons d'abord implémenter les éléments de haut niveau (variables d'instance, classe imbriquée statique, et des coquilles pour chacune des méthodes). Une fois tout ça en place, nous implémenterons le corps des méthodes, une à une.

a.  Premièrement, vous devez créer une définition initiale de **OrderedList**. Pour l'instant, nous ignorons l'implémentation des méthodes afin de nous concentrer sur les variables et la nécessité d'une classe « static » imbriquée afin de représenter les noeuds de la liste. Pour satisfaire les exigences du compilateur, toutes les méthodes de l'interface **OrderedStructure** doivent être déclarées. La classe doit donc contenir une classe **Node**, les **variables d'instance** et des **déclarations vides** pour chacune des méthodes de l'interface. Vous ne devez pas utiliser de variables **int size**. D'autant plus, sachez que notre classe **Node** doit sauvegarder des valeurs de type **Comparable**


Attention, le compilateur n'acceptera pas des déclarations vides pour les méthodes retournant une valeur. Vous pourriez inclure un énoncé de retour bidon, par exemple retourner la valeur -99 pour la méthode **size**, sachant que cet énoncé sera remplacé par une implémentation complète éventuellement.

**Cependant**, il se peut que vous oubliiez de faire ces changements et l'ensemble de la classe deviendrait difficile à déboguer. Pour cette raison, je préfère créer une définition initiale ne contenant que l'énoncé suivant.

```java
int size(){
  throw new UnsupportedOperationException("not implemented yet!");
}
```
Faites de même pour chacune des méthodes de votre classe.

Ça nous permet de compiler la classe et de travailler sur l'implémentation des méthodes une à une. Toute tentative d'utiliser une méthode qui n'a pas encore d'implémentation sera signalée par une exception ! Vous pouvez demander des explications supplémentaires à votre aide à l'enseignement si nécessaire.

Créez une classe test, **OrderedListTest**. Pour l'instant, elle ne contient qu'une méthode principale déclarant une variable de type OrderedList, désignant un objet OrderedList.

Assurez-vous que l'implémentation partielle de **OrderedList** comprenne tous les éléments ci-haut et qu'elle compile parfaitement. Lorsque ce sera fait, vous pouvez procéder à la prochaine étape, soit l'implémentation de la méthode size.

a.  Implémentez la méthode **size()**. Pour ce faire, remplacez l'énoncé **throw** par une implémentation itérative traversant la liste et comptant ses éléments.Ajoutez un test à la classe **OrderedListTest** afin de vous assurer que la méthode fonctionne pour la liste vide. Nous ajouterons d'autres tests lorsque nous aurons une méthode **add**.

b.  Implémentez la méthode **boolean add(Comparable obj)** . La méthode ajoute un élément à la liste en ordre croissant selon l'ordre naturel imposé par la classe de l'objet (c.-à-d. vous devez utiliser sa méthode **compareTo**). Elle retourne **true** si l'élément a été ajouté à cette liste ordonnée, **false** sinon.

c.  Ajoutez quelques tests afin de valider la méthode add. Il sera difficile d'évaluer la méthode proprement, mais au moins la taille de la liste devrait s'accroître à mesure que des éléments y sont ajoutés à la liste.

d.  Implémentez **Object get(int pos)**. Cette dernière retourne l'élément se trouvant à la position spécifiée de cette liste ordonnée ; le premier élément se trouve à la position 0. Cette opération ne doit pas transformer la liste.

e.  Ajoutez des tests afin de valider les méthodes **get** et **add**. Nous sommes maintenant en bien meilleure position pour évaluer les méthodes **add, get** et **size**. En particulier, nous pouvons ajouter des éléments, utiliser une boucle afin d'accéder aux éléments un à un à l'aide de la méthode **get**. Assurez-vous que toutes les méthodes fonctionnent bien avant de poursuivre. N'oubliez pas que votre méthode **get** retourne un élément de type **Object**, vous devrez donc forcer sa conversion dans le type choisi lors de vos tests (cast).

f.  Implémentez **void remove( int pos );** La méthode retire l'élément à la position spécifiée de cette liste ordonnée ; le premier élément se trouve à l'index 0.

g.  Ajoutez des tests afin de valider la méthode **remove**. Assurez-vous que cette méthode fonctionne (ainsi que les autres) avant de poursuivre.

Nous avons maintenant une implémentation complète de l'interface OrderedStructure.

2.  Ajoutez la méthode d'instance **void merge(OrderedList other)** qui ajoute tous les éléments de la liste **other** à cette liste tout en préservant l'ordre des éléments. Par exemple, si **a** et **b** sont deux listes ordonnées telles que a contient “D”, “E” et “G”, et **b** contient “A”, “C”, “D” et “F”, alors l'appel **a.merge(b)** transforme a de sorte qu'elle contient maintenant les éléments suivants “A”, “C”, “D”, “D”, “E”, “F” et “G” , tandis que **b** demeure inchangée par cet appel. La classe String implémente l'interface Comparable et peut être utilisée pour tester votre méthode.

Cet exercice a pour but d'apprendre à traverser et transformer des listes doublement chaînées. Ainsi, vous ne devez pas utiliser des méthodes auxiliaires, en particulier, n'utilisez pas la méthode **add** !

Votre implémentation doit traverser les deux listes et insérer les éléments (valeurs) de l'autre liste dans celle-ci ; en ordre croissant. **Rappelez-vous qu'il est préférable de développer ces habiletés maintenant, plutôt qu'à l'examen final !**

3. **Sujet avancé et optionnel** :

a.  Utilisez votre implémentation de la classe OrderedList comme point de départ afin de créer un type générique («generics») qui réalise l'interface OrderedStructure suivante :

```java
public interface OrderedStructure <T extends Comparable<T>> {
  int size();
  boolean add(T elem) throws IllegalArgumentException;
  T get(int pos) throws IndexOutOfBoundsException;
  void remove(int pos) throws IndexOutOfBoundsException;
}
```

L'un des avantages marqués de cette implémentation sera que tous les éléments de la liste auront le même type. Ce qui est très important pour la méthode compareTo.

b. Implémentez maintenant votre classe **OrderedList** sans utiliser de noeud factice. Que constatez-vous? Bien que plus longue, cette implémentation vous apprendra l'importance de bien traiter chaque cas particulier un à un, et ce, dans chaque méthode.


### Appendice

![An empty list](lab9_img1_dummy_list-00-00.png)
**Figure 1 :** Une liste vide.

![A list with one element](lab9_img2_dummy_list-01-00.png)
**Figure 2 :** Une liste contenant un seul élément.

![A list with two elements](lab9_img3_dummy_list-02-00.png)
**Figure 3 :** Une liste contenant deux éléments.

![A list with three elements](lab9_img4_dummy_list-03-00.png)
**Figure 4 :** Une liste contenant trois éléments.

**Section plus avancée :** ce concept vous sera utile pour le reste de vos études et possiblement au travail.


# Troisième partie

## Objectifs d'apprentissage

* Comprendre le concept de **version de contrôle** et son importance.
* Apprendre les bases du système de contrôle de versions **Git** ainsi que son service d'hébergement **GitHub**.
* Apprendre les commandes de base de Git, telles que git **init**, git **add**, git **commit**, git **push**, git **pull**.
* **Présenté** à fin d'introduction pour les étudiants n'ayant jamais appris à utiliser Git auparavant.

## Pourquoi apprendre Git?

Un problème commun lors que l'on manipule de l'information stockée sur un ordinateur est **la gestion des changements**. Par exemple, après l'ajout, la modification ou la suppression de texte, vous voulez parfois annuler vos changements (mais toutefois les faire plus tard). À niveau simple, ce problème est souvent résolu en cliquant **undo** ou précédent dans notre éditeur de texte (annuler notre action précédente).

Une méthode plus naïve pour gérer nos différents changements est l'usage de plusieurs fichiers pour chaque version, et ce, simplement en créant des copies du fichier avec différents noms et changements (Important_Document_V4_FINAL_FINAL.doc vous semble malheureusement peut-être familier). À un niveau plus avancé, vous voulez souvent partager ces fichiers avec d'autres personnes, plutôt que de simplement faire et défaire des changements, revoir vos échanges par courriel pour savoir qui a changé quoi, pourquoi, quand, quel était son but, quel était le changement, pour pouvoir conserver des versions différentes du document en parallèle, un système de gestion de version (comme Git) vous permettra d'effectuer toutes ces opérations et bien plus!

Un système de contrôle de version peut donc résoudre tous vos problèmes de révision de versions et de retour en arrière en permettant l'utilisation multiple d'un même fichier sans le dupliquer. Il permet aussi la collaboration de ce même fichier par plusieurs personnes. Pour ces raisons, plusieurs organisations et entreprises utilisent un système de gestion de versions dans le but de garder la trace des différents changements dans le code source et les autres fichiers textes durant le développement d'un logiciel. Ces systèmes ont une grande quantité de fonctionnalités allant de la sauvegarde, la mise à jour et la conservation de traces de tout changement effectué.

Il y a deux modèles (types) de logiciel de contrôle de version : le **Client-Server model** et le **Distributed model**.

* **Client-Server model**: Les développeurs utilisent un seul dossier qu'ils partagent. Quelques exemples:
    * Open source: CVS, Subversion, Vesta, etc.
    * Propriétaire: Microsoft Team Founday, Helix, etc.
* **Distributed mode**: Chaque développeur travaille directement et localement avec son dossier et les changements sont échangés entre leurs dossiers uniquement lorsque demandé. Par exemple:
    * Open source: **Git**, SVK, Fossil, etc.
    * Propriétaire: Visual Studio Team Services, Plastic SCM, etc.

Vous avez peut-être appris à utiliser certains de ces systèmes de contrôle de version, mais pour cette section, nous nous concentrerons sur le système de contrôle de versions **Git**.

Git est le choix souvent le plus populaire (à apprendre et à utiliser), car il s'agit de code source ouvert, est facile à apprendre, ne prend quasiment aucun espace mémoire et est des plus performant côté rapidité. Il surclasse plusieurs ds autres outils avec ses fonctionnalités.

Utiliser un système de contrôle de version est souvent bien utile lorsque vous travaillez sur un projet en équipe, où encore lorsque vous avez l'option de partager publiquement votre projet (tel qu'en partageant un lien sur votre profil LinkedIn. Cela rend la tâche plus facile pour les compagnies qui cherchent à vous engager et qui désirent voir de quelle manière vous résolvez des problèmes et votre manière de coder, et ce, en se basant sur votre historique de projet. De plus, une connaissance de tels systèmes est définitivement un plus que les compagnies recherchent lorsqu'elles engagent des étudiants.

## Introduction à Git

**Git** est un système de contrôle de version qui vous permet d'enregistrer tout changement à votre code ainsi que votre collaboration à celui d'autrui. Un Git **Repository** est en d'autres mots un dossier géré par Git où tous les changements au contenu sont enregistrés. Après avoir installé Git, vous pouvez transformer tous vos dossiers en Git Repository en tapant la commande suivante:
```bash
git init
```
La meilleure façon d'illustrer Git est l'enregistrement d'une capture d'écran instantanée de votre code.

1.  Vous faites des changements à vos fichiers.
2.  Vous sélectionnez les fichiers que vous voulez placer dans votre prochaine capture.
3.  Vous créez cette capture avec un message de description. Nous appelons ces captures des "**commits**".

### Git Local

Disons que nous avons un dossier contenant des fichiers sur notre ordinateur local dans « my_folder ».

* index.html
* about.html
* home.html
* contact.html
* style.css
* main.js
* README.txt

Et disons que nous effectuons des changements dans des fichiers de ce « my_folder » ...

* index.html
* [red]about.html
* [red]home.html
* contact.html
* [red]style.css
* main.js
* README.txt

Ainsi, la suite d'actions typiques pour commettre ces changements dans Git tel qu'illustré à la **Figure 1** serait:

1.  Faire des changements
2.  git status
3.  git add \<files\>
4.  git commit -m "Message"

Note: la commande "git status" affiche l'état de votre dossier auquel vous travaillez actuellement ainsi que les fichiers qui seront ajoutés à votre « commit ». Avant d'ajouter et de commettre ces changements, il est préférable de vérifier qu'est-ce que votre « commit » inclu et exclu.

AStuce: "git add ." est une commande commune pour ajouter tous les fichiers modifiés à ceux inclus dans le « commit ».

![Typical Workflow](lab10_gitintro.png)

**Figure 1 :** Typical Workflow

### Git Remote

Après un certain temps, vous vous retrouverez avec plusieurs captures et « commit ». Comment les partager avec vos coéquipiers? Avec Git Remote, vous vous mettez d'accord sur un endroit central où vous synchroniserez vos dossiers. Ensuite, vos coéquipiers peuvent aussi **synchroniser** leurs dossiers et fichiers dans cet endroit central que l'on appelle un “**Git Remote Repository**”.

Les Remote Repositories (dossiers à distance) sont uniquement des Git Repositories avec lesquels vous synchroniser vos données. Après chaque synchronisation, votre dossier local (local repository) et le dossier à distance (remote repository) contiene exactement les mêmes informations (toutes les captures, commits, etc.). Vous pouvez choisir n'importe quel endroit pour votre Git Remote repository, mais nous utiliserons un service appelé **GitHub** pour héberger notre dossier git à distance, tel qu'illustré dans la **Figure 2**.

![GitHub Remote Repository](lab10_gitremote.png)

**Figure 2 :** GitHub Remote Repository.

Pour débuter la synchronisation avec un Remote repository, vous devez

1.  Créer un Remote Repository sur Github.
2.  Ajouter son adresse à votre propre ordinateur (local)


Par exemple:
```bash
git add remote origin git@github.com:myusername/myRepoName.git
```
### Git Push

Comment synchroniser votre dossier local avec celui à distance? D'abord vous pouvez poussez (push) vous changement au dossier à distance.

```bash
git push <name of remote> <name of branch>
```
Par exemple:

```bash
git push origin master
```
### Git Pull

Vous pouvez obtenir (pull) les changements les plus récents au dossier à distance en utilisant :

```bash
git pull
```
Vos coéquipiers peuvent aussi obtenir les dernières versions en utilisant ces commandes. Il est recommandé d'utiliser git pull en premier pour obtenr les derniers changments, avant d'utiliser git push.

### Méthode recommandé pour une pratique personnelle :

1.  Installez Git ([https://git-scm.com/downloads](https://git-scm.com/downloads)).
2.  Essayez Git localement sur votre ordinateur.
3.  Créez vous un compte GitHub ([https://github.com/](https://github.com/)) (Utilisez votre adresse courriel étudiant pour obtenir gratuitement la version avancée!). **ATTENTION: GitHub utilise des dossiers privés et publics. Si vous travaillez sur un devoir, assurez-vous que le dossier est PRIVÉ pour éviter de mauvaises surprises!**
4.  Mettez en place un dossier à distance personnel (a personal remote repository) sur GitHub
5.  Pratiquez-vous à pousser (push) et obtenir (pull) de l'information

## References

Introduction à Git provient des notes de Casey Li [slides](https://docs.google.com/presentation/d/1dC-IEpPy4c9-FbBw02gPP4Jk8mR7z8V4OsBUqjLXmm4/). Pour davantage d'information sur GIT, nous recommandons fortement le vidéo suivant : ["Gitting to Know You"](http://www.caseyli.com/videos).

### Resources

* [https://docs.oracle.com/javase/tutorial/getStarted/application/index.html](https://docs.oracle.com/javase/tutorial/getStarted/application/index.html)
* [https://docs.oracle.com/javase/tutorial/getStarted/cupojava/win32.html](https://docs.oracle.com/javase/tutorial/getStarted/cupojava/win32.html)
* [https://docs.oracle.com/javase/tutorial/getStarted/cupojava/unix.html](https://docs.oracle.com/javase/tutorial/getStarted/cupojava/unix.html)
* [https://docs.oracle.com/javase/tutorial/getStarted/problems/index.html](https://docs.oracle.com/javase/tutorial/getStarted/problems/index.html)