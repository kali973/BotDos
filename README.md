## Apache2 Service for Kali Linux

Only for Kali Linux
```
  Ce script a été développé pour un projet académique et il ne doit pas être utilisé en dehors de ce cadre. 
```
```
Prérequis pour Attaque ICMP Flood et Slowloris. 
```
-	Wireshark (pour l’analyse du trafic) 
-	Xterm (Pour affichage des commandes dans une fenêtre externe à la console principale) 
```
1.	Installation du script 

        Comment utiliser le projet depuis Github : https://github.com/kali973/BotDos.git 

-	Faire le clone du folder BotDdos en utilisant votre IDE ou bien  
-	Exécuter les commandes suivant depuis votre terminale.

2.	Lancement du script 

        Le fichier ddosattack.py est celui qui lance tout le programme. 
        Voici la commande python qui nous permet de lancer notre script. 

```
git clone https://github.com/kali973/BotDos.git

cd botDos

python ddosattack.py

![img99.png](image%2Fimg99.png)

Les Options [5], [6], [7] et [8] sont les options principales de ce bot pour faire du Ping Flood (ICMP Flooding) ou du slowloris . 
```
     •	Option 5 :
      
     [5] :   Cette option nous montre l’adresse IP de la machine qui l’utilise pour ainsi connaitre le reseau dans lequel on se trouve : elle correspond à la commande ifconfig du terminal.    
             En lançant l’option 5 on exécute le programme ifConfigpython.py ( Voir code en Annexe ) . 

    •	Option 6 : 

     [6] :  Dans cette option , un scan de réseau est fait à l’ aide de la librairie python-nmap pour voir les machines hôtes connectés, la liste des ports et leur statuts. 
            Cette options permet à l’attaquant de choisir sa machine cible.  Le programme exécuter dans cette option est notre programme nmap.py  
            Ce programme utilise la bibliothèque "nmap" pour numériser une plage d'adresses IP et une plage de ports spécifiées par l'utilisateur. Le programme initialise un scanner de ports avec nmap, puis scanne la plage d'adresses IP spécifiée pour la plage de ports spécifiée. Enfin, le programme imprime les résultats de la numérisation, y compris l'état de chaque port trouvé pour chaque adresse IP.

    •	Option [7]

     [7] :  Une fois que la machine cible choisi, avec cette option 7 on lance l’attaque ICMP Flooding en se basant sur scapy. L’option 7 exécute donc le programme icmpflooding.py 

    •	Option [8]

     [8] :  Cette option permet à l’attaquant de lancer l’attack slowloris en exécutant le programme slowloris.py . 

     Autres Options.

    •	Teste en local de l’attaque Slowloris :
  
        Pour tester son propre serveur apache2 en local on peut utiliser les Options 1, 2, 3 et 4 avant de faire l’attaque slowloris pour tester. 

           [1] : Cette Option démarre le serveur apache sur la machine local en exécutant la commande  suivante : 
           [2] : Cette Option permet d’arrêter le serveur apache2 sur la machine local en exécutant la commande : 
           [3] : Celle-ci permet de redémarrer le server apache 2 sur la machine local  avec la commande : 
           [4] : Cette option affiche le localhost via Mozilla pour pouvoir la page d’accueil du serveur Apache2 sur la machine locale. 

           Une fois que ce Serveur est lancé, l’utilisateur peut choisir L’option 8 pour lancer l’attaque Slowloris sur son propre Serveur Apache2 et essayer de rafraichir la page pour constater l’inactivité du serveur et donc l’impact de l’attaque sur son localhost ou 127.0.0.1/

           Utilisation des outils de Detection 
           
           Pre requis : 
           
           [A] :  L’option A permet de lancer les outils de detection d’attaque Dos comme grafana, le plugin Apache explorer et prométheus.  Ces outils sont décrits dans la partie méthode de detection qui suit. 
           [A] :  Cette option installe de façons successive les différentes briques permettant d’analyser le bon fonctionnement d’un serveur . 
           
           Il s’agit de :   Grafana entreprise, Prometheus, Alerte manager, influx DB et apache exporter.  

           ## Quelle est la différence entre une attaque DDoS Slowloris et une attaque DDoS d'application traditionnelle ?
```
```
 Les attaques DDoS d'application traditionnelles sont conçues pour faire tomber un serveur en l'inondant d'un nombre écrasant de requêtes HTTP,
 ce qui nécessite des ressources substantielles de la part du pirate.
 
 En revanche, une attaque Slowloris peut ne nécessiter que quelques centaines de requêtes à intervalles longs, faibles et réguliers, plutôt que 
 des dizaines de milliers de requêtes HTTP en continu. La bande passante n'est pas une mesure clé dans la détection de ce type d'attaque DDoS.
 
 Les équipes de sécurité doivent plutôt évaluer le nombre standard de tentatives de connexion, les connexions ouvertes, les pools de connexion, les requêtes HTTP entrantes,
 les requêtes HTTP partielles, le nombre maximal de connexions autorisées par adresse IP source, les équilibreurs de charge gérant les tables de session,
 l'infrastructure de journalisation des serveurs Web et les autres chemins réseau ou système dans la DMZ.
```

