# Setup
1. Clone or fork the [repo](https://github.com/lpj-app/npm-package-template)

2. Install dependencies
```bash
npm i 
```

# Add custom functionality
Add your package functionality in `/src/index.ts`


# Publishing process

## 1. Customize the package metadata in `/package.json`

In the `package.json` file, customize the following fields:
- `name` -> this will be the name of your package on npm for scoped packages use `@<your-npm-username>/<package-name>`
- `version` -> Package version, needs to be increases with every release
- `description` -> Short package description
- `author` -> Your name
- `license` -> License type (e.g. MIT) as needed
- `keywords` -> Array of keywords that describe your package
- `main` -> The main entry point of the package (if changed from templates default)
Also when using git it's recommended to update the `repository` field with the package's git repo url as well as the `bugs/url` and `homepage` fields with the package's homepage url..

>**IMPORTANT**: Check files whitelist <br>
>In package.json, the files field is set to ["dist"]. This means only the contents of the dist folder 
> (plus mandatory files like README, LICENSE, and package.json) will be included in the final npm package. <br>
>If you add new folders (e.g., an assets folder) that should be part of the package, you must add them to the files array in `package.json`.

## 2. Tests
The file is located in `/tests/index.test.ts` (Write your own tests here, to check if your package works as expected) <br>

To test the package functionality, run: <br>
```bash
npm test
```
###
## 3. Build and Local Testing
    To compile your TypeScript into production-ready JavaScript, run the build command. The output will be stored in the `/dist` folder.

    ```bash
    npm run build
    ```

    <br/>
Testing locally ensures that your library functions correctly as a standalone package before you publish it to npm.
###
### 3.1. Soft Local Test

To test the package locally without publishing it to the web, use `npm link`. This is ideal for rapid development.

1. **In your package folder**: Run `npm link`
2. **In your test project**: Run `npm link <your-package-name>`

Now you can import your package in your test project and test it as if it were published. Changes you make in your library source code are reflected immediately in the test project.
###
### 3.2. Hard Local Test

If the soft test worked without problems, it is highly recommended to perform a "hard" local test. This simulates the actual installation process.

1. **In your package folder**: Create a packed archive with `npm pack`
2. **In your test project**: Install the created archive:
```bash
# You can install it directly from the path without moving the file
npm install ../path/to/numislib-api/numislib-1.0.0.tgz

```



> **Pro-Tip**: Installing the `.tgz` directly keeps your test project cleaner by avoiding manual file moves.

---
###
#### Comparison of Testing Methods

| Method | Best For... | Why it's important |
| --- | --- | --- |
| **Soft Test (`npm link`)** | Rapid development and debugging. | Changes are reflected immediately without rebuilding or reinstalling. |
| **Hard Test (`npm pack`)** | Verifying the published structure. | Ensures the `files` array in `package.json` includes the `data` folder and internal paths resolve correctly inside `node_modules`. |


> **Note** <br> 
> If you make changes to the source code, you need to run `npm run build` again in the 
> package directory for the changes to take effect in your test project.

Now you can import it as any other package. Example for this template:
```js
import {helloWorld, goodbyeWorld} from "@lpj.app/npm-package-template";

console.log(helloWorld());
console.log(goodbyeWorld());
```
and run it with 
```bash
node .\tests\manual-test.js
```
If your output is as expected, you can publish the package.

## 4. Publish
To publish a npm package you need to have an account on [npmjs.com](https://www.npmjs.com/) and setup the 2FA in your account settings. <br> 
With this done you can continue in your package directory. <br>

### 4.1 Verify publish with dry run
It is highly recommended to run a "dry run" first. 
This simulates the publishing process and shows you exactly which files will be included in your package without actually uploading it:
```bash
npm publish --dry-run
```
Check the output list. If you don't see the dist folder or if important files are missing, check your files array in `package.json`.

To finally publish the package to the public npm registry login to npm with `npm login`, follow the login instructions in the terminal then run
```bash
npm publish --access public
```
You will be asked to login to your account in a browser window. <br> 
After successful login, the package will be published automatically and you can track it in your npm account under `Packages`.

### 

# Usage 
After publishing your npm package to the public registry you'll get an install command like `npm i @lpj.app/npm-package-template` in the npm package site. <br>
<br>
From here it's the same process as for any other npm package.

> **IMPORTANT** <br>
> Keep in mind that the package template is optimized for ES Modules structure, 
> so when creating a new project where you want to use your package, make sure to 
> initialize the project with `npm init -y && npm pkg set type="module"` 
> or change the `type` field in `package.json` to `"module"` later on.

When using the package in your project, you can import it like any other package and use your custom functionality e.g.:
```js
import { helloWorld, goodbyeWorld } from "@lpj.app/npm-package-template";

console.log(helloWorld());
console.log(goodbyeWorld());
```

# Other
- [npm template package site](https://www.npmjs.com/package/@lpj.app/npm-package-template)

---
## License

See [LICENSE](./LICENSE).

--- 

&copy; [lpj.app](https://github.com/lpj-app). Licensed under MIT.
