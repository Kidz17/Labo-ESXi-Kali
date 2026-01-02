# Labo-ESXi-Kali
Déploiement d'un laboratoire de cybersécurité hybride combinant un hyperviseur VMware ESXi 8.0 et une machine d'attaque Kali Linux. Focus sur l'optimisation des ressources hardware (12 Go RAM) et le dépannage système (Troubleshooting PSOD).
 
# Projet : Infrastructure de Pentesting & Virtualisation (Home Lab)

##  Présentation
Déploiement d'un environnement de virtualisation local pour la pratique de la cybersécurité. Ce projet vise à simuler un réseau d'entreprise vulnérable et une machine attaquante dans un environnement cloisonné.

##  Stack Technique & Matériel
* **Hôte Physique :** AMD Ryzen 5 5600H / 12 Go RAM DDR4.
* **Hyperviseur :** VMware Workstation Pro / ESXi 8.0.
* **OS Attaquant :** Kali Linux 2024.x (Debian 12 Bookworm).

##  Architecture & Challenges Techniques

### Phase 1 : Test de l'Architecture Nested (ESXi)
J'ai tenté de déployer une infrastructure complexe avec un hyperviseur ESXi 8.0 virtualisé.
* **Problème rencontré :** Crash du système (PSOD - Purple Screen) lors du lancement des VMs imbriquées.
* **Analyse :** L'erreur `Admission check failed` a révélé que mes 12 Go de RAM étaient insuffisants pour supporter la "sur-allocation" mémoire demandée par l'ESXi 8.0.

### Phase 2 : Architecture Optimisée (Side-by-Side)
J'ai adapté l'architecture pour contourner cette limitation matérielle :
1.  **Attaquant (Kali Linux) :** Déployée directement dans VMware Workstation.
    * **Stockage :** Partitionnement assisté sur disque virtuel (`/dev/sda`).
    * **Réseau :** Configuration NAT pour l'accès internet et l'isolation partielle.
2.  **Cible :** Conservation du serveur ESXi éteint, disponible comme cible d'attaque future.

##  Compétences validées
* **Virtualisation :** Compréhension des limites hardware (RAM/CPU) et des types d'hyperviseurs.
* **Système Linux :** Installation graphique de Debian/Kali.
* **Résolution de problèmes :** Capacité à pivoter d'une solution technique à une autre face à une impasse matérielle.

 Pour ce projet, j'ai utilisé l'assistance d'une IA afin de m'aider à interpréter les logs d'erreurs critiques (PSOD) et explorer des architectures alternatives. Cela m'a permis de comprendre plus rapidement le concept d'over-provisioning mémoire et de pivoter vers une solution fonctionnelle.

##  Captures d'écran du projet

### 1. Diagnostic de l'erreur mémoire (PSOD)
Face à la limitation de 12 Go de RAM, l'hyperviseur ESXi a généré une erreur critique lors de l'allocation pour la VM imbriquée.

<img width="1014" height="788" alt="01_esxi_memory_panic" src="https://github.com/user-attachments/assets/edff9262-8048-44b3-af44-cb10dbfd0eb8" />


### 2. Optimisation via installation native
Migration vers une architecture plus légère avec partitionnement assisté sur le disque virtuel reconnu comme `/dev/sda`.

<img width="1918" height="1030" alt="image_7ef480" src="https://github.com/user-attachments/assets/af3eb424-6c80-4485-b308-cfac9ca8f7db" />


### 3. Finalisation du Bootloader
Installation réussie du chargeur de démarrage GRUB sur le secteur d'amorçage pour finaliser le laboratoire.

<img width="817" height="624" alt="image_88fc49" src="https://github.com/user-attachments/assets/348811a2-9636-4b96-be75-896a2ea2a3f1" />


### 4. Validation du système et connectivité
Le bureau Kali est opérationnel. Les tests `ping` et `ip a` confirment que la machine est correctement adressée sur le réseau (IP : `192.168.142.130`) avec 0% de perte de paquets.

<img width="1713" height="860" alt="image_8965c7" src="https://github.com/user-attachments/assets/eb771893-5659-42cd-a5f0-f56a6df897fe" />

