# DevSecOps 

Dit project bevat een DevSecOps-pipeline die gebruik maakt van Docker, Gitea, Prometheus, Grafana en een aantal andere tools. De pipeline is opgezet om de verschillende fasen van de ontwikkelingscyclus te automatiseren, inclusief versiebeheer, build, test, en deployment. Hieronder worden de belangrijkste onderdelen van het project beschreven.

## Overzicht

Het project maakt gebruik van twee virtuele machines (VM's):

1. **1e VM**: Bevat Docker, Gitea, Prometheus en Grafana (IP: 10.24.36.105)
2. **2e VM**: Bevat Docker, Gitea, Act_runner (Gitea runner) en Node Exporter

## Componenten

### 1. **Gitea-installatie geautomatiseerd met Ansible**
   - De installatie van Gitea wordt volledig geautomatiseerd met Ansible. Dit script zorgt ervoor dat Gitea automatisch wordt geïnstalleerd op de server waarop het playbook wordt uitgevoerd.

### 2. **Git versioning per release (Semantic Versioning)**
   - Git versiebeheer is ingesteld volgens het Semantic Versioning-concept, waarbij de versie automatisch wordt aangepast op basis van de pipeline.
   - Dit wordt gerealiseerd met de `standard-version` functionaliteit in de `package.json`.

### 3. **Monitoring van de infrastructuur**
   - Prometheus en Grafana zijn ingesteld voor het monitoren van de gehele infrastructuur.
   - Node Exporter wordt gebruikt op de runner VM om systeeminformatie naar de Prometheus-VM te sturen.

### 4. **Gebruik van Gitea Actions**
   - De pipeline maakt gebruik van Gitea Actions voor Continuous Integration en Continuous Deployment (CI/CD).

### 5. **Build, Test en Deploy**
   - Er zijn twee verschillende pipelines:
     - De *develop* pipeline: deze doorloopt de stappen *build*, *test*, *version* en *deploy*.
     - De *main* pipeline: deze doorloopt alleen *build*, *version* en *deploy*.
   - De teststap maakt gebruik van standaardtests van de Uptime Kuma clone, waaronder Playwright, MQTT en de testmap. Extra *skips* zijn toegevoegd aan Playwright en MQTT om fouten te vermijden door netwerkvertragingen tussen de Proxmox-servers.
