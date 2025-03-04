# Components

single files with main three sections:

- script
- html elements
- css

# Script js/ts

`<script lang="ts"> js/ts code </script>`  
script tag for logic coding.

`let { propName, children }: { propName: string, children: snippet} = $props()`  
receive props with Prop Rune.  
we get children prop as snippet.

`let reactiveState = $state('initial')`  
declare state with State Rune.

`let derivedState = $derived('hello ' + name)`  
declare a derived state that is based on value of another state with Derived Rune.

`$inspect(var)`  
used to track a var and debugging and when changes this Rune will tell us.

## Store

`/store/index.js`  
we can make a store to have global states.

`import { writable } from "svelte/store"`  
`export const globalSate = writable(initial)`  
we can use Writable to make a global State.

`import { globalState } from '/store'`  
`$globalState`  
we can use the globalState by importing it from store and use it reactively with $ sing.

## Side Effects

run function when value changes.

`$: function(value)`  
basic way of side effects. function will run when value changes.

`$effect(() => {})`  
side effect with Effect Rune.  
by default will run onMount.

`$effect(() => {`  
`...`  
`return() => {}`  
`})`  
run return function on UnMount.

# Html Elements

`<Header prop1={prop1} {prop2} />`  
passing props to comp.

`<input bind:value={value} />`  
binding values of elements to the vars.

`<p> this is my {text} </p>`  
use vars in elements content.

`<button on:click={func} onclick={func} {onclick}> click </button>`  
declare events handlers of elements.

## Special Templates

`<#if condition> elements </if>`  
basic if statement.

`<#if cond> ... <:else if cond> ... <:else> ... </if>`  
else if statements.

`{#snippet subComp({props}: {types})}`  
`elements`  
`{/snippet}`  
we can use Snippet Rune to declare a sub comp inside a comp file.  
`{@render subComp({props value})}`  
to render the snippet comp.

`{@render children({props value})}`  
we can also use render for children prop.

`{#each items as item (loop key)} ... {/each}`
basic loop over array.

## Animations

`<div transition:fly={{ x: 200, duration: 200, opacity: 0}}> ... </div>`  
we can use simple built-in animations of svelte.

`in:fly{{}} out:fly={{}}`  
we can set the entrance and exit anim of an element.

## Svelte Tag

`<svelte:window bind:scrollY={y} />`  
we can bind different attributes of window with our vars.

`<svelte:head>`  
`<title>document title</title>`  
`</svelte:head>`  
we can set he meta tags of head.

# Css

the css only targets the current comp elements.

`<style> pure css </style>`  
we can write pure css.

`:global(target) {...}`  
used to target globally and effect all the comps.

# Routing (SvelteKit)

file based routing.

`src/routes/`  
the main routing folder index page.

- +page.svelte - the index file.
- +layout.svelte  
  two main special files.

`src/route/about/+page.svelte`  
`/about`  
create a route with folder.

`<slot> page content </slot>`  
used in <strong>layout</strong> file. this tag will render the page file as children inside of it automatically.

`layout.reset.svelte`  
this special comp will overwrite the upper layouts.

`/[slug]/+page.svelte`  
dynamic routing with slugs.  
`load({ fetch, page })`  
`page.params.slug`  
to get the slug value with load.  
`import { page } from '$app/state'`  
`page.params.slug`  
to get the slug value with no load.

`error.svelte`  
costume error page.  
`load({ error })`  
`error.message`  
we can use the error prop in our template.

# Data fetching (SvelteKit)

`<script context="module">`  
`export async function load({ fetch }) {`  
`const res = await fetch(url)`  
`const data = await res.json()`  
`return {props: data}`  
`}`  
`</script>`  
we fetch the data in this script tag in comp file.  
load is special function.  
`export let data`  
we can get the data as prop in normal script tag.

`return { prop, status, redirect, error}`  
the attributes that we can use in return of <strong>load function</strong>.

- prop: for the data
- status: the status code - 404, ...
- redirect: the url to redirect to on 404
- error: pass the error object

`<a sveltekit:prefetch href="/path">`  
prefetch the data of the link on hover load the path faster.

# Api Endpoints (SvelteKit)

`/about/index.json.js`  
this is the basic endpoint in /about route.

`export async function get()`  
`return { status, body }`  
get func for handling get requests.

`[id].json.js`  
dynamic endpoint.  
`get({ params })`  
`params.id`  
access the id value.
