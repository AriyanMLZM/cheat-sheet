# Next js

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

```js
export async function generateStaticParams() {
	const usersData: Promise<User[]> = getAllUsers()
	const users = await usersData

	return users.map((user) => ({
		userId: user.id.toString(),
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
- route.ts  
  make the api routes endpoints.

## Metadata

`import type { Metadata } from 'next`

```js
export const metadata: Metadata = {
	title: 'doc title',
	description: 'this is my Web.',
}
```

we can export our costumed metadata in each page of our app.

### Dynamic Metadata

```js
export async function generateMetaData({ params, searchParams }) {
	const { id } = params
	const data = await getData(id)

	return {
		title: data.title,
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

## Api Routes

`app/api/path/route.ts`  
we create our endpoints in route.ts files.

```js
export const GET = async () => {
	return new Response('hello!')
}
```

simple get method in route.ts.

```js
import { NextResponse } from 'next/server'

return NextResponse.json({ msg: 'hello!' })
```

we can use nextResponse to send back json objects.

```js
export const GET = (req: Request) => {
	const { searchParams } = new URL(req.url)
	const name = searchParams.get('name')

	return NextResponse.json({ name })
}
```

get the search params from the req.

```js
export const GET = (req, { params: { id } }) => {
	...
}
```

get the params of dynamic route.

```js
export const POST = async (req: Request) => {
	const data = await req.json() // req.body
	const { name, email } = data

	return NextResponse.json({ name, email })
}
```

read the body data of req in post method.

### Middleware

`src/middleware.ts`  
special file that should be the same level as app dir.

```js
export const middleware = (req) => {
	...

	return NextResponse.next()
}
```

works as middleware for all the routes request.

```js
export const config = {
	matcher: '/api/:path*', // can be regex
}
```

narrow down the routes that that middleware apply to.  
we can also write if statements in middleware to check the route if matches.

## Env

`.env.local`  
store our env vars in this file in root dir.

`process.env.API_KEY`  
access the env var value.

## Types

`types.d.ts`  
we can declare our types that are used in our app in .d.ts files and will be used automatically without exporting.
