## Props

> 用 Proxy 的 get , set 和 deleteProperty 钩子。

```javascript
// erum.js
export default function enum(object) {
  return new Proxy(object, {
    get(target, prop) {
      if (target[prop]) {
        return Reflect.get(target, prop)
      } else {
        throw new ReferenceError(`Unknown enum '${prop}'`)
      }
    },

    set() {
      throw new TypeError('Enum is readonly')
    },

    deleteProperty() {
      throw new TypeError('Enum is readonly')
    }
  })
}
```