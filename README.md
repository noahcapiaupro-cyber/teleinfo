# Explication simple du script Python

Ce programme Python se connecte à un serveur `teleinfo` pour récupérer le numéro de série d’un compteur électrique.

---



# Fonctionnement du programme

## 1. Connexion au serveur

Le programme se connecte à l’adresse :

```text
192.168.1.241:2300
```

grâce à une socket TCP.

---

## 2. Lecture des données

Le serveur envoie des trames `teleinfo`.

Le programme les récupère avec :

```python
s.recv(1024)
```

---

## 3. Recherche de `ADCO`

Le script cherche la ligne contenant :

```text
ADCO
```

Cette ligne contient le numéro de série du compteur.

---

## 4. Extraction du numéro

Le numéro est extrait puis affiché :

```python
print(f"Numéro de série : {numeroSerie}")
```

---

# Exemple

Trame reçue :

```text
ADCO 123456789012 X
```

Résultat affiché :

```text
Numéro de série : 123456789012
```

---
```mermaid
graph TD
    A[Compteur EDF] -->|Téléinfo| B(Démodulateur)
    B -->|RS 232| C{Passerelle}
    C -->|Réseau local| D[PC de supervision]
```

```mermaid
graph TD
    A[Box Internet] --- B{Switch}
    B --- C[PC Prof]
    B --- D[Serveur Web]
    B --- E[Postes Étudiants]
```


##### 2. Diagrammes horizontaux
```mermaid
graph LR
    A[Capteur Temp] --> B(ESP32)
    B --> C{Seuil > 25°C}
    C -->|Oui| D[Ventilateur ON]
    C -->|Non| E[Veille]
```

##### 3. Diagrammes de séquence
```mermaid
sequenceDiagram
    Client CIEL->>Serveur: GET /api/data
    Note right of Serveur: Traitement Python
    Serveur-->>Client CIEL: 200 OK (JSON)
```


##### 4. Diagrammes d'état
```mermaid
stateDiagram-v2
    [*] --> Repos
    Repos --> Mesure : Interrupt Timer
    Mesure --> Envoi_Data : Conversion OK
    Envoi_Data --> Repos : Success
    Envoi_Data --> Erreur : Timeout
    Erreur --> Repos : Reset
```
