
# Système de surveillance d'un frigo industriel

Projet réalisé dans le cadre du cours **Conception et analyse de schémas** — ISIB, cours de M. Rodrigues.

## Objectif du projet

Concevoir une électronique de mesure et de surveillance destinée à être embarquée dans un frigo industriel, capable de détecter et signaler tout comportement anormal (porte oubliée, dérive de température, coupure de courant), depuis le schéma électronique jusqu'au circuit imprimé fini.

## Cahier des charges

| Exigence | Détail |
|---|---|
| Environnement | Boîtier étanche, tenue aux températures négatives |
| Mesure de température | Thermocouples, de préférence type T, connecteurs standards |
| Résolution | 1 °C ou mieux |
| Alerte à distance | En cas de comportement anormal (porte ouverte, baisse anormale de température, …) |
| Alerte locale | Alarme sonore/visuelle sur place |
| Communication | Ethernet |
| Consommation | Minimale |
| Alimentation | Protection contre les coupures de courant (secours sur batterie) |
| Indication | Témoins de fonctionnement (LEDs d'état) |

## Structure du projet

Le cours se déroule en deux volets complémentaires, correspondant aux deux dossiers du dépôt :

### 1. Schématique — `schematic/`
- Analyse du cahier des charges et découpage fonctionnel du système
- Choix et justification des composants (datasheets, calculs de dimensionnement)
- Câblage du schéma électronique complet
- Vérification des règles électriques (ERC)

### 2. Circuit imprimé — `pcb/`
- Placement des composants et contraintes mécaniques (boîtier, connecteurs)
- Routage des pistes (KiCad)
- Respect des règles de conception (largeur de piste, isolation, plan de masse)
- Génération des fichiers de fabrication (Gerbers, BOM, plan de perçage)

## Architecture électronique retenue

| Bloc | Composant | Rôle |
|---|---|---|
| Microcontrôleur | STM32L476 | Traitement, logique de surveillance |
| Mesure température (thermocouple) | MAX31855 + thermocouple type T | Mesure haute précision |
| Mesure température (secours/locale) | DS18B20 | Redondance de mesure |
| Communication | W5500 + MagJack RJ45 | Interface Ethernet |
| Alimentation secteur | HLK-PM01 (230 V → 5 V) | Alimentation principale isolée |
| Régulation | AMS1117-3.3 | Alimentation logique 3,3 V |
| Secours | Pile CR123A | Continuité de service en cas de coupure |

> La zone réseau 230 V est isolée de la basse tension par une barrière d'isolement, conformément aux règles de sécurité électrique.

## Outils utilisés

- **KiCad** — schématique et routage PCB
- **LaTeX** — rédaction du rapport de conception

## Organisation des fichiers

```
├── schematic/          # Fichiers de schéma KiCad, notes de choix de composants
├── pcb/                # Layout, règles de conception, fichiers de fabrication
├── datasheets/         # Documentation des composants clés
├── rapport/            # Rapport LaTeX du projet
└── README.md
```
