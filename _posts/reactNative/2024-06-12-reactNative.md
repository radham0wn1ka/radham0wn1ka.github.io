---
layout: post
title:  "react native"
date:   2024-06-12 09:29:20 +0700
categories: react native
usemathjax: true
---
## links
```
https://reactnative.dev/
https://reactnative.dev/docs/getting-started
https://docs.expo.dev/get-started/set-up-your-environment/
```
## contnet
- It provides a core set of platform agnostic native components like View, Text, and Image that map directly to the platform's native UI building blocks.
- n Android and iOS development, a view is the basic building block of UI: a small rectangular element on the screen which can be used to display text, images, or respond to user input
-  Even the smallest visual elements of an app, like a line of text or a button, are kinds of views. Some kinds of views can contain other views. It’s views all the way down!
- Kotlin or Java -andorid
- Swift or Objective-C -ios
- With React Native, you can invoke these views with JavaScript using React components
- At runtime, React Native creates the corresponding Android and iOS views for those components
- Because React Native components are backed by the same views as Android and iOS, React Native apps look, feel, and perform like any other apps. We call these platform-backed components Native Components.
-  Core Components.
- TextInput is a Core Component that allows the user to enter text. It has an onChangeText prop that takes a function to be called every time the text changed, and an onSubmitEditing prop that takes a function to be called when the text is submitted.
- npm run web/android/ios
- npm install expo
- `npx expo start`
- The ScrollView works best to present a small number of things of a limited size. All the elements and views of a ScrollView are rendered, even if they are not currently shown on the screen. If you have a long list of items which cannot fit on the screen, you should use a FlatList instead
- The FlatList component displays a scrolling list of changing, but similarly structured, data. FlatList works well for long lists of data, where the number of items might change over time. Unlike the more generic ScrollView, the FlatList only renders elements that are currently showing on the screen, not all the elements at once.
- The FlatList component requires two props: data and renderItem. data is the source of information for the list. renderItem takes one item from the source and returns a formatted component to render
- stop process at a port `sudo lsof -i :8081` and `kill -9 <PID>`
- use other port `npm start -- --port=8088`
- Platform.os/version
- Platform-specific extensions
```
BigButton.ios.js
BigButton.android.js
import BigButton from './BigButton';
```
```
Container.js # picked up by webpack, Rollup or any other Web bundler
Container.native.js # picked up by the React Native bundler for both Android and iOS (Metro)

import Container from './Container';
```
- Pro tip: Configure your Web bundler to ignore .native.js extensions in order to avoid having unused code in your production bundle, thus reducing the final bundle size.
- framework, a toolbox with all the necessary APIs to let you build production ready apps.
- Expo provides features like file-based routing, high-quality universal libraries, and the ability to write plugins that modify native code without having to manage native files
- The React Native community has spent years refining approaches to navigation, accessing native APIs, dealing with native dependencies, and more. Most apps need these core features. A React Native Framework provides them from the start of your app.
- If your app has unusual constraints that are not served well by a Framework, or you prefer to solve these problems yourself, you can make a React Native app without a Framework using Android Studio, Xcod
- Expo is a production-grade React Native Framework. Expo provides developer tooling that makes developing apps easier, such as file-based routing, a standard library of native modules, and much more.
- Expo Application Services (EAS), an optional set of services that complements Expo, the Framework, in each step of the development process.
- Watchman is a tool by Facebook for watching changes in the filesystem. It is highly recommended you install it for better performance and increased compatibility in certain edge cases
- React Native uses Metro to build your JavaScript code and assets.
- In React Native, your Metro config should extend either @react-native/metro-config or @expo/metro-config. These packages contain essential defaults necessary to build and run React Native apps
- The terms "library" and "package" are used interchangeably in the JavaScript community.
- TypeScript is a language which extends JavaScript by adding type definitions. New React Native projects target TypeScript by default, but also support JavaScript and Flow
- New projects created by the React Native CLI or popular templates like Ignite will use TypeScript by defaul
- With React Native, you style your application using JavaScript. All of the core components accept a prop named style. The style names and values usually match how CSS works on the web, except names are written using camel casing, e.g. backgroundColor rather than background-color
- as  a component grows in complexity, it is often cleaner to use StyleSheet.create to define several styles in one place
- e flex in a component's style to have the component expand and shrink dynamically based on available space. Normally you will use flex: 1, which tells a component to fill all available space, shared evenly amongst other components with the same parent. The larger the flex given, the higher the ratio of space a component will take compared to its siblings.
- `A component can only expand to fill available space if its parent has dimensions greater than 0. If a parent does not have either a fixed width and height or flex, the parent will have dimensions of 0 and the flex children will not be visible.`
- https://reactnative.dev/docs/height-and-width
- You will normally use a combination of flexDirection, alignItems, and justifyContent to achieve the right layout.
- Flexbox works the same way in React Native as it does in CSS on the web, with a few exceptions. The defaults are different, with flexDirection defaulting to column instead of row, alignContent defaulting to flex-start instead of stretch, flexShrink defaulting to 0 instead of 1, the flex parameter only supporting a single number
- flex will define how your items are going to “fill” over the available space along your main axis. Space will be divided according to each element's flex property.
- flex direction :column (default value) Align children from top to bottom. If wrapping is enabled, then the next line will start to the right of the first item on the top of the container
- Layout Direction
### justify contnet
```
justifyContent describes how to align children within the main axis of their container. For example, you can use this property to center a child horizontally within a container with flexDirection set to row or vertically within a container with flexDirection set to column.
    flex-start(default value) Align children of a container to the start of the container's main axis.
    flex-end Align children of a container to the end of the container's main axis.
    center Align children of a container in the center of the container's main axis.
    space-between Evenly space off children across the container's main axis, distributing the remaining space between the children.
    space-around Evenly space off children across the container's main axis, distributing the remaining space around the children. Compared to space-between, using space-around will result in space being distributed to the beginning of the first child and end of the last child.
    space-evenly Evenly distribute children within the alignment container along the main axis. The spacing between each pair of adjacent items, the main-start edge and the first item, and the main-end edge and the last item, are all exactly the same.
```
- align items align self