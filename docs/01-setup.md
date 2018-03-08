## 01-Setup:

Branch: [01-setup](/tree/01-setup)

First things first, we're going to use [yarn](https://yarnpkg.com) instead of `npm` to ensure our dependencies are in
lock step.

Now install broccoli-cli globally:

`yarn global add broccoli-cli`

Then, create a new directory for this tutorial, and:

`yarn add --dev broccoli`

In your `package.json` add the following to the `scripts` node (add this if it's not present):

```
"scripts": {
    "clean": "rm -rf dist",
    "build": "npm run clean && broccoli build dist",
    "serve": "broccoli serve || 1",
    "debug-build": "npm run clean && node $NODE_DEBUG_OPTION $NODE_DEBUG_OPTION $(which broccoli) build dist",
    "debug-serve": "node $NODE_DEBUG_OPTION $(which broccoli) serve"
},
```

You can now use `npm run build` and `npm run serve` for convenience.]

Note, the `debug-build` and `debug-serve` are for use with [VS Code](https://code.visualstudio.com/) to allow for
interactive debugging. If you wish to use this, you'll need the files in [this directory](.vscode). You can add 
breakpoints and then hit the `debug` icon (or CMD + SHIFT + D) and click "play".

Now create a `Brocfile.js` in the root of your project, with the contents: `module.exports = "app";`.

Next, create a directory `app` within the project, and add a `index.html` file with the contents `Eat your greens!`.

That's it, you're done.

The initial setup of this tutorial merely copies files from the input `app` directory by exporting the string `app`.
The `Brocfile.js` contains the Broccoli configuration for the build. The `module.exports` line must export a Broccoli
tree. "But it's a string" you say, yes, Broccoli will automatically convert a string into a `source node`, and on build,
validate that the directory exists. In this case, the Brocfile merely exports a single tree, containing the contents of
the `app` directory, this will then be copied to the destination directory (`dist` in our case).

To run a build, run `npm run build` (if you added the script) or `rm -rf dist && broccoli build dist`.
You should see something like:

```
> broccoli-tutorial@0.0.0 build /Users/oli/Projects/broccoli-tutorial
> npm run clean && broccoli build dist

> broccoli-tutorial@0.0.0 clean /Users/oli/Projects/broccoli-tutorial
> rm -rf dist
```

This npm run command will remove any previous builds, and run a new build, outputting to the `dist` directory.
Broccoli doesn't remove previous builds by default, so we must remove it before starting a new build.

The contents of `app` should now be in the `dist` directory. Try:

```
$ cat dist/index.html
Eat your greens!
```

Now try running `npm run serve` or `broccoli serve` and open `http://localhost:4200`, you should see your the same
output.

Great, your first Broccoli build is complete, pat yourself on the back 👏.

Next: [Filtering files](/blob/parts/02-filtering-files/docs/02-filtering-files.md)
