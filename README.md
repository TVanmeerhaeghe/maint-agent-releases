# maint-agent-releases

Versions publiées de **Maint Agent**, le plugin WordPress de l'outil de maintenance `tv/maintenance`.

Le plugin est **en lecture seule** : il transmet à l'outil l'inventaire du site (versions de WordPress, de PHP, des extensions et des thèmes, mises à jour disponibles). Il ne modifie rien, n'a pas d'interface d'administration et n'a aucune dépendance.

Ce dépôt ne contient pas de code. Les versions sont publiées uniquement en **pièces jointes des releases**.

## Installation et mises à jour

- **Installation** : le plugin est fourni préconfiguré par l'outil de maintenance qui suit le site. Le zip publié ici ne contient pas cette configuration : seul, il ne peut communiquer avec aucun outil.
- **Mises à jour** : elles apparaissent dans **Extensions** de WordPress, comme pour toute extension. Elles sont manuelles par défaut, et l'administrateur du site peut activer les mises à jour automatiques.
- **Prérequis** : WordPress 5.8 et PHP 7.4 au minimum.

## Contenu d'une release

| Fichier | Rôle |
|---|---|
| `maint-agent-X.Y.Z.zip` | Le plugin |
| `latest.json` | Le manifeste : version, PHP minimum et empreinte SHA-256 du zip, signés par une clé de publication |
| `keys.json` | La liste des clés de publication valables, signée par la clé racine |

## Sécurité des mises à jour

Ce dépôt n'est pas considéré comme sûr : seules les signatures font foi. Avant d'installer une mise à jour, le plugin :

1. vérifie `keys.json` avec la clé publique racine inscrite dans son code, et refuse une liste plus ancienne que la plus récente déjà vue ;
2. vérifie que `latest.json` est signé par l'une des clés de `keys.json` ;
3. n'accepte qu'une version plus récente que celle installée ;
4. refuse tout zip dont l'empreinte diffère de celle signée.

Au moindre échec, la mise à jour n'est pas installée. Les signatures utilisent Ed25519, et les clés privées ne sont jamais en ligne.

Clé publique racine :

```
tbJpwmRQ/zLKpDwrkkZKmtYhmQRQuOdpxXMeWZWjDCc=
```
