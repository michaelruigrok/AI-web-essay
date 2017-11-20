# You’re Unknowingly Helping Create the Future of AI — And Why That’s a Good Thing

A website essay I put together for the University of Queensland Course
COMU3110: Media Platforms. The article is aimed at the general public, and
aims to educate readers about the mechanics involved with and the cultural
implications of machine learning data sets, as well as the importance of
diverse, unbiased, and comprehensive data. The article features several
interactive set pieces, mostly built out of svgs.

In order to host the production build of the site yourself, you'll need to
replace the production ReCAPTCHA key with your own in
`src/componenets/ReCaptcha.vue`. For the purpose of switching between the
development and production keys, the production_builder shell script is
provided. To use it, ensure the lines with the keys keep the comments on the
end, and that 'development' and 'production' appear nowhere else in the
ReCaptcha component.

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
# make sure the ReCaptcha component is using the production key
npm run build
# or instead, run production_builder to automatically swap the keys

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
