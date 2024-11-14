# DevSecOps Pipeline

Dit project bevat een DevSecOps-pipeline die gebruik maakt van Docker, Gitea, Prometheus, Grafana en andere tools. De pipeline automatiseert het versiebeheer, build, test en deployment van de applicatie. Hieronder worden de belangrijkste onderdelen van het project beschreven.

## Overzicht

Er zijn twee VM's gebruikt in dit project:

1. **1e VM**: Bevat Docker, Gitea, Prometheus en Grafana (IP: 10.24.36.105).
2. **2e VM**: Bevat Docker, Gitea, Act_runner (Gitea runner) en Node Exporter.

## Onderdelen die zijn uitgevoerd

### 1. **Gitea-installatie geautomatiseerd met Ansible – Zeer goed**
   Door middel van een Ansible-script wordt Gitea automatisch geïnstalleerd op de server waarop het playbook wordt uitgevoerd.  
   (Zie de map 'ansible' en de bewijsfoto's in de 'screens' map.)

### 2. **Git versioning per release, bijvoorbeeld met version tags volgens semantic versioning – Zeer goed**
   Door gebruik te maken van de functionaliteit "release": "standard-version" in de `package.json` wordt de versie automatisch aangepast in de pipeline.  
   (Zie de pipelines en de bewijsfoto's in de 'screens' map.)

### 3. **Monitoring ingesteld voor de gehele infrastructuur – Goed**
   Voor de monitoring van de gehele infrastructuur is gebruik gemaakt van Prometheus en Grafana. Daarnaast heeft de runner (op een aparte VM) een Node Exporter om gegevens van de aparte VM naar de Prometheus-VM te sturen.  
   (Zie de bewijsfoto's in de 'screens' map.)

### 4. **Gebruik van Gitea Actions – Voldoende**
   Tijdens deze assessment is ervoor gekozen om Gitea Actions te gebruiken.  
   (Zie de pipelines.)

### 5. **Correct gebruik van build, test en deploy stappen – Zeer goed**
   Er zijn twee verschillende pipelines gemaakt:
   - De pipeline voor de *develop* branch doorloopt de stappen *build*, *test*, *version* en *deploy*.
   - De pipeline voor de *main* branch doorloopt alleen de stappen *build*, *version* en *deploy*.

   In de teststap wordt gebruik gemaakt van de standaard tests van de Uptime Kuma clone, waaronder Playwright, MQTT en de testmap. Bij Playwright en MQTT heb ik extra *skips* toegevoegd, omdat er regelmatig fouten optreden door de langzame verbinding tussen de Proxmox-servers, wat invloed heeft op de communicatie tussen beide VM's.  
   (Zie de pipelines.)

### 6. **Applicatie in een container – Goed**
   De Uptime Kuma applicatie draait in een Docker-container.  
   (Zie de pipelines.)

## Filmpje
https://youtu.be/JFueaMu8oOE
