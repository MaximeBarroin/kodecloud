https://github.com/janaom/KodeKloud-Engineer-2.0/blob/main/Docker_1/1_Install_Docker_Package.md

   I want to ssh stapp02	172.16.238.11	stapp02.stratos.xfusioncorp.com	steve	Am3ric@	Nautilus App 2
stapp01	172.16.238.10	stapp01.stratos.xfusioncorp.com	tony	Ir0nM@n	Nautilus App 1
```bash
ssh  steve@172.16.238.11
 puis taper le mot de passe
```
 ensuite super admin 
```bash
sudo su -
```

puis on prend le repo docker compose 
curl -L "https://github.com/docker/compose/releases/download/1.28.6/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

ls -la /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

ls -la /usr/local/bin/docker-compose



[5044] Error loading Python lib '/tmp/_MEI2QGfVl/libpython3.7m.so.1.0': dlopen: libcrypt.so.1: cannot open shared object file: No such file or directory
```bash
docker-compose --version
```
If you encounter the error `Error loading Python lib '/tmp/_MEI2QGfVl/libpython3.7m.so.1.0': dlopen: libcrypt.so.1: cannot open shared object file: No such file or directory`, it indicates that the required library `libcrypt.so.1` is missing from your system.
To resolve this issue, you can try the following steps:
1. **Install the missing library**: You can install the `libcrypt` library using the package manager for your distribution. For example, on Ubuntu or Debian-based systems, you can use:

```bash
sudo dnf install libxcrypt-compat


sudo yum config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

yum install docker-ce docker-ce-cli containerd.io


rpm -qa |grep docker

systemctl enable docker


systemctl start docker

systemctl status docker


docker --version

docker ps (to check if docker is running)

docker-compose --version


Voici une brève synthèse des actions décrites dans ce document markdown pour l'installation de Docker :

Synthèse de l'installation Docker
1. Connexion au serveur
SSH vers le serveur stapp02 (172.16.238.11) avec l'utilisateur steve
Passage en mode super administrateur avec sudo su -
2. Installation de Docker Compose
Téléchargement de Docker Compose v1.28.6 depuis GitHub
Placement du binaire dans /usr/local/bin/
Attribution des permissions d'exécution
3. Résolution d'erreur
Correction de l'erreur libcrypt.so.1 manquante
Installation de libxcrypt-compat avec dnf
4. Installation de Docker Engine
Ajout du repository Docker officiel CentOS
Installation des packages : docker-ce, docker-ce-cli, containerd.io
Vérification de l'installation avec rpm -qa
5. Configuration et démarrage
Activation du service Docker au démarrage (systemctl enable)
Démarrage du service Docker (systemctl start)
Vérification du statut et des versions
6. Tests de validation
Vérification des versions Docker et Docker Compose
Test de fonctionnement avec docker ps
Ce document couvre une installation complète de Docker sur un système CentOS/RHEL avec résolution des problèmes de dépendances.