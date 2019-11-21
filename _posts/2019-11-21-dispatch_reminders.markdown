---
layout: post
title:      "Dispatch Reminders"
date:       2019-11-21 20:00:56 +0000
permalink:  dispatch_reminders
---


Understanding the importance and function of `mapDispatchToProps` is essential to utilizing Redux effectively within a project. Although it is possible to have components that only utilize `mapStateToProps` to extract data from the store, it is by dispatching actions that a user becomes able to alter the state within the Redux store. The `mapDispatchToProps` function is the second argument that is passed into the `connect()` function, which allows specific React components to connect to the Redux store.

Although a user does not need to specify a second parameter within the `connect()` function, a connected component will receive the ability to access `this.props.dispatch` by default. When the `mapStateToProps` parameter is indeed declared, connect will conventionally accept either objects or functions that return objects. This parameter is often declared using object shorthand (which I utilized within my portfolio project) where the logic is imported in the form of action creator functions:

![](https://i.imgur.com/3cxywS8.png)

In the above component of my project, the `mapStateToProps` function connects to the Redux store and makes `state.user` available to the component as `this.props.user`. Both importing my action creator functions and then calling them under the `mapDispatchToProps` parameter similarly makes those functions available as props within the component. More importantly, however, is that it allows the action objects that these functions return to modify the state within the Redux store. In my project, these functions edit the store to disable individual buttons after being clicked or create Book and Purchase objects in my Rails backend.

This functionality is perhaps the most important reason to use Redux within a project. Being able to dispatch state modifications to the store allows a user to asynchronously interact with an API backend and then dynamically render that data within an application. This control flow helps to create fluid, responsive programs, rather than forcing full page reloads or route redirects to show the results of a user's actions. 
