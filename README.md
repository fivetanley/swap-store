Swap Store
============

The Swap Store allows you to use two different adapters in conjunction with
each other.

For instance: Say you want to use Ryan Florence's
[localStorage adapter][ls-adapter] with Ember Data's [RESTAdapter][rest-adapter].

You might want to use the localStorage adapter as a cache, but need to be able
to tell the server of changes to data you've made, and use the server to keep
the cache in sync.

## Example Usage

You can use the `SwapAdapter` by setting it as your store in your application's
initial code:

```javascript
App.Store = DS.SwapStore.extend({
  primaryAdapter:   DS.LSAdapter,
  secondaryAdapter: DS.RESTAdapter
});
```

The `primaryAdapter` is the adapter that is **written** and **read from first**.
This means when you do `App.MyModel.find()`, it will ask the `primaryAdapter`
for the data first, and, if that fails, go to the `secondaryAdapter` to read
or write data.

## TODO

* Data conflicts between cache / server (need mode for simply deciding which
one should be considered "correct", need advanced mode for more fine-grained
control for handling conflicts).
* Need option for deciding how often to sync the stores.


[ls-adapter]: https://github.com/rpflorence/ember-localstorage-adapter
[rest-adapter]: http://emberjs.com/guides/models/the-rest-adapter
