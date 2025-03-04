`npm i typescript`  
`tsc main.ts output.js`  
compile the ts files to js.

`tsc -w`  
watch all the files in rootDir.

`tsc --noEmitOnError -w`  
this will won't compile if there is ts error.

# TS Config

`tsc --init`  
make a ts config file.

`rootDir: "./src"`  
the root dir of ts files.  
`outDir: "./build/js`  
the compiled files dir.

`target: "es2016"`  
the version of js lang.

`noEmitOnError: true"`  
this stops the compiling the js if there is ts error.

`include: ["src"]`  
only watch these files dirs.

# Types

`let a: string = "ali"`  
`let a: number = 12`  
`let a: boolean = true`  
basic types.

`let a: any`  
can be anything.

`let a: number | string`  
union type.

`let a: number[]`  
array type.

`let a: (number | string)[]`  
mixed array type.

`let a: [number, string]`  
Tuple type.

`enum var {a, b, c}`  
declare enum.  
var.a --> 0  
`enum var {a = 2, b}`  
set the index manually.  
var.b --> 3

`let a: "ali"`  
literal types.

`<T1 extends T2>`  
combined types.

`type a = Exclude<unionType, type>`  
exclude the type from union that can not be used.  
`type a = Extract<unionType, type>`  
use only the extracted type from union.

`type a = NonNullable<type>`  
exclude the null and undefined from the type.

`let a: object`  
`let a: RegExp = /\w+\g`

## objects

`let a: {prop1: number; prop2: string}`  
json object type.

`type a = {prop: number, prop2: string}`  
declare a type.

`{prop?: number}`  
optional prop.

`obj.name?.toUpperCase()`  
we make the prop optional to run the method in case of undefined possibility.

`interface a {prop: number}`  
declare an interface. works like a type.

`interface a { readonly [index: string]: number}`  
index signature to use the dynamic index on object.

`type a = Record<string, number>`  
use Record to set the type of object.

`a as keyof interfaceName`  
set the type as the keys of an object.

`let a: Partial<interfaceName>`  
Partial type to be a sub type of another type.

`let a: Required<interfaceName>`  
all the props are required from interface even the optionals.

`let a: Readonly<interfaceName>`  
can not be reassigned later.

`let a: Pick<interfaceName, type>`  
pick the type from interface and use that.  
`let a: Omit<interfaceName, type>`  
omit the type from interface that can not ber used.

## functions

`const func = (a: number, b: string): number => {}`  
func params types.

`(a?: number, b: string)`  
optional func param.

`(a: number, ...params: number[])`  
the rest params type.

`const func = <T>(a: T): boolean => {}`  
we can use generic type that can be anything.

`type a = ReturnType<typeof funcName>`  
grt the return type of func automatically.

`type a = Parameters<typeof funcName>`  
get the parameters type of func automatically.

`type a = Awaited<ReturnType<typeof funcName>>`  
Awaited used to get the return type of async func.

## Type Assertion or Type Casting

`let a = b as string`  
we make less or more specific type.

`let a = func() as string`  
we determine the exact return type of func.

`let a = b!`  
not Null Assertion.  
tell ts that we know that is not null.

## Classes

`constructor(public a: string, private a: number, protected c: boolean)`  
we need to set the attributes' types and visibility modifiers in constructor of class.

- private - can only be accessed in own class.
- protected - can also be accessed in sub classes.
- public - can be accessed anywhere.

`class a implements interfaceName {}`  
set an interface to a class.

`static a: number = 0`  
static vars refers directly to class and not the objects.
