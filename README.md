### Issues with [TanStack Form SSR](https://tanstack.com/form/latest/docs/framework/react/guides/ssr)

Below heading: Using TanStack Form in TanStack Start

1. Console error: `No HTTPEvent found in AsyncLocalStorage. Make sure you are using the function within the server runtime.`

```
(index):2 Injected From Server:
__TSR_SSR__.initMatch({"id":"__root__","__beforeLoadContext":"{}","loaderData":"{\"$undefined\":0}","error":"{\"$undefined\":0}","extracted":null,"updatedAt":1751828052645,"status":"success","ssr":true})
(index):3 Injected From Server:
__TSR_SSR__.initMatch({"id":"/","__beforeLoadContext":"{}","loaderData":"{\"$undefined\":0}","error":"{\"$error\":{\"message\":\"No HTTPEvent found in AsyncLocalStorage. Make sure you are using the function within the server runtime.\",\"stack\":\"Error: No HTTPEvent found in AsyncLocalStorage. Make sure you are using the function within the server runtime.\\n    at getEvent (file:///node_modules/@tanstack/start-server-core/dist/esm/h3.js:30:11)\\n    at file:///node_modules/@tanstack/start-server-core/dist/esm/h3.js:44:20\\n    at getInternalTanStackCookie (/node_modules/@tanstack/react-form/src/start/utils.ts:16:18)\\n    at getFormData (/node_modules/@tanstack/react-form/src/start/getFormData.tsx:15:16)\\n    at getFormDataFromServer (/src/routes/index.tsx:69:12)\\n    at middlewareFn (/node_modules/@tanstack/start-client-core/src/createServerFn.ts:987:30)\\n    at applyMiddleware (/node_modules/@tanstack/start-client-core/src/createServerFn.ts:874:10)\\n    at next (/node_modules/@tanstack/start-client-core/src/createServerFn.ts:256:14)\\n    at executeMiddleware (/node_modules/@tanstack/start-client-core/src/createServerFn.ts:274:10)\\n    at run (/node_modules/@tanstack/start-client-core/src/createServerFn.ts:162:15)\",\"cause\":{\"$undefined\":0}}}","extracted":null,"updatedAt":1751828052641,"status":"error","ssr":true})
(index):4 Injected From Server:
__TSR_SSR__.dehydrated = "{\"manifest\":{\"routes\":{\"__root__\":{\"preloads\":{\"$undefined\":0},\"assets\":[{\"tag\":\"script\",\"attrs\":{\"type\":\"module\",\"suppressHydrationWarning\":true,\"async\":true},\"children\":\"import { injectIntoGlobalHook } from \\\"/@react-refresh\\\";\\ninjectIntoGlobalHook(window);\\nwindow.$RefreshReg$ = () => {};\\nwindow.$RefreshSig$ = () => (type) => type;;;import('/~start/default-client-entry')\"}]}},\"clientEntry\":\"/~start/default-client-entry\"},\"dehydratedData\":{\"$undefined\":0},\"lastMatchId\":\"/\"}"
react-dom_client.js?v=41e9480f:17987 Download the React DevTools for a better development experience: https://react.dev/link/react-devtools
react-dom_client.js?v=41e9480f:6264 Error: No HTTPEvent found in AsyncLocalStorage. Make sure you are using the function within the server runtime.
    at getEvent (/node_modules/@tanstack/start-server-core/dist/esm/h3.js:30:11)
    at /node_modules/@tanstack/start-server-core/dist/esm/h3.js:44:20
    at getInternalTanStackCookie (/node_modules/@tanstack/react-form/src/start/utils.ts:16:18)
    at getFormData (/node_modules/@tanstack/react-form/src/start/getFormData.tsx:15:16)
    at getFormDataFromServer (/src/routes/index.tsx:69:12)
    at middlewareFn (/node_modules/@tanstack/start-client-core/src/createServerFn.ts:987:30)
    at applyMiddleware (/node_modules/@tanstack/start-client-core/src/createServerFn.ts:874:10)
    at next (/node_modules/@tanstack/start-client-core/src/createServerFn.ts:256:14)
    at executeMiddleware (/node_modules/@tanstack/start-client-core/src/createServerFn.ts:274:10)
    at run (/node_modules/@tanstack/start-client-core/src/createServerFn.ts:162:15)

The above error occurred in the <MatchInnerImpl> component.

React will try to recreate this component tree from scratch using the error boundary you provided, CatchBoundaryImpl.

defaultOnCaughtError @ react-dom_client.js?v=41e9480f:6264
chunk-WW3J4ABH.js?v=41e9480f:188 Warning: The following error wasn't caught by any route! At the very least, consider setting an 'errorComponent' in your RootRoute!
warning @ chunk-WW3J4ABH.js?v=41e9480f:188
chunk-WW3J4ABH.js?v=41e9480f:188 Warning: No HTTPEvent found in AsyncLocalStorage. Make sure you are using the function within the server runtime.
warning @ chunk-WW3J4ABH.js?v=41e9480f:188
```

