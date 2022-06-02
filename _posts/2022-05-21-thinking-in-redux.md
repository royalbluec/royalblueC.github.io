---
title: Thinking In Redux
author: royalblueC
date: 2022-05-21 09:00:00 -0500
categories: [Frontend]
tags: [Redux]
---

# Three Principles

## Single source of truth

The **global state** of your application is stored in an object tree within a single **store**

## State is read-only

The only way to change the state is to emit an **action**, an object describing what happe

## Changes are made with pure functions

To specify how the state tree is transformed by actions, you write pure **reducers.**

# Glossary

## Action

An action is a plain object that representan intention to change the state. Actions are the only way to get data into the store

## Reducer

A reducer (also called a reducing function) is a function that accepts an accumulation and value and returns a new accumulation. They are used to reduce a collection of values down to single value.

## Dispatching Function

A dispatching function (or simply dispatch function) is a function that accepts an action or an async action. it then may or may not dispatch one or more actions to the store.

The base dispatch function always synchronously sends an action to the store's reducer, along with the previous state returned by the store, to calculate a new state. It expects actions to be plain objects ready to be consumed by the reducer.

## Action Creator

An action creator is, quite simply, a function that creates an action.

## Store

A store is an object that holds the application's state tree. There should only be a single store in a Redux app, as the composition happens on the reducer level
