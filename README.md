# 🧠 TP Systèmes d’Exploitation – xv6-riscv (INF4097)

## 📌 Présentation

Ce dépôt contient le travail réalisé dans le cadre du **TP de Systèmes d’Exploitation (INF4097)** basé sur le noyau éducatif **xv6-riscv**.

L’objectif du TP est de comprendre **le fonctionnement interne d’un système d’exploitation** à travers des modifications concrètes du noyau :
- ajout d’un appel système
- surveillance de l’activité système
- modification du scheduler
- gestion avancée de la mémoire (lazy allocation)

---

## 🧩 Fonctionnalités implémentées

### 1️⃣ Appel système `getactivity()`
- Ajout d’un nouvel appel système permettant de récupérer :
  - l’état du système
  - l’activité CPU
  - l’utilisation mémoire
- Communication complète **user ↔ kernel**

📂 Fichiers modifiés :
- `kernel/sysproc.c`
- `kernel/syscall.c`
- `kernel/syscall.h`
- `kernel/usys.S`
- `kernel/defs.h`

---

### 2️⃣ Programme utilisateur `activitymon`
- Programme de surveillance exécuté en mode utilisateur
- Fonctionne comme un **démon** :
  - boucle infinie
  - affichage périodique (toutes les 5 secondes)
- Utilise l’appel système `getactivity()`

📂 Fichiers :
- `user/activitymon.c`
- `Makefile`

---

### 3️⃣ Ordonnancement Lottery Scheduler
- Remplacement du scheduler Round-Robin par un **Lottery Scheduler**
- Attribution de tickets aux processus
- Sélection probabiliste du processus à exécuter

📂 Fichier modifié :
- `kernel/proc.c`

🎯 Objectif :
- illustrer la notion de **priorité**
- comparer équité déterministe vs probabiliste

---

### 4️⃣ Lazy Allocation (allocation paresseuse)
- Désactivation de l’allocation immédiate dans `sbrk()`
- Allocation dynamique des pages mémoire au **premier accès**
- Gestion des page faults (load/store)

📂 Fichiers modifiés :
- `kernel/sysproc.c`
- `kernel/trap.c`

---

## 🧪 Tests réalisés

- Test de `sbrk()` sans accès mémoire
- Test d’accès mémoire déclenchant un page fault
- Test d’accès hors limites (protection mémoire)
- Test du scheduler avec processus CPU-bound
- Observation du comportement du démon `activitymon`

---

## ⚙️ Compilation et exécution

### Pré-requis
- Environnement xv6-riscv
- Toolchain RISC-V (`riscv64-unknown-elf-gcc`)

### Lancer xv6
```bash
make qemu
