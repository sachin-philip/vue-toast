# vue-bulma-toastr

## Setup

Using npm
```bash
npm install  vue-bulma-toastr --save
```
Or using yarn
```bash
yarn add  vue-bulma-toastr
```

## Usage
### Import Component
```javascript
import BulmaToastr from 'vue-bulma-toastr'

Vue.use(BulmaToastr)
```

Optional Global configuration options
```javascript
var toastrConfigs = {
    position: 'top right',
    showDuration: 2000
}
Vue.use(BulmaToastr, toastrConfigs)
```

### Call Notification Instance
```javascript
this.$toast.success({
    message:''
})
```

### type

* `success`
* `info`
* `warning`
* `error`

### position

* `top right`
* `bottom right`
* `bottom left`
* `top left`
* `top center`
* `bottom center`
* `top full width`
* `bottom full width`
