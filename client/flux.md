## Flux
Flux is the application architecture that Facebook uses for building client-side web applications. It makes use of React's composable view components. It's more of a pattern rather than a formal framework.

<br />
#### Overview
Flux application have three major parts: the dispatcher, the stores and the views (React components).

A small subset of the views are called Controller-View. These are views sitting at the top of the hierarchy, who get new data from the stores, update their state with this new data, thus re-rendering themselves and all their component children as they pass part of this new data down to them.

Flux encourages an unidirectional data flow: when a user interacts with a React view, the view propagates an action through a central dispatcher, to the various stores that hold the application's data and business logic, which updates all of the views that are affected.

![alt tag](http://facebook.github.io/flux/img/flux-simple-f8-diagram-with-client-action-1300w.png)

Each store registers their own callbacks to the Dispatcher. When the dispatcher receives an action, it invokes all the store callbacks. The stores then emit a _change_ event to alert all the controller-views that their internal data has changed. Controller-views listen for these events and upon reception they retrieve data from the stores. The controller-views then call their own `setState()`.

<br />
#### Dispatcher
The dispatcher has no business logic. It is just a registry of callbacks into the stores. Each store registers itself and provides a callback. When an action creator provides the dispatcher with a new action, all stores in the application receive the action via the callbacks in the registry.

Dispatchers might become just a bit smarter as the application grows, as they can decide the order in which stores should be notified after an action.

<br />
#### Stores
Stores contain the application state and logic. They do not represent the state of a single object, instead they manage the state of all objects belonging to a particular domain of the application.

A store registers itself with the dispatcher and provides it with a callback. This callback receives the action as a parameter. Within the store's registered callback, a switch statement based on the action's type is used to interpret the action and to provide the proper hooks into the store's internal methods where the state of the store is updated. They then broadcast an event declaring that their state has changed, so the views may query the new state and update themselves.

<br />
#### Views and Controller-Views
When a Controller-View receives the change event from the store, it first requests the new data it needs via the stores' public getter methods. It then calls its own `setState()` or `forceUpdate()` methods, causing its `render()` method and the `render()` method of all its descendants to run.

Controller-Views often pass the entire state of the store down the chain of views in a single object, allowing different descendants to use what they need.

When store data changes, your views shouldn't care if things were added, deleted, or modified. They should just re-render entirely.

<br />
#### Actions
The dispatcher exposes a method that allows us to trigger a dispatch to the stores, and to include a payload of data, which we call an action. The action's creation may be wrapped into a semantic helper method which sends the action to the dispatcher.

Actions may also come from other places, such as the server. This happens, for example, during data initialization. It may also happen when the server returns an error code or when the server has updates to provide to the application.

<br />
#### Resources
http://blog.andrewray.me/flux-for-stupid-people/