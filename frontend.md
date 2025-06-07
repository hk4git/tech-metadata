## Javascript | Commmon
- `import a, { b, c } from ''`
We put non default exports in {} braces e.g. a-> default export, b, c -> non default expoerts.
We can change default import by directly changing name, we can change name to non default using alias 'as' syntax 
e.g. `import A { b as B, c as C} from ''`
Tools like Bable does auto conversion to support ES Module

- Vite: uses incremental module, HMR -> Hot Module replacement (keeps existing module state intact while loading incremental/new modules). 

- JSX: JavaScript eXtension. let us write HTML & Javadscript togather. wrtite javacscript in curly braces {}.
- TSX: equavalent JSX, addtional type checking etc. enabled.

- contexts:
  - The reason React has contexts is to allow for multiple sibling components to share a piece of state-data.
  - The implementation requires that a component be created, called a Context.Provider component, and then you have to wrap the components who need access to the shared data inside the Context.Provider
  - The Provider is used to wrap the part of your component tree where you want the context to be available. It accepts a compulsory value prop that holds the data you want to share across other components. When the value prop of the Provider changes, all descendants that consume the context will re-render.
  The Consumer allows any descendant component to use the context. It takes a function as a child, where the function argument is the current context value. In modern React, the useContext hook is often used instead of Consumer for better readability and simplicity.
  - Context API is a term that is created to pass as a global variable and can be accessed anywhere in the code.
  ```
  <MyContext.Provider value={{ text, setText }}>
	in child component: const { text, setText } = useContext(MyContext);
  ```

 ## Fluent AI:
Fluent AI is a collection of UX guidance, patterns, and React components for building Copilot experiences based on Fluent UI React v9 and the Fluent 2 design language.
- https://ai.fluentui.dev/?path=/docs/welcome--docs [Microsoft specific]
- https://react.fluentui.dev/?path=/docs/icons-catalog--docs [Microsoft specific]
- https://github.com/microsoft/fluentui [public]
- https://github.com/microsoft/fluentai
- styling: https://griffel.js.org/

## NPM

### Routine:
- `npm install -g vsts-npm-auth --registry https://registry.npmjs.com --always-auth false`
- `npm config set registry https://registry.npmjs.org/`
- `npx vsts-npm-auth -c .npmrc`, If you get **error like couldn't get an authentication token for** ..., It may be possible that existing Auth/PAT expired (due to org policy - like expires PAT in a week or so ) then do 
  **delete ".npmrc" form /users folder & then try again.**
- `npm install  --force`

## Issues:
- Could not find a declaration file for module ''. implicitly has an 'any' type.
  Ans: definne, type file in solution.

