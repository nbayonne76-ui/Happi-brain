---
name: happi-brain-website
description: H'appi Website — blog bilingue FR/EN (Next.js 15 + next-intl v4), articles React components (pas MDX), agrégateur RSS live 15 sources ISR 1h
metadata:
  type: project
---

# HAPPI BRAIN — H'APPI WEBSITE & BLOG

## INFOS PROJET
- **Repo** : `github.com/nbayonne76-ui/h-appi-website` (branch `main`)
- **Deploy** : h-appi-website.vercel.app
- **Type** : Site vitrine corporate + blog bilingue FR/EN + news live

## STACK
```
Next.js 15 App Router + TypeScript
Tailwind CSS + @tailwindcss/typography  ← prose classes pour article body
Framer Motion 11                        ← animations (hover, stagger, transitions)
next-intl 4                             ← i18n (fr + en, défaut fr)
Resend 6                                ← formulaire newsletter + contact
Lucide React                            ← icônes
```

---

## ARCHITECTURE BLOG

```
lib/blog-data.ts               → types + helpers (getArticles, getArticleBySlug…)
messages/fr.json               → métadonnées articles en français (blogData.articles)
messages/en.json               → métadonnées articles en anglais
app/[locale]/blog/page.tsx     → listing blog (client component — filtres + animations)
app/[locale]/blog/[slug]/page.tsx → détail article (server component, SSG)
components/blog/
  ArticleCard.tsx              → carte article (variant featured + standard)
  ArticleLayout.tsx            → layout article (header + prose + sidebar sticky)
  BlogCategoryNav.tsx          → navigation catégories
  BlogNewsletter.tsx           → bloc newsletter bas de page
  NewsSection.tsx              → agrégateur news live (client component)
  NewsCard.tsx                 → carte news individuelle
app/api/news/route.ts          → API route news (RSS aggregator, ISR 1h)
```

## MODÈLE DE DONNÉES (`lib/blog-data.ts`)

```typescript
export type Article = {
  slug: string;
  title: string;
  excerpt: string;
  category: string;         // 'Produit' | 'Guide' | 'Tendances' | 'Conformité' (FR)
  categoryColor: string;    // classe Tailwind pour le badge
  accentHex: string;        // couleur hex pour gradients + icônes
  date: string;
  readTime: string;
  author: string;
  authorRole: string;
  featured?: boolean;       // true sur l'article index 0
};
```

**Pattern clé** : données séparées du contenu
- Métadonnées → `messages/fr.json` et `messages/en.json` sous `blogData.articles`
- Slugs → tableau hardcodé dans `blog-data.ts`
- Corps de l'article → composants React inline dans `[slug]/page.tsx` (pas de CMS ni MDX)

```typescript
// blog-data.ts
const slugs = ['mon-slug-1', 'mon-slug-2', ...];  // 1:1 avec blogData.articles

export function getArticles(locale: string): Article[] {
  const data = (messages[locale] || messages.fr).blogData.articles;
  return data.map((item, index) => ({
    slug: slugs[index],
    ...item,
    categoryColor: categoryColors[item.category] || 'bg-gray-100 text-gray-700',
    accentHex: categoryAccent[item.category] || '#3B82F6',
    featured: index === 0,
  }));
}
```

**Mapping catégories → couleurs** :
| Catégorie (FR) | EN | Couleur | Hex |
|---|---|---|---|
| Produit | Product | happi-blue | `#3B82F6` |
| Guide | Guide | happi-green | `#10B981` |
| Tendances | Trends | purple-400 | `#c084fc` |
| Conformité | Compliance | red-400 | `#f87171` |

---

## PAGE LISTING BLOG

`'use client'` — requis pour l'état des filtres et les animations.

