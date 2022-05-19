## TV Show Finder

## Draft

### General Todos

#### naming conventions

- folders & files
  - js files
  - pages
  - components
- media
- functions & variables
- css

installed tools & dependencies

- [ ] Vue cli
- [ ] vue-axios
- [ ] tailwindcss

#### dependencies installing steps

- create vue app using Vue-cli
- cleanup the app
- install dependencies,
- add tailwind, then create postcss.config.js from its docs
- initialise tailwindcss using cli command: npx tailwindcss init

#### app folders & files - creations & communication

- import VueRouter into main & we let Vue use it
- we then create routes file, import routes into main
- in App.vue add <router-view/> into the template to render the routes
- create css folder, css/styles.css then we paste as tailwindcss docs
- then in app.js we import as tailwindcss docs
- start with mocked data before the actual fetching

#### pages

- home
- ...

#### components

- in theory
  split into 4 categories
- atoms (base components like button, input & an alert)
- molecules (combinations of correlated components & other elements like a card & a spinner …etc)
- blocks (full pieces of a page, consist of multiple components & other elements, not necessarily interacted with each other)
- organisms (organizing by folders full UI-components existence of a process like login (forms, blocks), or like header on (desktop, mobile) …etc)
- in action
- header
  - Navbar.vue
  - SearchForm.vue
  - ...

#### Notes

- to get rid of hash in the url, we add into the router a property (mode) : “history”
-
-

#### Challenges Occurred during the development phase

- an error happened due to tailwind version, check the docs to install the recommended
-

#### TODOS

- feature card in the homepage
- about page with regards
- not found page
- closeMenu
- clear console warnings
- toggle body scrolling when submenu is opened
