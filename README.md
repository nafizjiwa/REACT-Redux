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
 - Are JS functions: Accept the state and action object as arguments, and returns the next state
 
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
Pure functions always have the same outputs given the same inputs.</br>
 `Redux manages and upates state with redux Actions`</br>
 'Actions describe an occuring event and provide info about what needs to be updated in state'</br>
 
 ### **Immutable Updates and Pure Functions
 #### Immutable - No changes to original argument
 #### Pure Functions - Return the same outputs given the same inputs
            -------------------------------------------------------------
            import React from 'react';
            //Modify mutable function to immutable
            // export const removeItemAtIndex = (list, index) => {
                  //  list.splice(index, 1);   //MUTABLE
                  //  return list; 
            // };
            export const removeItemAtIndex = (list, index) => {
              return [
                 ...list.slice(0, index),          //IMMUTABLE
                ...list.slice(index + 1, list.length)
              ]; 
            };
            --------------------------------------------------------------
            //Modify impure function to Pure Function
            // export const generateUniqueId = () => {
            //         const timestamp = Date.now();
            //         const random = Math.floor(Math.random() * 1000);
            //   return timestamp + random;
            // };
            //Make function Pure by removing function outside
            export const generateUniqueId = (timestamp, random) => {
              return timestamp + random;      //PURE FUNCTION
            };
            const App = () => {
              const result = removeItemAtIndex(['a', 'b', 'c', 'd'], 1);
              //Make function calls here
              const timestamp = Date.now();
              const random = Math.floor(Math.random() * 1000);
              //Then call pure funciton hence output same everytime input is same
              const uniqueId = generateUniqueId(timestamp, random);
            -----------------------------------------------------------------
              //Don't touch the content below this!
              return (
                <div>
                  <h1>Remove Item at Index</h1>
                  <p>Output: {result.join(', ')}</p>
                  <h1>Unique ID:</h1>
                  <p>Output: {uniqueId}</p>
                </div>
              );
            };
            
            export default App;
### **4. STORE (single source of truth)

      - Contains the reducer and state, it provides a way to dispatch actions,
      - An action is dispatched to the store which calls the reducer 9it needs the action and current state).
      
#### DESCRIBE THE ONE-WAY DATA FLOW BETWEEN STATE, ACTIONS, AND REDUCERS
      = from state to view to action back to state
`1. The STORE initializes the state with a default value.`</br>
`2. The VIEW displays that state to the user.`</br>
`3. The USER INTERACTS WITH THE VIEW, such as clicking a button, an ACTION DISPATCHED to the store.`</br>
`4. The STORE'S REDUCER combines the dispatched action and the current state to DETERMINE THE NEXT STATE.`</br>
`5. The VIEW IS UPDATED to display the new state to the user.`</br>

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