2. Guide is missing imports:

   `Cannot find name 'createServerFn'.`

   -> `import { createServerFn } fro '@tanstack/react-start'`

   `Cannot find name 'setResponseStatus'`s

   -> `import { setResponseStatus } from '@tanstack/react-start/server'`

3. Other TS errors:

`key={error as string}`

-> `Conversion of type 'undefined' to type 'string' may be a mistake because neither type sufficiently overlaps with the other. If this was intentional, convert the expression to 'unknown' first.`

`.handler(async (ctx) => {` TS error:

```
Argument of type '(ctx: ServerFnCtx<"POST", "data", undefined, (data: unknown) => FormData>) => Promise<Response | "There was an internal error" | "Form has validated successfully">' is not assignable to parameter of type 'ServerFn<"POST", "data", undefined, (data: unknown) => FormData, Response | "There was an internal error" | "Form has validated successfully">'.
Type 'Promise<Response | "There was an internal error" | "Form has validated successfully">' is not assignable to type '"There was an internal error" | "Form has validated successfully" | Promise<"There was an internal error" | "Form has validated successfully" | { readonly headers: { append: "Function is not serializable"; ... 9 more ...; [Symbol.iterator]: "Function is not serializable"; }; ... 14 more ...; text: "Function is not s...'.
 Type 'Promise<Response | "There was an internal error" | "Form has validated successfully">' is not assignable to type 'Promise<"There was an internal error" | "Form has validated successfully" | { readonly headers: { append: "Function is not serializable"; delete: "Function is not serializable"; get: "Function is not serializable"; ... 7 more ...; [Symbol.iterator]: "Function is not serializable"; }; ... 14 more ...; text: "Function...'.
   Type 'Response | "There was an internal error" | "Form has validated successfully"' is not assignable to type '"There was an internal error" | "Form has validated successfully" | { readonly headers: { append: "Function is not serializable"; delete: "Function is not serializable"; get: "Function is not serializable"; ... 7 more ...; [Symbol.iterator]: "Function is not serializable"; }; ... 14 more ...; text: "Function is not ...'.
     Type 'Response' is not assignable to type '"There was an internal error" | "Form has validated successfully" | { readonly headers: { append: "Function is not serializable"; delete: "Function is not serializable"; get: "Function is not serializable"; ... 7 more ...; [Symbol.iterator]: "Function is not serializable"; }; ... 14 more ...; text: "Function is not ...'.
       Type 'Response' is not assignable to type '{ readonly headers: { append: "Function is not serializable"; delete: "Function is not serializable"; get: "Function is not serializable"; getSetCookie: "Function is not serializable"; has: "Function is not serializable"; ... 5 more ...; [Symbol.iterator]: "Function is not serializable"; }; ... 14 more ...; text: "F...'.
         The types of 'headers.append' are incompatible between these types.
           Type '(name: string, value: string) => void' is not assignable to type '"Function is not serializable"'.
```
