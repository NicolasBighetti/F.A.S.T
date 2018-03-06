## Ballistix *(aka Fire.A.S.T)*
**Description:**
Ce projet g�re le tir depuis la tourelle du vaisseau, en se connectant au serveur et en utilisant la webcam afin d'enregistrer la position d'une balle de scratch tir�e sur une cible en tissu adapt�, en en rep�rant la couleur.

**Requis:**
*Ce projet C++ n�cessite Opencv, de version 2.8 au moins afin de fonctionner, ainsi qu'une webcam.*
*Des conditions id�ales d'�clairage sont conseill�es.*

**Pour compiler le projet:**
cmake .
make

**Pour ex�cuter le projet:**
./ballistix [ip_du_serveur] [Optionnel : search_ball_only]

**Fonctionnement:**
L'application a deux fa�on de fonctionner, selon la pr�sence ou non du troisi�me param�tre optionnel.
**Si le troisi�me param�tre est donn�**, l'application affiche 4 croix vertes, repr�sentant les 4 coins o� il est n�cessaire de fixer la cible, et ne rep�re alors que la balle.
**Si le troisi�me param�tre n'est pas donn�**, l'application recherche trois marqueurs de la m�me couleur afin de rep�rer la cible et sa taille, un coin par quart de l'�cran, � savoir en haut � gauche, en haut � droite, et en bas � droite. On peut voir que l'application � rep�r� les trois rep�res et la balle, par les indicateurs du coin sup�rieur gauche,

Quand les �l�ments n�cessaires sont rep�r�s pendant 10 frames (r�glable dans le code), afin de s'assurer qu'il ne s'agit pas simplement d'une erreur, la pr�cision du tir est calcul�e, puis la r�ponse est envoy�e au serveur.
L'application ne d�tecte alors plus pendant 200 frames (r�glable dans le code), temps largement n�cessaire pour marcher vers la balle, la d�tacher de la cible, et s'�carter de la cam�ra avant qu'elle ne recommance � d�tecter.
Il redevient alors � nouveau possible de tirer.

**Calibration:**
A l'execution du projet, plusieurs fen�tres se lancent.
Une repr�sente la cam�ra, avec des croix repr�sentant les objets d�tect�s.
Deux repr�sentent des valeurs HSV minimum et maximum r�glables avec des curseurs, chacune correspondant � une backprojection, � savoir les �l�ments film�es dont la couleur sont compris entre ces minimum et maximums.
De base, l'application est pr�vue pour d�tecter une balle rouge et des rep�res de cible verts, dans une pi�ce obscure �clair�e par une lumi�re forte.
Lors de la calibration, l'objectif est de n'afficher sur la backprojection que les �l�ments que l'on cherche � d�tecter, sans autres objets ni bruit, en d�finissant les minimums et maximums de teinte(H), saturation(S) et valeur(V).
En cas de probl�me, n'h�sitez pas � vous aider d'un color picker HSV pour vous aider.

**Si vous n'arrivez pas � installer OpenCV, il est possible de t�l�charger la VM du cours de Computer Vision:**

> Pour cet enseignement, il est n�cessaire d'avoir install� la librairie
> OpenCV en version 3.3 (ou sup�rieur) que vous pouvez t�l�charger sur
> le site 
> [officiel](https://github.com/opencv/opencv/releases/tag/3.3.0)  ainsi
> que les "contrib"s (opencv_contrib). Il ne reste plus qu'� l'installer
> sur votre ordinateur, ce qui peut prendre un certain temps. Apr�s
> l'avoir t�l�charg�e, vous pourrez suivre 
> [ici](http://docs.opencv.org/3.3.0/df/d65/tutorial_table_of_content_introduction.html)
> les instructions d'installations selon votre syst�me d'exploitation.  
> 
> Vous aurez besoin de  **cmake**  pour pr�parer la compilation. Afin de
> compiler les exemples, il suffit d'invoquer cmake avec l'option:  
> 
> `-DBUILD_EXAMPLES=ON`
> 
> Il suffit ensuite d'ex�cuter les commandes habituelles:  `make`  puis 
> `sudo make install`  
> 
> La librairie OpenCV poss�de un bon nombre de d�pendances mais toutes
> ne sont pas n�cessaires.
> 
> Apr�s l'installation, utilisez un des nombreux exemples pour la
> v�rifier.
> 
> (Pour les installations sous Windows 10 : vous trouverez
> l'installation de PathEditor 
> [ici](https://moodle.polytech.unice.fr/pluginfile.php/64/course/section/41/PathEditor.exe)).
> 
> En cas d'�chec, on vous fournira une  [machine virtuelle Ubuntu 17.04
> avec OpenCV
> 3.3](http://www.i3s.unice.fr/~lingrand/PNSwithOpenCVandpcl.ova). Vous devrez avoir install� virtualbox et les extensions (voir la page de 
> [St�phane
> Lavirotte](http://stephane.lavirotte.com/teach/vm/install.html)  si
> vous ne l'avez pas d�j�) et avoir 30 Go de disponibles.  
> 
> Pour activer le r�seau (NAT) dans la machine virtuelle:
> 
> sudo dhclient enp0s3 -v   sudo ifconfig enp0s3 up  
> #pour tester que le r�seau fonctionne:   ping google.fr  
> #r�ponse du type:  
> #PING google.fr (216.58.210.227) 56(84) bytes of data.  
> #64 bytes from mrs04s10-in-f227.1e100.net (216.58.210.227): icmp_seq=1 ttl=50 time=15.0 ms   \# ...  
>   
> 
>   
> 
> Documentation OpenCV 3.3 :
> [http://docs.opencv.org/3.3.0/index.html](http://docs.opencv.org/3.3.0/index.html)


