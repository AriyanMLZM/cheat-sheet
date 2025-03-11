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

## Special Files

- page.tsx  
  the index file of each route.
- layout.tsx  
  the layout of pages that apply also to the inner routes pages.
- error.tsx  
  make a costume error boundary to catch the errors within each routes.
- loading.tsx  
  make a costume suspense based loading for each page.

## Styling

`app/globals.css`  
use a global css file for whole app and import it in root layout.tsx.  
`import './globals.css'`

`page.module.css`  
make individual css files for components that will be only applied to that comp.  
`import styles from './page.module.css`  
`<div className={styles.className} />`
