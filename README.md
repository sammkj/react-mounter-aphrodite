# React Mounter Aphrodite

React Mounter Aphrodite lets you mount React components to DOM easily with Aphrodite.

> React Mounter Aphrodite supports Server Side Rendering when used with [FlowRouter](https://github.com/kadirahq/flow-router).
> If you're not using Aphrodite, use react-mounter instead.

React Mounter Aphrodite can work as a simple Layout Manager where you can use with [Flow Router](https://github.com/kadirahq/flow-router).

## Basic Usage

Install with:

```
npm i --save react-mounter-aphrodite react react-dom aphrodite
```

> `aphrodite`, `react` and `react-dom` are peerDependencies of `react-mounter-aphrodite`. So, you need to install them into your app manually.

Create a component with styles:

```
import React, { PropTypes } from 'react';
import { StyleSheet, css } from 'aphrodite';

const styles = StyleSheet.create({
  red: {
    backgroundColor: 'red',
    height: '300px',
    '@media (min-width: 400px)': {
      backgroundColor: 'blue',
    },
  },
  random: {
    backgroundColor: 'blue',
  },
});

const Hello = ({ name }) => (
  <div className={css(styles.red)}>
    <div className={css(styles.random)}>hello {name()}</div>
  </div>
);

```

Rehyrate style tag on client-side (if you use SSR)

```
if (Meteor.isClient) {
  StyleSheet.rehydrate(window.renderedClasses);
}
```

Mount the component.

```
import React from 'react';
import Hello from '../hello';
import { mount } from 'react-mounter';

mount(Hello, { name: 'Sam' });
```

## Configure Root DOM node

By default React Mounter render our components into a DOM node called `react-root`. But, you can configure if by like below:

```js
const {mount, withOptions} from `react-mounter`;
const mount2 = withOptions({
    rootId: 'the-root',
    rootProps: {'className': 'some-class-name'}
}, mount);

mount2(WelcomeComponent, {name: 'Arunoda'});
```

## Server Side Rendering (SSR)

SSR is supported when used with [FlowRouter SSR](https://github.com/kadirahq/flow-router/tree/ssr). Checkout this [sample app](https://github.com/kadira-samples/meteor-data-and-react).
