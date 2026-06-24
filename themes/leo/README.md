# Leo

Leo is the local Hexo theme for this site.

It currently keeps the visual baseline of Cactus so the site can switch themes
without a visible redesign. Future layout and style changes should happen here
instead of in `themes/cactus`.

## Runtime Model

Leo is a native Hexo theme:

- templates live in `layout/`
- theme helpers and generators live in `scripts/`
- styles, scripts, fonts, and static assets live in `source/`
- default theme options live in `_config.yml`
- site-specific overrides live in the root `_config.yml` under `theme_config`

There is no separate Gulp/Webpack/Vite build step for the theme. Hexo renders
EJS and Stylus through the root project dependencies, which keeps the theme
smaller and easier to maintain across future Node and Hexo upgrades.

## Usage

The root `_config.yml` should point to this theme:

```yml
theme: leo
```

Then verify the site from the repository root:

```sh
npm run clean
npm run build
npm run server
```

## Customization

Prefer this order when changing the theme:

1. Use root `theme_config` for site-specific values.
2. Change `themes/leo/_config.yml` for Leo defaults.
3. Change `layout/` for HTML structure.
4. Change `source/css/` for visual design.
5. Change `scripts/` only for Hexo helpers or generators.

For style work, start with:

- `source/css/style.styl`
- `source/css/_variables.styl`
- `source/css/_colors/`
- `source/css/_partial/`

## Origin

Leo is derived from Cactus by Pieter Robberechts and keeps the original MIT
license notice in `LICENSE`.