## Comment se déroule une attaque Slowloris ?

```
 Une attaque Slowloris se déroule en quatre étapes :
 
    - Le pirate transmet des instructions de commande et de contrôle à son botnet ou à ses proxys inverses, qui envoient de multiples requêtes HTTP, incluent des en-têtes aléatoires et utilisent d'autres techniques de contournement, tout en ouvrant de nombreuses connexions à un serveur ciblé depuis leurs réseaux mondiaux.
    - Le serveur ciblé ouvre une connexion TCP pour chaque demande, en prévoyant de fermer le thread dès que la demande HTTP est terminée. Le serveur interrompt toute connexion excessivement longue afin de libérer le thread pour les demandes suivantes.
    - Pour empêcher la fermeture des threads, le pirate envoie par intermittence des en-têtes de requête partiels ou des requêtes HTTP supplémentaires pour maintenir le serveur Web ciblé en activité et le convaincre d'attendre que la requête HTTP soit terminée.
    - En attendant que d'autres requêtes HTTP et connexions TCP soient lancées, le serveur cible finit par manquer de connexions disponibles et ne plus pouvoir répondre aux requêtes du trafic légitime, ce qui entraîne un déni de service.
```

Before Ddos Attack

![img_1.png](image/img_1.png)

Attack Ddos SlowLoris

![img_2.png](image/img_2.png)

After Ddos Attack the server Apache is out,
we can see any metric on dashboard during the attack Ddos (red line)

![img_3.png](image/img_3.png)

## DDoS protection

```
DDoS Protect is an open source denial of service mitigation tool that uses industry standard sFlow telemetry from routers
to detect attacks and automatically deploy BGP remotely triggered blackhole (RTBH) and BGP Flowspec filters 
to block attacks within seconds
```

![img.png](image/ddosProtectSflow.png)

```
DDoS Protect is a lightweight solution that uses standard telemetry and control (sFlow and BGP) capabilities 
of routers to automatically block disruptive volumetric denial of service attacks.

You can quickly evaluate the technology on your laptop or in a test lab. 
The solution leverages standard features of modern routing hardware to scale easily to large high traffic networks.
```

## Getting Started

```
Try out sFlow-RT's real-time analytics by following the steps in this guide.
```

# Step 1: Install sFlow-RT

```
Follow the download and installation instructions for your platform.
```

# Step 2: Install applications

```
Start off by installing the browse-metrics and browse-flows applications:
```

```
sudo /usr/local/sflow-rt/get-app.sh sflow-rt browse-metrics
sudo /usr/local/sflow-rt/get-app.sh sflow-rt browse-flows
```

# Restart sFlow-RT to load the applications:

```
sudo systemctl restart sflow-rt
```

# Step 3: Access user interface

```
The user interface can be accessed using a web browser. Connect to HTTP port 8008 on the host running sFlow-RT, 
for example http://localhost:8008 if you are running the software on your laptop/desktop.
![img.png](img.png)
The sFlow-RT Status page shows key metrics about the health and performance of sFlow-RT.
```

# Step 4: Configure / deploy agents

```
Agents describes how to configure sFlow in existing network devices and/or deploy agents to monitor hosts, 
hypervisors, containers, Swarm and Kubernetes clusters. Use the sFlow-RT Status page to verify that sFlow 
telemetry is being received.

If you don't have immediate access to a network, Real-time network and system metrics as a service describes
how to replay captured sFlow data to explore the capabilities of the software on your laptop. Alternatively, 
sflow-rt/containerlab includes projects that emulate leaf and spine networks, EVPN, and DDoS mitigation, 
that can be run on a laptop using Docker Desktop.
```

# Step 5: Explore data

```
Access the sFlow-RT user interface.
```

![img.png](image/interfaceApp.png)# botdos

# botdos

# botdos
# botdos
# BotDos
