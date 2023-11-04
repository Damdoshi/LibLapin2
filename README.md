# LibLapin2

Ce projet n'est pas commencé.
Ce dépot est temporaire et une fois LibLapin2 stabilisée et complétée suffisament pour remplacer LibLapin1, LibLapin1 verra son contenu mis à jour avec celui de LibLapin2.

Quelques idées peuvent être trouvées ici https://github.com/Damdoshi/LibLapin/projects/7

L'objectif de LibLapin 2 est d'être une ré écriture complète de la première LibLapin tout en restant autant que possible compatible,
en permettant la systématisation de certains élément interessant de la LibLapin qui sont resté parcelaire (mécanismes de chargement, lecture, déchifrage, configuration, etc. pouvant etre chainée)
et en éliminant les répétitions qui peuvent être trouvées (bunny_loop, bunny_loop_mw, bunny_start_, bunny_start_style, etc.) La possibilité de configurer n'importe quoi dans n'importe quel
format en particulier est très interessant - même si cela impliquera forcment pour certains formats de réaliser plusieurs systèmes de configuration (node base (ini, dabsic, json) vs array base (xml...))

Un autre objectif est d'exploiter plus fréquemment C++ et de limiter les interfaces internes C pour leur favoriser des interfaces plus C++ienne.
La bibliothèque exterieure demeurera C.

L'ordonnanceur réseau devra être ré écrit et permettre une gestion plus générique des file descriptor, afin de permettre l'adjonction de plusieurs sockets d'ecoute
TCP et l'utilisation d'UDP. Il serait interessant de multithreader les chargements de fichier et de faire contenir aux éléments un champ indiquant si le chargement est terminé ou
non. Une fonction d'attente (ainsi qu'un paramètre) permettrait de s'assurer du chargement complet, quand c'est requis. Il faudrait donc enteriner le bunny thread pool même quand
on utilise pas fast foreach.

Le gestionnaire de ressource doit être totalement détaché des dépendances afin qu'on puisse se passer totalement de SFML -ce qui était le cas avant son existence si on ne
se servait pas du module graphique.

Il faudrait des hashs plus puissant.

Il faudrait probablement simplifier asynclock ou plutot l'expliciter afin d'oser moi meme m'en servir.

Il faut intégrer dès le départ bunny monitor un peu partout afin de faciliter le debug coté game design, et qu'il dispose de GUI pour manipuler des configurations live.

Un autre objectif est d'atteindre une couverture de test frisant les 100%, principalement pour le module de configuration.
Dabsic doit devenir plus fiable et intégrer l'ensemble des éléments précédents, enrichis des éléments nouveaux (mode erreur, définition de type, voir le livre)
Bunny configuration doit être construit sur une classe noeud plus riche et gérant l'intégralité des aspects qui ici ont parfois été ajouté après et source d'erreur.
En même temps, les fonctions et expressions ne doivent plus etre conservé a un format d'arbre à parcourir mais être compilé en sequence afin de permettre
l'écriture à l'avenir de debugger et également pouvoir se placer a une position intermediaire facilitant les tests.
De plus, les performences du module de configuration sont minables. Si ses capacités sont très interessantes, il convient d'améliorer les performences de manière drastique.
Les litteraux doivent également être enrichi, afin de permettre d'établir comme valeur des noeuds ou des tableaux complets.
Le type pointeur est également mysterieux...

Il faut écrire des tutoriaux en même temps que ré écrire chaque module.
Il faut documenter les fichiers .h de sorte a ce qu'il puisse etre possible de les lire comme étant une doc.
Il serait interessant de les redécorer comme avant la 1.8 pour les rendre sympa à parcourir.
Il faut créer un format d'auto documentation satisfaisant pour la LibLapin - je n'aime ni le rendu de doxygen ni l'uatre dont j'ai oublié le nom. En utilisant libcrawler pour
parcourir les .h, je devrais pouvoir extraire les commentaires de descriptions des éléments de la Lib et en sortir un site web dans le style de ce qui est liblapin.org.

L'allocateur de la LibLapin n'a peut etre pas de raison d'être: l'idée consistant à générer un espace mémoire contrôlé pour permetre la sauvegarde du tas et la correction des pointeurs est interessante mais risque de compromettre la stabilité de l'ensemble de la bibliothèque.

Les conteneurs pourraient être basé sur ceux de C++ pour les plus complexes, sinon basé au choix sur ds tableaux ou des listes pour les plus simples.

L'appel de fonction via le style "nommé" devra être utilisé et devra être renud accessible via un suffixe ajouté au nom des fonctions.
Ce mécanisme sera terribleement utile pour les fonctions prenant beaucoup de paramètres, et disposer d'un suffixe plutot que d'une unique fonction
permettra de tout de meme proposer une API simple utile lors des cours de programmation graphique.

Le nouveau pixelarray doit pouvoir faire du 64b (full float) 32b 24b 16b 8b 4b 2b 1b.
Le nouveau t_bunny_effect doit permettre de gérer en plus du sample par seconde un nombre de canaux indéterminé (mono, stéreo, etc.)

Il faut permettre la construction d'un module de type .deb et d'un .rpm qui pourraient etre ajouté a des repos.
Il faut un discord LibLapin a coté du site, ou un forum de discussion.

Le système de "scream log", "scream error" est beaucoup trop verbeux, beaucoup trop casse pied à manipuler, et son implémentation à base de macro est très embetante.
Il faut inventer un nouveau mécanisme qui permette d'améliorer ces éléments. L'un des principaux défaut est le mélange des erreurs de type "impossible de faire X",
et des erreurs de type "je ne trouve pas X" (dans une liste ou finalement, bah, X sera trouvé, sauf que chaque essai donne un log...). Peut etre que la fonction appelante
devrait être responsable d'indiquer si oui ou non le log interesse?



