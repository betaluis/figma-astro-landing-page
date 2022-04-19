# Getting Started with the Develpoment

## Installing Astro

> npm init astro

Get started with the generic template.

> npm install

Set up your git repository.

> npm run dev

## Installing other dependencies

> npm i astro-icon

- Minify our own svg icons.

> npm i -D postcss autoprefixer

> npm i -D open-props postcss-jit-props

### Customizing Stack

Add Config to astro.config.mjs

    vite: {
        ssr: {
            external: ["svgo],
        },
    },

- Allows us to minify our local svgs. 

Got to package.json and add in "browserList":

    "browserList": [
        "defaults"
    ],

Add new file called `postcss.config.cjs`:

    const postcssjitprops = require("postcss-jit-props");
    const OpenProps = require("open-props");

    module.exports = {
        plugins: [
            postcssjitprops(OpenProps),
            require('autoprefixer')
        ]
    }

> npm run dev

- If everything was done correctly you should be able to launch a local server.


