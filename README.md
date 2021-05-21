# Tuto Raylib/Blender/Mixamo

Hello ! Apres un rapide regard au sujet, je vois que l'implémentation des animations sur **Raylib** peut être un peu coton. Je me suis penché sur la question, et je vous propose un rapide tuto pour vous expliquer comment télécharger une animation sur **Mixamo**, l'importer sur **Blender**, et l'exporter dans un format accepté par **Raylib**.


# Mixamo
https://www.mixamo.com/#/
Ce site propose de nombreuses animations 3D gratuites, libres au téléchargement.

![test](https://www.dropbox.com/s/upcjbfbfvaznu4t/Mixamo.PNG?dl=1)

Recherchez l'animation qui vous intéresse :

![](https://www.dropbox.com/s/qzxc7avv5zbhv2q/MixamoSearch.PNG?dl=1)

Cliquez sur le resultat, observez l'animation se jouer à droite.
Si vous êtes satisfait de votre recherche, vous allez pouvoir télécharger l'animation :

![](https://www.dropbox.com/s/imes6drhn7dpezb/MixamoDownload.PNG?dl=1)

Cliquez donc sur ce bouton download, vous devriez voir apparaître la fenêtre de dialogue suivante :

![](https://www.dropbox.com/s/ff5nvy6xrgbm6vy/MixamoDownloadSettings.PNG?dl=1)

Ne changez rien, et appuyez sur le bouton "Download".


# Blender

Blender est un éditeur 3D gratuit et open-source, vous pouvez l'obtenir ici :
https://www.blender.org/

Une fois téléchargé et installé, lancez Blender :

![](https://www.dropbox.com/s/6lbhisirl1cmovp/Blender.PNG?dl=1)

Supprimez le cube (cliquez dessus, et appuyez sur Suppr), puis importez votre animation nouvellement acquise :

![](https://www.dropbox.com/s/873k222d10lpzpi/BlenderImport.PNG?dl=1)

![](https://www.dropbox.com/s/dmo1sl5nv86a96m/BlenderPostImport.PNG?dl=1)

Vous devez ensuite reset l'échelle à son format original. Pour ce faire, il vous suffit de cliquer sur "Armature" d'appuyer sur ALT + S :

![](https://www.dropbox.com/s/vy1a8xdf08he2au/BlenderResetScale.PNG?dl=1)

Ensuite, vous devez installer un addon qui permettra à Blender d'exporter votre objet et son animation dans un format qui convient à Raylib. Rendez-vous donc sur ce **GitHub** :
https://github.com/lsalzman/iqm
Et cliquez ici :

![](https://www.dropbox.com/s/6j38ss4hqn0u0uz/BlenderIQMExporter.PNG?dl=1)

Une fois dans ce dossier, téléchargé le fichier python qui s'y trouve :

![](https://www.dropbox.com/s/6opltc7xy9m115n/BlenderIQMExporterPythonFile.PNG?dl=1)

Une fois cette opération terminée, revenons à Blender. Il faut maintenant installer l'addon. Pour ce faire, cliquez sur Edit > Preferences :

![](https://www.dropbox.com/s/uro014oru78vpmy/BlenderAddon.PNG?dl=1)

Cliquez ensuite sur "Install" comme indiqué ici :

![](https://www.dropbox.com/s/ur0kk2tw5s6owrw/BlenderAddonInstall.PNG?dl=1)

Dans la fenêtre qui s'ouvre, trouvez le fichier python que vous venez de télécharger, puis cliquez sur "Install Addon" :

![](https://www.dropbox.com/s/xaavh1u3123wdw2/BlenderAddonInstallFromFile.PNG?dl=1)

Ensuite, si il n'apparaît pas de suite, cherchez "iqm" dans la barre de recherche, et assurez vous de cocher l'addon "Import-Export: Export Inter-Quake Model (.iqm/.iqe)" :

![](https://www.dropbox.com/s/3px1ime3cp08x55/BlenderAddonChecked.PNG?dl=1)

Vous pouvez ensuite exporter le modèle en **.iqm** :

![](https://www.dropbox.com/s/sdieudc9zay2ll9/BlenderExportAsIQM.PNG?dl=1)

Il vous faudra faire deux exports pour que cela fonctionne avec Raylib. Le premier se fait comme ci-dessous. Il ne **FAUT PAS CHANGER LES SETTINGS A DROITE** pour le premier export :

![](https://www.dropbox.com/s/e344im9wo0nvqzn/BlenderExportIQMUntouched.PNG?dl=1)

Une fois que c'est fait, on arrive sur la partie à peine plus technique : l'export de l'animation. Pour cela il va falloir changer le nom de l'animation dans **l'architecture d'objet Blender**. Déroulez "Armature" > "Animation" et changer le nom "mixamo[...]" par le nom que vous souhaitez donner à votre animation :

![](https://www.dropbox.com/s/aroaqbs1snre4zo/BlenderChangeAnimationName.PNG?dl=1)

Ensuite cliquez sur l'icône indiqué par la flèche de gauche sur l'image ci-dessous, qui fera pop le menu suivant, puis cliquez sur "Dope Sheet" :

![](https://www.dropbox.com/s/nuokbdvev0t7bjw/BlenderCheckKeyframes.PNG?dl=1)

Sur la nouvelle fenêtre ouverte, scrollez vers la droite afin de trouver la dernière **keyframe** de votre animation (comme vous le voyez ici, votre animation est représentée par un trait vert sur lequel se trouve des points jaunes, qui représentent les keyframes). Notez le numéro de votre dernière keyframe (ici 372) :

![](https://www.dropbox.com/s/ic2c4uelv8w1feq/BlenderFindLastKeyframe.PNG?dl=1)

Vous allez maintenant pouvoir exporter l'animation. Il faut pour cela répéter la procédure de l'export du **.iqm** précédent. Une fois que vous avez cliqué sur "File" > "Export" > ".iqm", il va falloir changer le nom du fichier (souvent le nom du modèle exporté + "Animation" ou "Anim"), puis ajouter la ligne indiquée par la flèche de droite selon le format suivant : NOM DE L'ANIMATION QUE VOUS AVEZ CHANGE:FRAME DE DEBUT DE L'ANIMATION (toujours 1):FRAME DE FIN DE L'ANIMATION COMME RECUP AU DESSUS:FRAMES PAR SECONDE (je vous conseille 30):1 POUR QUE VOTRE ANIMATION LOOP, 0 SINON
Le **séparateur** entre chacun de ses éléments est un **":"** (exemple ci-dessous) :

![](https://www.dropbox.com/s/ljgsg9r0drw1aki/BlenderExportAnimation.PNG?dl=1)

# Raylib

Maintenant que vos fichiers sont prêts, voici comment les utiliser avec Raylib.
Rendez-vous sur le site de **Raylib** :
https://www.raylib.com/
Cliquez sur "Examples" puis "Models" puis sur l'animation avec le bonhomme jaune :

![](https://www.dropbox.com/s/kaqz3pxbfkf2897/RaylibExample.PNG?dl=1)

Ce code se trouve dans le fichier "**models_animation.c**" dans les exemples qui sont dans le dossier **raylib/examples/models** obtenu après le DL de raylib. Dans ce code, remplacez le path indiqué par **1** par celui vers le fichier model (GangNam.iqm), commentez les lignes indiquées par les flèches, et remplacez le path indiqué par **2** par celui vers le ficher animation (GangNamAnimation.iqm) :

![](https://www.dropbox.com/s/x5zt7371bv7hrwa/RaylibCode1.PNG?dl=1)

![](https://www.dropbox.com/s/icgdlrpyz6ckowv/RaylibCode2.PNG?dl=1)

Une fois que ça c'est fait, compilez le tout (la méthode dépend de votre installation, référez-vous à la doc de l'install Raylib !), puis lancez le binaire **models_animation**. Vous obtiendrez la fenêtre suivante, mais pas de panique, c'est juste ultra zoomé :

![](https://www.dropbox.com/s/riyl4axlvfwm6sh/RaylibExecZoomed.PNG?dl=1)

Dézoomez en scrollant avec votre pad, et voilà :

![](https://www.dropbox.com/s/2vr06dz24whj94a/RaylibExecUnzoomed.PNG?dl=1)

Aaaand ... done ! Vous n'avez plus qu'à rester appuyer sur espace pour voir votre animation se jouer !

Bon courage, j'espère que ça vous aidera !
