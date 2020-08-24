<h1 align="center">
Whack a Vue
</h1>

<div align="center">
<img width="150" src="https://tepexic.com/whack-a-vue/whack-a-vue.gif" alt="Whack a vue demo" />
</div>

<p align="center">Vue implementation of the Whack-A-Mole game, as seen in Wes Bos' <a href="https://javascript30.com/" target="_blank">Javascript30 course</a></p>

This Vue implementation uses the Mole.vue component to emmit the "bonk" event to the parent container (App.vue) and increase the score, whenever a mole is clicked.

The score is multiplied by the level(1-10), which is based on a random time that decreases linearly. There is an all time high score, stored in localStorage. The mole does not appear at the same hole twice in a row.

The countdoun timer resets at the end of every level. 

All CSS styling is handled by TailwindCSS. [See it live on Netlify](https://whack-a-vue.netlify.app/)


## Dependencies
 - @fullhuman/postcss-purgecss
 - @vue/cli-plugin-babel
 - @vue/cli-plugin-eslint
 - @vue/cli-service
 - babel-eslint
 - eslint
 - eslint-plugin-vue
 - purgecss
 - tailwindcss
 - vue-template-compiler

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