Sections :
1. Hero avec stats (nb articles, catégories, sources live, fréquence)
2. Navigation catégories avec compteurs
3. Article "À la une" (index 0, variant `featured`)
4. Tab bar : toutes les catégories + onglet "Actualités/News" spécial
5. Grille articles (2 cols sm / 3 cols lg) avec stagger Framer Motion
6. Section newsletter bas de page

**Onglet News** : affiche `<NewsSection />` — données live via `/api/news`.

---

## PAGE DÉTAIL ARTICLE

Server component (pas de `'use client'`).

```typescript
// SSG : génère toutes les combinaisons locale × slug
export async function generateStaticParams() {
  const locales = ['fr', 'en'];
  return locales.flatMap(locale => slugs.map(slug => ({ locale, slug })));
}

// Corps d'article : composants React inline
<ArticleLayout article={article} sources={[...]} toc={[...]}>
  {locale === 'fr' ? <Article1_FR /> : <Article1_EN />}
</ArticleLayout>
```

---

## AGRÉGATEUR NEWS LIVE (`app/api/news/route.ts`)

```typescript
export const revalidate = 3600;  // ISR : rebuild toutes les heures

// 15 sources RSS/API : Hacker News, Dev.to (ai, chatbot, webdev),
// InfoQ, The New Stack, CSS-Tricks, Smashing Mag, Medium (chatbot, AI),
// Reddit (ML, webdev, programming), TechCrunch, Product Hunt

// Filtres :
// 1. Langue : EN/FR seulement (bloque Cyrillic, Arabic, CJK)
// 2. Spam : regex casino/betting/seo/crypto...
// 3. Pertinence : keywords IA/chatbot/tech pour feeds non-tagués
// 4. Dedup : Set<url>
// 5. Sort newest first, cap 80 items

// Headers Vercel edge :
'Cache-Control': 'public, s-maxage=3600, stale-while-revalidate=7200'
```

**Important** : pas de bibliothèque rss-parser — parser XML custom (support CDATA, Atom, RSS2).

---

## i18n AVEC next-intl v4

```typescript
// i18n/config.ts
export const locales = ['fr', 'en'] as const;
export const defaultLocale: Locale = 'fr';
// URLs : /fr/blog, /en/blog
```

**Données article dans les JSON de traduction** :
```json
// messages/fr.json
{
  "blogData": {
    "articles": [
      {
        "title": "Mon article",
        "excerpt": "...",
        "category": "Produit",
        "date": "15 mai 2026",
        "readTime": "5 min",
        "author": "Nada Bayonne",
        "authorRole": "Fondatrice H'appi"
      }
    ]
  }
}
```

---

## COMMENT AJOUTER UN NOUVEL ARTICLE

1. Ajouter le slug dans le tableau `slugs` de `lib/blog-data.ts`
2. Ajouter les métadonnées dans `messages/fr.json` et `messages/en.json` → `blogData.articles` (même index)
3. Créer les composants `ArticleN_FR()` et `ArticleN_EN()` dans `app/[locale]/blog/[slug]/page.tsx`
4. Ajouter le cas dans le switch de rendu

**Règle** : les tableaux `slugs` et `blogData.articles` doivent toujours avoir la même longueur et le même ordre.

---

## LEÇONS APPRISES

- **Corps d'article en React components** (pas MDX) = moins de dépendances, meilleure performance, JSX avancé possible.
- **`@tailwindcss/typography`** : nécessite `prose-invert` ou overrides custom sur fond sombre (`prose-headings:text-white`).
- **`'use client'` sur la page listing** : obligatoire pour filtres + animations, mais le détail reste server component (SEO optimal).
- **ISR `revalidate = 3600`** sur la route API = news fraîches toutes les heures sans rebuild full.
- **Parser XML custom** : plus léger qu'`rss-parser`, supporte CDATA + Atom + RSS2.
- **Filtres langue sur RSS** : sans filtre, ~30% des items sont en cyrillique/arabe/turc.

---

*Mis à jour : 2026-05-31 — extrait de happi_brain.md v22 (Section 22)*
