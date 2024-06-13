---
layout: post
title:  "type script"
date:   2024-06-13 09:29:20 +0700
categories: type script
usemathjax: true
---
## ref
- https://code.visualstudio.com/docs/editor/debugging#_debug-actions
- https://www.youtube.com/watch?v=d56mG7DezGs
## env
- `tsc -v`:type script compiler
- `npm install -g typescript`
- let age: number=10
- annotatage age with number
- on doing tsc ts1.ts a ts1.js is made
- for `let age:number=2`=>`var age = 2;`
- usually tsc convets to old js,to use new js change the targe in below file
- `tsc --init`=>creates tsconfig.json
- we have contorl over source files and where generated destination files will  be by changing tsconfig.json
- like this if we have a folder then to run ts files we can just `tsc` which will compile all ts files
- in vs code we have in debug panel ,a create launch.json file,it tells vs code how to debug this app
- declared uninilized variables are of type `any`
- with this we can do
```
let a;
a=10
a="abcd"
function t(a){//implicity any gives err
    console.log(a)
}
let aray1:number[]=[1,2]
```
- in some cases  implicit any returns err,to turn it off change change tsconfig.ts
- tuples type in ts:
```
let student:[number,string]=[191034,"mounika"]
```
- enum Color={"red","blue","green"};let x:C0lor=Color.red
- for functions
```
function voteEligibility(age:number):boolean{
    ...
    return false    
}
```