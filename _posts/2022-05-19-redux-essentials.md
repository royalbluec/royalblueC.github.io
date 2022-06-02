---
title: Redux Essentials
author: royalblueC
date: 2022-05-19 09:00:00 -0500
categories: [Frontend]
tags: [Redux]
---

# Redux Overview and Concepts

## What is Redux?

**Redux is pattern and library for managing and updating application state, using events called "actions".** It serves as a centralized store for state that needs to be used across your entire application, with rules ensuring that the state can only be updated in a predictable fashion.

### Why Should I Use Redux?

Redux helps you manage "global" state - state that is needed across many parts of your application

**The patterns and tools provided by Redux make it easier to understand when, where, why, and how the state in your application is being updated, and how your application logic will behave when those changes occur.** Redux guides you towards writing code that is predictable and testable, which helps give you confidence that your application will work as expected.

### When Should I Use Redux?

- You have large amounts of application state that are needed in many places in the app
- The app state is updated frequently over time
- The logic to update that state may be complex
- The app has a medium or large-sized codebase, and might be worked on by many people

## Terminology

### Actions

An **action** is a plain JavaScript object that has a type filed. **You can think of an action as an event that describes something that happened in the application.**

The `type` field should be a string that gives this action a descriptive name. The first part is the feature or category that this action belongs to, and the second part is the specific thing that happened.

An action object can have other fileds with additional information about what happened. By convention, we put that information in a field called `payload`.

### Action Creators

An **action creator** is a function that creates and returns an action object.

### Reducers

A **reducer** is a function that receives the current `state` and an `action` object, decides how to update the state if necessary, and returns the new state. **You can think of a reducer as an event listener which handles events based on the received action type.**

- They should only calculate the new state value based on the `state` and `action` arguments
- They are not allowed to modify the existing `state`. Instead, they must make immutable updates, by copying the existing `state` and making changes to the copied values.
- They must not do any asynchronous logic, calculate random values, or cause other "side effects"

### Store

The current Reudx application state lives in an object called the **store**.

### Dispatch

The only way to update the state is to call **dispatch** and pass in an action object.

### Selectors

**Selectors** are functions that know how to extract specific pieces of information from store state value.
