## Extending Axios

If you need to customize axios by registering interceptors and changing global config, you have to create a nuxt plugin.

**nuxt.config.js**

```js
{
  modules: [
    '@nuxtjs/axios',
  ],

  plugins: [
    '~/plugins/axios'
  ]
}
```

**plugins/axios.js**

```js
export default function ({ $axios, redirect }) {
  $axios.onRequest(config => {
    console.log('Making request to ' + config.url)
  })

  $axios.onError(error => {
    const code = parseInt(error.response && error.response.status)
    if (code === 400) {
      redirect('/400')
    }
  })
}
```
