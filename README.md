# Bibliothèque de liseuse

Une application web en un seul fichier HTML (`bibliotheque.html`) : une étagère de
bibliothèque personnelle vue de face, avec livre ouvert animé en 3D, édition en place,
rangement par glisser-déposer, recherche, ajout de livres via Open Library, gestion des
couvertures (automatique, image locale ou adresse collée) et persistance locale.

Aucune dépendance, aucun build : le fichier s'ouvre directement dans un navigateur.

## Capture d'écran

![Capture d'écran de l'étagère](docs/capture.png)

*Le fichier `docs/capture.png` est un espace réservé vide — remplace-le par une vraie
capture d'écran de l'application une fois ouverte dans un navigateur.*

## Ouvrir l'application

Deux façons d'ouvrir `bibliotheque.html` :

- **Double-clic** sur le fichier. Tout fonctionne, à l'exception de la recherche en
  ligne (voir ci-dessous).
- **Via un serveur local**, pour profiter aussi de la recherche Open Library :

  ```bash
  python3 -m http.server 8000
  ```

  puis ouvrir `http://localhost:8000/bibliotheque.html`.

## Pourquoi certains appels réseau sont bloqués

Ouverte directement depuis un fichier (`file://`), la page ne peut pas contacter
Open Library : les navigateurs bloquent ce type d'appel pour les pages locales, et
l'application affiche un message expliquant pourquoi plutôt que de rester bloquée en
silence. Le reste — étagère, édition en place, rangement, couvertures locales ou
collées, export et import — fonctionne entièrement sans réseau, avec ou sans serveur.

## Format d'export

Le bouton **Exporter** télécharge un fichier daté `bibliotheque-AAAA-MM-JJ.json` :

```json
{
  "version": 1,
  "exporteLe": "2026-09-22T20:03:38.223Z",
  "livres": [
    {
      "id": "livre-01",
      "titre": "Le Nom du vent",
      "auteur": "Patrick Rothfuss",
      "annee": 2007,
      "serie": "Chronique du tueur de roi, livre 1",
      "statut": "à lire",
      "telecharge": true,
      "rayon": "Fantasy",
      "themes": ["magie", "musique", "apprentissage"],
      "resume": "…",
      "couverture": "https://covers.openlibrary.org/b/id/11480483-M.jpg",
      "couvCherchee": true,
      "note": "",
      "couleur": "#1f4d3a",
      "ordre": 0
    }
  ]
}
```

Le bouton **Importer** relit ce même format et propose, au choix, de remplacer la
bibliothèque actuelle ou d'ajouter les livres importés à la suite.

## Licence

MIT — voir [LICENSE](LICENSE).
