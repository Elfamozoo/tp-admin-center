# Fiche Technique

*Gestion d’un domaine Active Directory avec Windows Admin Center*

![image-01.jpeg](assets/image-01.jpeg)

## Sommaire

- [Objectif](#objectif)
- [Définition brève](#définition-brève)
- [Prérequis](#prérequis)
- [Tâches](#tâches)
  - [1. Installation de Windows Admin Center](#1-installation-de-windows-admin-center)
  - [2. Ajout du contrôleur de domaine](#2-ajout-du-contrôleur-de-domaine)
  - [3. Gestion via Windows Admin Center](#3-gestion-via-windows-admin-center)
  - [4. Vérification :](#4-vérification-)

| Rédigé par | Illyes Zerga |
|---|---|
| Date | 03/07/25 |

## Objectif

Installer et configurer Windows Admin Center sur un client Windows pour gérer à distance un contrôleur de domaine Active Directory, puis effectuer des tâches d’administration via son interface graphique.

## Définition brève

Windows Admin Center est une interface graphique web permettant de gérer à distance des serveurs et clients Windows, y compris les contrôleurs de domaine Active Directory, sans utiliser les outils traditionnels comme RSAT.

## Prérequis

- Un contrôleur de domaine (DC) Windows Server configuré avec Active Directory et DNS.

- Un client Windows (ex. Windows 10/11 Pro) intégré au domaine.

- Accès administrateur sur le DC et le client.

## Tâches

### 1. Installation de Windows Admin Center

- On va donc commencer par l’installation de Windows Admin Center sur le poste Client-1 :

![image-02.png](assets/image-02.png)

- On va choisir l’installation personnalisé

![image-03.png](assets/image-03.png)

- Ensuite ici ont choisi **Accès a distance**

![image-04.png](assets/image-04.png)

- On choisit **Connexion au formulaire HTML** cela va permettre à l’utilisateur de saisir son nom et mot de passe dans une page Web

![image-05.png](assets/image-05.png)

- On laisse le port HTTPS par défaut

![image-06.png](assets/image-06.png)

- Nous n’avons pas de certificat officiel émis par une autorité on choisit donc l’autre option

![image-07.png](assets/image-07.png)

- On choisit le nom du réseau accessible a distance

![image-08.png](assets/image-08.png)

- On autorise uniquement l’accès réseau aux ordinateurs du domaine

![image-09.png](assets/image-09.png)

- On laisse le choix par défaut ici la communication via http.

![image-10.png](assets/image-10.png)

- On autorise les MAJ a s’effectuer automatiquement comme recommandé

![image-11.png](assets/image-11.png)

- Choisissiez l’option qui vous plait ici.

![image-12.png](assets/image-12.png)

- Vous pouvez choisir ou placer le dossier raccourci.

![image-13.png](assets/image-13.png)

- On a un résumé de l’installation et on va pouvoir confirmer en cliquant sur **Installer**

![image-14.png](assets/image-14.png)

- Vous devriez avoir cela a la fin de l’installation avec une invitation a ouvrir la page Web

![image-15.png](assets/image-15.png)

![image-16.png](assets/image-16.png)

### 2. Ajout du contrôleur de domaine

- Nous allons donc nous connecter à Windows Admin Server en utilisant un utilisateur de notre domaine :

![image-17.png](assets/image-17.png)

- Voilà ce que vous devriez voir :

![image-18.png](assets/image-18.png)

- Afin d’ajouter le contrôleur de domaine ( le serveur ) dans la barre du haut, cliquez sur **Ajouter** (bouton « + Ajouter »).
- Vous devriez avoir cela qui apparait. Nous allons ajouter un serveur.

![image-19.png](assets/image-19.png)

- Ici on ajoute le nom complet du serveur et on clique sur Ajouter

![image-20.png](assets/image-20.png)

- On le retrouve bien dans la liste des équipements :
- On va donc cliquer sur `<SERVEUR>`.<domaine> afin de s’y connecter :

![image-21.png](assets/image-21.png)

- Voila la page d’accueil du Serveur :

![image-22.png](assets/image-22.png)

- Et voici celle du client qui est aussi manageable via l’interface Admin Center :

![image-23.png](assets/image-23.png)

### 3. Gestion via Windows Admin Center

- La gestion du DNS n’étant pas présent de base dans les outils nous allons devoir l’ajouter pour se faire nous allons dans les paramètres puis dans l’onglet **Extensions** :

![image-24.png](assets/image-24.png)

- Ici nous allons chercher l’extension « DNS » et l’installer :

![image-25.png](assets/image-25.png)

- L’extension est bien installée

![image-26.png](assets/image-26.png)

- Et on la retrouve bien lorsque que on va sur l’interface du contrôleur de domaine :

![image-27.png](assets/image-27.png)

- Dans la zone de recherche Directe du domaine on va **créer un enregistrement DNS**

![image-28.png](assets/image-28.png)

- Dans la case Adresse IP, saisir l’IPv4 statique de ton hôte `<POSTE>` (c’est-à-dire l’adresse attribuée dans notre réseau ici `<IP_DU_SERVEUR>`).
- Type d’enregistrement DNS : Hôte (A)
- Nom d’enregistrement : `<POSTE>`
- Nom de domaine complet : `<POSTE>`.<domaine> (affiché en lecture seule)
- Durée de vie (TTL) : laissez 3600
- Une fois le champ Adresse IP rempli, cliquez sur Créer afin de valider l’enregistrement DNS.

![image-29.png](assets/image-29.png)

![image-30.png](assets/image-30.png)

- Ensuite pour ajouter un utilisateur dans AD via Windows Admin Center on va installer l’extension Active Directory comme pour l’extension DNS précédemment.

![image-31.png](assets/image-31.png)

- Ensuite lorsque l’extension est installée on va ajouter un utilisateur comme ceci :

![image-32.png](assets/image-32.png)

- Ensuite on remplit le formulaire d’ajout d’utilisateur :

![image-33.png](assets/image-33.png)

- Ensuite on active l’utilisateur (ici grisé car déjà activé)

![image-34.png](assets/image-34.png)

### 4. Vérification :

- L’utilisateur que l’on a crée précédemment sur le Windows Admin Center est bien visible et actif sur le Contrôleur de Domaine :

![image-35.png](assets/image-35.png)

- L’enregistrement DNS est présent dans la zone DNS du contrôleur de domaine :

![image-36.png](assets/image-36.png)
