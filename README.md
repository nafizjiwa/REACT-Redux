# REDUX CORE CONCEPT
- Redux, is a Library to manage state with tools to update state through the STORE.
- The state object (initialState) and the state management logic (stateReducer)
- Actions trigger the reducer function and then change state
#### Apps have 3 parts
- State - holds apps current data
- View - displays state to user
- Actions - events to change the state

      Store → View → Actions → Store → View👏
      
      The store informs the view, user interactions trigger actions, actions are
      processed by reducers to update the store, and the updated store triggers
      the view to reflect the changes in the user interface.
#### In React, these part overlap. Components Render interface and Mange state

#### Redux separates all 3
- A views component requests a state change using an action</br>

### **1. STATE - SET OF DATA NEEDED BY OR IT DESCRIBES AN APPLICATION
- State values - any js type: string, boolean, array, object;

      const initialApplicationState = [ 'array', 'of', 'String', 'Values' ];
### **2. 'ACTIONS' ARE JS OBJECTS THEY ARE REQUESTS TO CHANGE THE STATE 
- Actions are
      - events with info about how to update state
      - triggered by UI to change state
      - dispatched to notify parts of an app.
 #### Action Syntax
      const action = {   
        type: 'action type', //a string that specifies the type of action being done.
        payload: 'additional data' //'Optional value' Contains info pn how to perform the operation
      };
--------

      const addNewSong = {      ACTION OBJECT NAME: 'addNewSong'
         type: 'songs/addSong',    TYPE --> DESCRIBES THE type of ACTION
         payload: 'Halo'        PAYLOAD --> INFO ABOUT ACTION
       };
  
       const removeAll = {    AN ACTION WITH NO PAYLOAD
         type: 'songs/removeAll'   
       }

### **3. REDUCERS DEFINE HOW TO CHANGE THE STATE
 - Are JS functions: Accept the state and action object as arguments, and returns the next state</br>

            --SYNTAX--
            const appReducer = (state = initialState, action) => {
                    switch (action.type) {
                      default: {
                        return state;
                           }
                        }
                  }

 ----
       const reducer =  (state = initialState , action) => {
         switch(action.type){
           case 'songs/addSong': {
             return {
               ...state,
               songs: [state.song, action.payload]
               };
           }
           default: {
             return state;
           }
         }
       }
Reducer functions make immutable changes to state by creating a copy and modifing that copy.</br>
`Redux` manages and upates `state` with redux Actions`</br>
'Actions` describe an occuring event and provide info about what state needs updating</br>
 
 ### **3. REDUCERS DO IMMUTABLE UPDATES and THEY ARE PURE FUNCTIONS
 ##### Immutable - When a functions doesn't change the original argument but makes a copy
 ##### Pure Functions - Return the same outputs when given the same inputs
            -------------------------------------------------------------
            import React from 'react';
            //Modify mutable function to immutable
            export const removeItemAtIndex = (list, index) => {
                  list.splice(index, 1);   //MUTABLE
                    return list;             //because splice changes the array
            };
            export const removeItemAtIndex = (list, index) => {
              return [
                 ...list.slice(0, index),          //IMMUTABLE
                ...list.slice(index + 1, list.length) //because slice creates a copy
              ]; 
            };
            --------------------------------------------------------------
            //Modify impure function to Pure Function
            export const generateUniqueId = () => {
                    const timestamp = Date.now();
                     const random = Math.floor(Math.random() * 1000);
              return timestamp + random;
             };
            //Make function Pure by removing functions so they are outside
            export const generateUniqueId = (timestamp, random) => {
              return timestamp + random;      //becomes PURE FUNCTION
            };
            const App = () => {
              //Pure funciton hence output same output everytime input is same
              const uniqueId = generateUniqueId(timestamp, random);
                    return ( some code );
              }
            -----------------------------------------------------------------
             
### **4. STORE (single source of truth `object`
- A container for state
- Dispatches actions
- Triggers the reducer to react to actions
- Actions are dispatched to the store which calls the reducer
- Reducers require an action and current state.
      
#### THE ONE-WAY DATA FLOW BETWEEN STATE, ACTIONS, AND REDUCERS
      `state to view to action back to state`
`1.` The `STORE` initializes` the state with a default value.</br>
`2.` The `VIEW displays` that state to the user.</br>
`3.` The `USER INTERACTS` WITH THE VIEW, such as clicking a button, an ACTION DISPATCHED to the store.`</br>
`4.` The `STORE'S REDUCER combines` dispatched action + current state for `THE NEXT STATE.`</br>
`5.` The `VIEW IS UPDATED` to display the new state to the user.`</br>

User interacts with UI
actions are dispatched in response to a user interaction like a click.
the store runs the reducer function to calculate a new state.
the UI reads the new state to display the new values.

|REVIEW|NOTES|
|----:|:---|
|Redux| library to manage state|
|All states| stored in a single object the STORE|
|REDUX Store [An Object]|Manages State|
|It recieves an Action Objects|--> Executes state changes|
|The state changes based on: |Action Type|
|When change occurs the store calls listener function||
|REDUCERS|Handle actions and update state/data for its slice|
|To create a STORE object Redux uses:| createStore( )|
|createStore(accepts reducer function)| --> Store Object|
|Store Object has 3 methods||
|store.getState( )|retrieves current state|
|store.dipatch(action)|receives action to trigger state change|
|store.subscribe(listener)|these function are called when state changes|
