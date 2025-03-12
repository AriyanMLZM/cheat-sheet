`npx create-next-app`

## Routing

directory based routing.

`app/page.tsx`  
entry point '/' route of app.

`app/about/page.tsx`  
route of '/about'

`import Link from "next/link"`  
`<Link href="/about">About</Link>`  
make links to navigate in different routs of app.

`import { useRouter } from "next/navigation"`  
`const router = useRouter()`  
`router.push('/path')`  
change the current route.

`import { notFound } from 'next/navigation`  
`notFound()`  
this will make a 404 error and shows the default not found page or the not-found.tsx file.

### Dynamic Route

`app/path/[id]/page.tsx`  
create a slug that serves as dynamic route.  
`Page({ params: { id } })`  
we can get the params as prop in page comp.

### Static Params

`app/user/[userId]/page.tsx`  
generate the static params for this slug.

```
export async function generateStaticParams() {
    const usersData: Promise<User[]> = getAllUsers()
    const users = await usersData

    return users.map(user => ({
        userId: user.id.toString()
    }))
}
```

static params for a dynamic route that change the SSR to SSG.

## Fetching Strategies

- `fetch('', { cache: 'force-cache' })`  
  always cache the data.
- `fetch('', { cache: 'no-store' })`  
  don't cache the data
- `fetch('', { next: { revalidate: 60 } })`  
  implements ISR approach that automatically get updated datas every 60secs.

## Special Files

- page.tsx  
  the index file of each route.
- layout.tsx  
  the layout of pages that apply also to the inner routes pages.
- error.tsx  
  make a costume error boundary to catch the errors within each routes.
- loading.tsx  
  make a costume suspense based loading for each page.
- not-found.tsx  
  make a costumed not-found page that renders on 404 errors.

## Metadata

`import type { Metadata } from 'next`

```
export const metadata: Metadata = {
  title: "doc title",
  description: "this is my Web."
}
```

we can export our costumed metadata in each page of our app.

### Dynamic Metadata

```
export async function generateMetaData({ params, searchParams}) {
  const { id } = params
  const data = await getData(id)

  return {
    title: data.title
  }
}
```

we can generate the metadata based on the params.  
the generator gets the params as input and return a metadata object.

## Styling

`app/globals.css`  
use a global css file for whole app and import it in root layout.tsx.  
`import './globals.css'`

`page.module.css`  
make individual css files for components that will be only applied to that comp.  
`import styles from './page.module.css`  
`<div className={styles.className} />`

## Types

`types.d.ts`  
we can declare our types that are used in our app in .d.ts files and will be used automatically without exporting.
