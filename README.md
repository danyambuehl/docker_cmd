Docker 
====

# **Container erstellen**
  
  **Erstellen eines Docker Image mit -t option für "target string" zu gitlab registry in das akutelle Verzeichnis (.) am ende**
  
  > `$ docker build -t registry.gitlab.com/daniel.ambuehl/nginx .`

  **Zeigt alle laufenden docker images an**
  
  > `$ docker image ls` 

## Mit Gitlab Repostiory verbinden 

  **Einloggen in das gitlab repositroy**
  
  > `$ docker login registry.gitlab.com/daniel.ambuehl/nginx` 

  **Ladet aktuell erstelltes Image in mein gitlab repository**
  
  > `$ docker push registry.gitlab.com/daniel.ambuehl/nginx` 

## Container starten & managen

  **Startet den dockercontainer | --name = Servername  | -p = Port-forwarding | Image**

  > `$ docker container run -d --name container-webserver -p 8080:8080 registry.gitlab.com/daniel.ambuehl/nginx` 

  **Container stoppen with name or Container ID -> mit docker image ls herausfinden **
  
  > `$ docker container stop container-webserver `
  > `$ docker container stop 2ab14852033e `
  
 **zeige alle Container (auch die gestoppten) und filtere nach "container-webserver"**
  
  > `$ docker container ls -a | grep -i container-webserver` 
  
  **Container löschen with name or Container ID **
  
  > `$ docker container rm container-webserver `
  > `$ docker container rm 2ab14852033e `

## Container Image managen

 **zeige alle Docker Images an**
  
  > `$ docker image list ` 
  
 **Löscht das entsprechende Docker Images -f = Force**
  
  > `$ docker image rm a21c252409e8 -f ` 


# **Docker Compose konfigurieren**
  
  **Installieren des Docker Compose**
  
  > `$ sudo apt install docker-compose`

  **Version und installation kontrolieren**
  
  > `docker-compose version` 
  > `sudo apt list | grep -i docker-compose` 

  **Umgebung starten**
  
  > `$ docker-compose up -d `
  
 **Umgebung stoppen und entfernen**
  
  > `$ docker-compose down `

# Docker Swarm installieren
  
  **Initrieren des Docker Swarm**
  
  > `$ docker swarm init`

  **Docker Image von Repo herunterladen**
  
  > `docker pull registry.gitlab.com/daniel.ambuehl/nginx` 

  **Startet das Docker Image | -p = Portforwarding | --replicas = 3 Times this "Image Scalability"**
  
  > `$ docker service create --name web -p 8080:8080 --replicas 3 registry.gitlab.com/daniel.ambuehl/nginx`
  
## Docker Swarm verwalten

  **Skaliert den web server auf insgesamt 10 Container"**
  
  > `$ docker service scale web=10`
  
  **Überprüfen ob Service und Container laufen**
  
  > `$ docker service ps web `
  > `$ docker service ls | grep -i web `
  > `$ docker container ls | grep -i web`
  
  **Löscht den Service web und die Container**
  
  > `$ docker service rm web`
   
# Deklarativ Docker Stack erstellen

  **Erstellt ein neues Image auf Repository**
  
  > `$ docker image build -t registry.gitlab.com/daniel.ambuehl/nginx:1.0 .`

 **Push Image auf Gitlab**
  
  > `$ docker push registry.gitlab.com/daniel.ambuehl/nginx:1.0`

  **Startet den stack Named "zaehler" mit dem -c Compose File docker-compose.yml**
  
  > `$ docker stack deploy -c docker-compose.yml zaehler`


## Deklarativ Docker Stack verwalten und löschen

**Übersicht über die vorhandenen Dockerstacks**
  
  > `$ docker stack ls`

  **Zeigt die beiden Container an, wobei der "counter_web_fe" 10x repliziert ist**
  
  > `$ docker stack services zaehler	`

  **Zeigt die einzelnen Container**
  
  > `$ docker stack ps zaehler`

  **docker-compose.yml Ändern um die Anzahl Replicas zu verringern**
  
  > `$ vi docker-compose.yml`  

  **Um die Änderungen zu aktivieren, das abgeänderte yml-File nochmals deployen**
  
  > `$ docker stack deploy -c docker-compose.yml zaheler`  

  **Um die Änderungen zu aktivieren, das abgeänderte yml-File nochmals deployen**
  
  > `$ docker stack deploy -c docker-compose.yml zaheler`  

  **Löschen des stacks mit**
  
  > `$ docker stack rm zaehler` 

---

Quelle Befehlsüberischt : [Docker Befehle](https://docs.docker.com/engine/reference/commandline/image_ls/ "DOCKER")

---

> [⇧ **Zurück zur Hauptseite**](/README.md)

---
