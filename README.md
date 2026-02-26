<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/8/8d/42_Logo.svg" alt="42 logo" width="120"/>
  <h1>push_swap</h1>
  <p>Projet 42 : trier une pile d'entiers avec un nombre minimal d'opérations sur deux stacks</p>

  <p>
    <img src="https://img.shields.io/badge/Language-C-00599C?logo=c&logoColor=white" alt="C"/>
    <img src="https://img.shields.io/badge/Build-Makefile-427819?logo=gnu&logoColor=white" alt="Makefile"/>
    <img src="https://img.shields.io/badge/School-42-black?logo=42&logoColor=white" alt="42"/>
    <img src="https://img.shields.io/badge/Norminette-friendly-success" alt="Norminette"/>
  </p>
</div>

---

## 📚 Description

`push_swap` est un programme qui reçoit une liste d'entiers en arguments et affiche sur la sortie standard une suite d'instructions (`sa`, `pb`, `ra`, etc.) permettant de trier la pile `a` en ordre croissant.

Le tri est réalisé uniquement avec les opérations autorisées du sujet 42, en manipulant deux piles chaînées :

- `a` : pile principale (entrée)
- `b` : pile auxiliaire

---

## 🗂️ Structure

- `includes/push_swap.h` : structures (`t_lst`) et prototypes
- `sources/push_swap.c` : point d'entrée et dispatch selon la taille
- `sources/parsing/` : validation d'arguments, conversion, détection de doublons, indexing
- `sources/operations/` : opérations autorisées (`sa`, `pb`, `ra`, `rra`, ...)
- `sources/sort/` : algorithmes de tri (petites tailles + grand volume)
- `sources/utils/` : utilitaires (liste chaînée, split, conversions)
- `python_visualizer.py` : visualiseur Tkinter pour rejouer les opérations
- `checker_Mac` : binaire checker fourni pour valider les coups

---

## ⚙️ Compilation

### Construire `push_swap`

```bash
make
```

Génère : `push_swap`

### Nettoyer

```bash
make clean
make fclean
make re
```

---

## 🚀 Utilisation

### Exemples de lancement

```bash
./push_swap 2 1 3
./push_swap "3 2 1"
./push_swap 9 3 5 1 8 4 7 2 6
```

---

## ✅ Vérification avec checker

Pour vérifier que la sortie trie bien la pile :

```bash
ARG="4 67 3 87 23"
./push_swap $ARG | ./checker_Mac $ARG
```

Résultat attendu : `OK`.

Pour compter les opérations générées :

```bash
ARG="$(seq 1 100 | shuf | tr '\n' ' ')"
./push_swap $ARG | wc -l
```

---

## 🧠 Stratégie de tri

### Petites tailles

- `2` éléments : échange simple (`sa`) si nécessaire
- `3` éléments : cas optimisés (`sa`, `ra`, `rra`)
- `4` et `5` éléments : extraction des plus petits vers `b`, tri de `a`, puis `pa`

### Grandes tailles

Le programme assigne d'abord un index trié à chaque valeur, puis applique un **radix sort binaire** sur ces index :

- bit à `0` → `pb`
- bit à `1` → `ra`
- en fin de passe → rapatriement de `b` vers `a` avec `pa`

---

## 🔎 Parsing & erreurs

- Accepte des arguments séparés ou une chaîne unique entre guillemets
- Refuse : valeurs non numériques, hors `INT_MIN` / `INT_MAX`, doublons, argument vide
- En cas d'erreur : sortie sur `stderr` avec `ERROR`

---

## 🎨 Visualisation (optionnel)

Le script `python_visualizer.py` permet de visualiser les opérations produites :

```bash
python3 python_visualizer.py 5 2 8 1 4 3
```

Prérequis : Python 3 + Tkinter.

---

## ✅ Norme & qualité

- Code C compilé avec : `-Wall -Wextra -Werror`
- Organisation respectant les exigences du cursus 42

---

## 👤 Auteur

- `biaroun` — 42

---

## 📄 Licence

Projet académique 42.
Usage pédagogique et personnel.
