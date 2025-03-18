# R4.Crea.09_24

# Astro JS : BLOG

## 1 - Installation

- Créer un répertoire pour votre projet Astro, l'ouvrir dans VSCode et ouvrir le Terminal.

- Créez un nouveau projet Astro en utilisant la commande suivante :

```bash
  # create a new project with npm
  npm create astro@latest
```

- Confirmer `y` pour installer `create-astro`

- Créer le template `Blog`

- Lorsque l'invite vous demande où créer le projet, saisissez le nom d'un dossier pour créer un nouveau répertoire pour votre projet, par exemple `./td_Astro` ou `.` pour créer le projet dans le répertoire actuel.

- Lorsque l'invite vous demande si vous souhaitez ou non installer des dépendances, saisissez ou sélectionnez `y`.

- Lorsque l'invite vous demande si vous souhaitez ou non initialiser un nouveau référentiel git, saisissez ou sélectionnez `y`.

## 2 - Prettier :

```bash
  npm install --save-dev prettier prettier-plugin-astro
```

Ajouter un fichier`.prettierrc`:

```json
{
  "plugins": ["prettier-plugin-astro"],
  "overrides": [
    {
      "files": "*.astro",
      "options": {
        "parser": "astro"
      }
    }
  ]
}
```

## 3 - TailwindCSS

```bash
  npx astro add tailwind
```

- Effacer le fichier `src/styles/global.css`
  et ajouter

```css
@import "tailwindcss";
```

- Prettier pour TailwindCSS:

```bash
  npm install --save-dev prettier-plugin-tailwindcss
```

Modifier le fichier `.prettierrc`

```json
{
  "plugins": ["prettier-plugin-astro", "prettier-plugin-tailwindcss"],
  "overrides": [
    {
      "files": "*.astro",
      "options": {
        "parser": "astro"
      }
    }
  ]
}
```

## 4 - Créer un layout

- Créer un fichier `BaicLayout.astro` dans le dossier `src/layouts`:

## 5 - Ajouter des data

- Dans le répertoire `content` créer un dossier `data` et y ajouter le fichier `pizzas.json`.

- Ajouter une page `pizza.astro` dans le dossier `src/pages`:

```astro
---
---
import BasicLayout from "../layouts/BasicLayout.astro";
import pizzas from "../content/data/pizzas.json";
---

<BasicLayout>
  <h1 class="text-4xl font-bold text-center">Pizza</h1>
  <div class="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-3">
    {
      pizzas.map((pizza) => (
        <div class="bg-gray-100 p-4 rounded-lg shadow-lg">
          <h2 class="text-xl font-bold">{pizza.pizzaName}</h2>
        </div>
      ))
    }
  </div>
</BasicLayout>

```

- Allez sur la page `http://localhost:4321/pizza` pour voir le résultat.

- Trouver le moyen d'ajouter les ingrédiants des pizzas à votre page.

## 6 - Content collection

- Ouvrir le fichier `content.config.js` et ajouter:

```js
import { file, glob } from 'astro/loaders';
...

const pizzas = defineCollection({
  loader: file("src/content/data/pizzas.json"),
  schema: z.object({
    id: z.number(),
    pizzaName: z.string(),
    ingredients: z.array(z.string()),
  }),
});

export const collections = { blog, pizzas };

```

- Modifier le fichier `pizza.astro`:

```astro
---
import BasicLayout from "../layouts/BasicLayout.astro";
import { getCollection } from "astro:content";

const pizzas = await getCollection("pizzas");
---

<BasicLayout>
  <h1 class="text-4xl font-bold text-center">Pizza</h1>
  <div class="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-3">
    {
      console.log(pizzas)
    }
  </div>
</BasicLayout>

```

- Regarder la console pour voir le résultat.

- Modifier le code pour afficher les pizzas et les ingrédients.
