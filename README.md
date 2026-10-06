# maint-agent-releases

Versions publiées de **Maint Agent**, le plugin WordPress en lecture seule de l'outil de maintenance `tv/maintenance`.

Ce dépôt ne contient pas de code : les versions sont uniquement des **pièces jointes de releases**. Rien n'est lu depuis la branche.

## Contenu d'une release

Chaque release `vX.Y.Z` porte trois fichiers :

| Fichier | Rôle |
|---|---|
| `maint-agent-X.Y.Z.zip` | Le plugin |
| `latest.json` | Le manifeste : version, PHP minimum, empreinte SHA-256 du zip, signé par une clé de publication |
| `keys.json` | La liste des clés de publication valables, signée par la clé racine |

Les sites et l'outil lisent toujours la release marquée **Latest**, via :

```
https://github.com/TVanmeerhaeghe/maint-agent-releases/releases/latest/download/keys.json
https://github.com/TVanmeerhaeghe/maint-agent-releases/releases/latest/download/latest.json
```

## Vérification

Ce dépôt n'est **pas** de confiance : un fichier modifié ici est refusé. Avant toute installation, le plugin :

1. vérifie `keys.json` avec la clé publique racine inscrite dans son code, et refuse une version plus ancienne que la plus récente déjà vue (anti-retour) ;
2. vérifie que `latest.json` est signé par l'une des clés de `keys.json` ;
3. n'accepte qu'une version plus récente que celle installée ;
4. télécharge le zip et refuse toute empreinte différente de celle signée.

Au moindre échec, aucune mise à jour. Il n'y a pas de repli.

Les clés privées ne sont jamais dans ce dépôt : chiffrées par phrase de passe, elles sont conservées hors ligne.

## Publier une version

Depuis le dépôt de l'outil, clé USB branchée :

```sh
npm run agent:release -- <clé de publication> <keys.json>
```

Puis créer une release `vX.Y.Z`, y joindre les **trois** fichiers produits dans `dist/` et la marquer comme **Latest**.

Ne jamais supprimer ni modifier une release publiée : les sites en cours de mise à jour s'y réfèrent.
