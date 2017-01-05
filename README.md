<h1 align="center">
  Vue Google Tag Manager
  <br>
  <br>
</h1>

<h4 align="center">Simple implementation of Google Tag Manager in Vue.js</h4>

<p align="center">
  <a href="https://github.com/feross/standard"><img src="https://cdn.rawgit.com/feross/standard/master/badge.svg" alt="Standard - JavaScript Style Guide"></a>
</p>
<br>

This plugin will helps you in your common GTM tasks.

# Requirements

- **Vue.js.** >= 2.0.0
- **Google Tag Manager account.** To send data to

**Optionnals dependencies**

- **Vue Router** >= 2.x - In order to use auto-tracking of screens


# Configuration

`npm install vue-gtm -S` or `yarn add vue-ua` if you use [Yarn package manager](https://yarnpkg.com/)

Here is an example of configuration, compose with it on your own :

```javascript
import VueGtm from 'vue-gtm'
import VueRouter from 'vue-router'
const router = new VueRouter({routes, mode, linkActiveClass})

Vue.use(VueGtm, {
  debug: true, // Whether or not display console logs debugs (optional)
  vueRouter: router, // Pass the router instance to automatically sync with router (optional)
  ignoredViews: ['homepage'], // If router, you can exclude some routes name (case insensitive) (optional)
})
```

# Documentation

Once the configuration is completed, you can access vue gtm instance in your components like that :

```javascript
export default {
    name: 'MyComponent',
    data () {
      return {
        someData: false
      }
    },
    methods: {
      onClick: function() {
        this.$gtm.trackEvent({
					category: 'Calculator',
					action: 'click',
					label: 'Home page SIP calculator',
					value: 5000
				});
      }
    },
    mounted () {
      this.$ua.trackView('MyScreenName', 'currentpath');
    }
}
```

You can also access the instance anywhere whenever you imported `Vue` by using `Vue.gtm`. It is especially useful when you are in a store module or
somewhere else than a component's scope.

## Sync gtm with your router

Thanks to vue-router guards, you can automatically dispatch new screen views on router change !
To use this feature, you just need to inject the router instance on plugin initialization.

This feature will generate the view name according to a priority rule :
- If you defined a meta field for you route named `gtm` this will take the value of this field for the view name.
- Otherwise, if the plugin don't have a value for the `meta.gtm` it will fallback to the internal route name.

Most of time the second case is enough, but sometimes you want to have more control on what is sent, this is where the first rule shine.

Example : 
```javascript
const myRoute = {
  path: 'myRoute',
  name: 'MyRouteName',
  component: SomeComponent,
  meta: {gtm: 'MyCustomValue'}
}
```

> This will use `MyCustomValue` as the view name.

## Credits
[ScreamZ vue-analytics](https://github.com/ScreamZ/vue-analytics)