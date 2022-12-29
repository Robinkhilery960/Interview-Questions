## React interview Questions

## 1. What is React:
1. React is a javascript library used for building user interfaces.
### Cross Questions:
    1. What is UI?
    
## 2. Framework vs library:
Both libraries and frameworks are reusable code written by someone else which helps developer to solve their problem. Library are like you are making your house from the scratch while framework is like you are buying a new house , what does I mean here is that  when you are using library then  you are the one who decides that when to call you library code and when to use it in your code but in  case of your framework it is the framework that decides that when your code will be called and where you code should be placed. In other word I can say that it is inversion of control that makes difference between library and framework.

## 3.What are major features of the react?
1. React uses virtual DOM 

## 4. What is  DOM and Virtual DOM ?
Virtual DOM is a lightweight copy of the actual DOM which don't have the power to directly manipulate the DOM.Updating the virtual DOM is cheaper as compared to the actual DOM. 
Whenever there is a change in the UI at that time your virtual dom is get updated and compared to the previous version of the virtual dom and then it s updated to the actual DOM using some diffing algorithm.
You don not directly deal with the DOM you tells the react and react does it for you . Every component have a jsx structure and this jsx structure is nothing more but html like structure  so for every component that will be  a DOM for it , so for this there will a copy  a virtual dom in  memory is created , if any element in te virtual dom get updated then still dom is not going to directly update the virtual dom instead of that this dom is going to create a new virtual dom for you with updated , now react will do a diff between the current virtual  dom  and the last one  to identify that what actually has been changed, so make some update to the original n based to that so that change get reflected. but is it going to updated directly just after second update no , there is something called as batch update, on batch basis they will be done on  basis of react algo , 
reconciliation is the process in  which it is decided that what parts is needed to change and then update the Original DOM.
Diffing algo:
1. When the root got changed then entire tree will be build again 
2. Change in attribute- no tear down happen inly that portion reflected

## What is CDN?