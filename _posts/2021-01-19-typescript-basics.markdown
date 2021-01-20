---
layout: post
title:      "TypeScript Basics"
date:       2021-01-19 21:41:00 +0000
permalink:  typescript_basics
categories: tools
tags: typescript
# image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
# image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG
---

## TypeScript Basics

Another technology that is commonly brought up now: TypeScript. What is TypeScipt? Typescript is a typed superset of JavaScript. When a language is a superset of another language, it means that any JavaScript code is also valid TypeScript. TypeScript does not alter JavaScript but it expands new and valuable features. 

So how does TypeScript improve JavaScript? 

> TypeScript extends JavaScript by adding types. By understanding JavaScript, TypeScript saves you time catching errors and providing fixes before you run code.

The goal of TypeScript is to make JavaScript development more efficient by catching early mistakes through a "type system". What TypeScript does is that it strictly defines what a given variable can contain. It's an additional layer of protection for your project and this is done by introducing constraints that makes it harder to create bugs. This is essential when it comes to large codebases that are maintained by many developers.

For example, with JavaScript we can declare the following variables:

```
let name = 'Yvonne',
age = 28;
```

This is dynamically typed and this could introduce errors later on into our project because the variable, name, could be cast as a number, boolean, or any other type. A dynamically typed language means that the types and datatype errors are spotted only at runtime. 

With TypeScript, however, that could be fixed.

```
let name: string = 'Yvonne',
age: number = 28;
```

This is static typed and the name, in this case, would always be a string. 

> The compiler alerts developers to type-related mistakes, so they have no opportunity to hit the production phase. This results in less error-prone code and better performance during execution.

Hope this helps,
Yvonne