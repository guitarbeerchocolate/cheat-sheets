# Next.js 14 Cheat Sheet

Almost all titles have links to the oficial NextJS documentation!

## Summary

- [ ] [01 - Creating a new project](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#creating-a-new-project)
  - [ ] [1.1 - CLI to create](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#cli-to-create)
  - [ ] [1.2 - Going to folder](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#going-to-folder)
  - [ ] [1.3 - Installing modules](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#installing-modules)
  - [ ] [1.4 - Running dev. server](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#running-dev-server)
- [ ] [02 - NextJS folders Structure](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#nextjs-folders-structure)
- [ ] [03 - NextJS CSS](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#nextjs-css)
- [ ] [04 - Image optimization](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#image-optimization)
- [ ] [05 - Routing & Layout](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#routing--layout)
- [ ] [06 - Link component and navigation optimization](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#link-component-and-navigation-optimization)
- [ ] [07 - Server Components to fetch data](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#server-components-to-fetch-data)
- [ ] [08 - Requests optimization](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#requests-optimization)
- [ ] [09 - Rendering Static vs Dynamic](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#rendering-static-vs-dynamic)
  - [ ] [09.1 - Static Rendering](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#static-rendering)
  - [ ] [09.2 - Dynamic Rendering](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#dynamic-rendering)
- [ ] [10 - Loading.tsx & Skeletons Loading](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#loadingtsx--skeletons-loading)
- [ ] [11 - Searching](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#searching)
- [ ] [12 - Mutating Data - "CRUD"](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#mutating-data---crud)
- [ ] [13 - revalidatePath Fresh Data fetching](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#revalidatepath-fresh-data-fetching)
- [ ] [14 - Errors and NotFound](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#errors-and-notfound)
- [ ] [15 - Metadata and SEO](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#metadata-and-seo)
- [ ] [16 - Checklist to optimize pages](https://gist.github.com/lucasKoyama/7545e28e857a8045976ab9988d0b0353#checklist-to-optimize-pages)

### [Creating a new project](https://nextjs.org/learn/dashboard-app/getting-started#creating-a-new-project)

#### CLI to create

`npx create-next-app@latest --typescript`

#### Going to folder

`cd <project-name>`

#### Installing modules

`npm install`

#### Running dev. server

`npm run dev`

### NextJS folders Structure

- `/app:` Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.
- `/app/lib:` Contains functions used in your application, such as reusable utility functions and data fetching functions.
- `/app/ui:` Contains all the UI components for your application, such as cards, tables, and forms. To save time, we've pre-styled these components for you.
- [`/app/ui/fonts.ts`](https://nextjs.org/learn/dashboard-app/optimizing-fonts-images) is where you should keep external fonts, by doing that, Next will download them previously to reduce fetching.
- `/public:` Contains all the static assets for your application, such as images.
- `/scripts:` Contains a seeding script that you'll use to populate your database in a later chapter.
  Config Files: You'll also notice config files such as next.config.js at the root of your application. Most of these files are created and pre-configured when you start a new project using create-next-app. You will not need to modify them in this course.

### [NextJS CSS](https://nextjs.org/learn/dashboard-app/css-styling)

`global.css` at root `layout.tsx`
`home.module.css` [module CSS](https://nextjs.org/learn/dashboard-app/css-styling#css-modules) allow you to scope CSS to a component by automatically creating unique class names, so you don't have to worry about style collisions as well.

### [Image optimization](https://nextjs.org/learn/dashboard-app/optimizing-fonts-images#the-image-component)

Use the `<Image/>` component with the width and height equal to the aspect ratio of the image

### [Routing & Layout](https://nextjs.org/learn/dashboard-app/creating-layouts-and-pages#nested-routing)

![image](https://gist.github.com/assets/121680414/e5a2725b-e1c9-4cc9-abcb-12f453ef9bfd)
![image](https://gist.github.com/assets/121680414/96caf904-3852-4e76-ad36-e18722067c8e)

<p>Each `folder` is a route, inside the folder you need a `page.tsx` which will be the "`index.html`", the `layout.tsx` will be some standard layouts for the page.</p>

### [Link component and navigation optimization](https://nextjs.org/learn/dashboard-app/navigating-between-pages#the-link-component)

`<Link />` component works just like the tag `<a>`, but with the difference that it prefetches other pages, resulting in a faster navigation between pages due to the background preload

### [Server Components to fetch data](https://nextjs.org/learn/dashboard-app/fetching-data#using-server-components-to-fetch-data)

Use `async` in the function `Page()` and then use an await to fetch some data directly with SQL queries or ORM.

### [Requests optimization](https://nextjs.org/learn/dashboard-app/fetching-data#what-are-request-waterfalls)

![image](https://gist.github.com/assets/121680414/5c5fc509-9a5d-472b-afd1-bf7158c8cc5f)
Use `Promise.all([Promise1, Promise2, Promise3])` for parallel data fetching

### Rendering Static vs Dynamic

#### [Static Rendering](https://nextjs.org/learn/dashboard-app/static-and-dynamic-rendering#what-is-static-rendering)

- **What is?** Fetches data > render the page > cache it to deliver later on requests > Content Delivery Network (CDN) > clients
- **When should be used?** When using UI with no data or data that is shared across users
- **Pros:** Faster Websites, Reduced Server Load, SEO.

#### [Dynamic Rendering](https://nextjs.org/learn/dashboard-app/static-and-dynamic-rendering#what-is-dynamic-rendering)

- **What is?** Content is rendered on the server for each user at request time (when the user visits the page)
- **Pros:** Real-Time Data, User-Specific Content (personalized content based on user interactions), Request Time Information.
  With dynamic rendering, your application is only as fast as your slowest data fetch.

#### [Making Dinamic](https://nextjs.org/learn/dashboard-app/static-and-dynamic-rendering#making-the-dashboard-dynamic)

`import { unstable_noStore as noStore } from 'next/cache';`
Use the `noStore()` inside the **server components** or inside the **async functions**

### [Loading.tsx & Skeletons Loading](https://nextjs.org/learn/dashboard-app/streaming#streaming-a-whole-page-with-loadingtsx)

- `loading.tsx` is a special Next.js file, it s**how as a replacement while page content loads**.
- Inside it can be rendered static content like "loading skeletons"
- To avoid the `loading.tsx` rendering in other sub-routes, move the `page.tsx` and `loading.tsx` to a folder with `(` `)`
  ![image](https://gist.github.com/assets/121680414/0851e209-77ff-4732-8362-028da966feff)
  ![image](https://gist.github.com/assets/121680414/772f9c43-096c-4b1c-ad9b-08028640ce52)
  Contents like `CardWrapper`, `RevenueChart` and `LatestInvoices` are the components with data being fetched, while the data is streaming the `Suspense` loads the `skeletons` which are just the prototype structures of the UI

### [Searching](https://nextjs.org/learn/dashboard-app/adding-search-and-pagination#why-use-url-search-params)

1. Capture the user's input. With `handleChange`
2. Update the URL with the search params.
3. Keep the URL in sync with the input field.
4. Update the table to reflect the search query.

Searching component + sync with field and URL + debouncing optimization

```ts
"use client";

import { MagnifyingGlassIcon } from "@heroicons/react/24/outline";
import { usePathname, useSearchParams, useRouter } from "next/navigation";
import { useDebouncedCallback } from "use-debounce";

export default function Search({ placeholder }: { placeholder: string }) {
  const searchParams = useSearchParams();
  const pathname = usePathname();
  const { replace } = useRouter();

  const handleSearch = useDebouncedCallback((term) => {
    console.log(`Searching... ${term}`);
    const params = new URLSearchParams(searchParams);
    // params.set('page', '1'); pagination
    if (term) {
      params.set("query", term);
    } else {
      params.delete("query");
    }
    replace(`${pathname}?${params.toString()}`);
  }, 500);

  return (
    <div className="relative flex flex-1 flex-shrink-0">
      <label htmlFor="search" className="sr-only">
        Search
      </label>
      <input
        className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
        placeholder={placeholder}
        onChange={(event) => handleSearch(event.target.value)}
        defaultValue={searchParams.get("query")?.toString()}
      />
      <MagnifyingGlassIcon className="absolute left-3 top-1/2 h-[18px] w-[18px] -translate-y-1/2 text-gray-500 peer-focus:text-gray-900" />
    </div>
  );
}
```

### [Mutating Data - "CRUD"](https://nextjs.org/learn/dashboard-app/mutating-data)

### [`revalidatePath` Fresh Data fetching](https://nextjs.org/learn/dashboard-app/mutating-data#6-revalidate-and-redirect)

Allows fresh data to be fetched from the server.

### [Errors and NotFound](https://nextjs.org/learn/dashboard-app/error-handling)

- `error.tsx` UI rendered upon any error (catch-all)
- `not-found.tsx` UI served when used the `{ notFound } from 'next/navigation';`

### [Metadata and SEO](https://nextjs.org/learn/dashboard-app/adding-metadata)

## Checklist to optimize pages

- Created a database in the same region as your application code to reduce latency between your server and database.
- Fetched data on the server with React Server Components. This allows you to keep expensive data fetches and logic on the server, reduces the client-side JavaScript bundle, and prevents your database secrets from being exposed to the client.
- Used SQL to only fetch the data you needed, reducing the amount of data transferred for each request and the amount of JavaScript needed to transform the data in-memory.
- Parallelize data fetching with JavaScript - where it made sense to do so.
- Implemented Streaming to prevent slow data requests from blocking your whole page, and to allow the user to start interacting with the UI without waiting for everything to load.
- Move data fetching down to the components that need it, thus isolating which parts of your routes should be dynamic in preparation for Partial Prerendering.
- Using Debouncing to prevent triggers in requests to the server everytime something occurs, adding a delay before the next thing, like for each keystroke make a request to query something, adding a debounce, it adds a delay before triggering the query, allowing multiples keystrokes without triggering requests

## Extra

### [Setting up PostgreSQL in Vercel](https://nextjs.org/learn/dashboard-app/setting-up-your-database)

- Project in GitHub
- Deploy in Vercel
- In Vercel dashboard > "Storage" > Postgres > After creation > tab `.env.local` > "Show Secrets" > "Copy Snippet"
- In your project file `.env` paste the secrets copied from the DB
- run in project folder `npm i @vercel/postgres`
- For "automatic" database seeding checkout `seed.js` file, and insert the the script in `package.json` > `"seed": "node -r dotenv/config ./scripts/seed.js"` then run `npm run seed`

### [Other cool CheatSheet](https://medium.com/@yuvrajkakkar1/next-js-14-unleashed-%EF%B8%8F-a-comprehensive-cheat-sheet-for-modern-web-development-86721d678379)
