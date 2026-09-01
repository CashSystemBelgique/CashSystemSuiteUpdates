# CashSystem Suite — mises à jour

Ce dépôt ne contient **aucun code source**. Il sert uniquement à livrer le
programme compilé aux caisses des clients.

| Fichier | Rôle |
|---|---|
| `version.json` | La fiche que chaque caisse vient lire : dernière version, où la télécharger, et son empreinte SHA-256. |
| Releases | Le `CashSystem-Suite-Setup.exe` de chaque version. |

## Comment une caisse se met à jour

Sur le poste serveur, l'icône CashSystem près de l'horloge propose
**« Mettre à jour la Suite »**. Elle lit `version.json`, compare avec la version
installée, télécharge l'installeur, **vérifie son empreinte**, sauvegarde la
base de données, installe, puis vérifie que la caisse répond vraiment. En cas
d'échec, la version précédente est redémarrée.

## Pour publier une version (côté développement)

1. Incrémenter `<Version>` dans `CashSystem.Cloud.csproj`
2. `powershell -ExecutionPolicy Bypass -File deploy\release.ps1`
3. Créer la release et y attacher le `Setup.exe` — **d'abord**
4. Remplacer `version.json` — **ensuite**

⚠️ Cet ordre n'est pas négociable : l'inverse annonce aux caisses une version
qui n'existe pas encore, et chacune tombe en erreur de téléchargement.
