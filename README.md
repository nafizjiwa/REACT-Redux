# REACT-Redux
- Library to manage and update state through the STORE OBJECT.
- The state object (initialState) and the state management logic (stateReducer)
- Actions trigger the reducer function and then change state
- A dispatched Action --> Describes what to change

### **1. STATE Defined
      const initialState = [ 'Take Five', 'Claire de Lune', 'Respect' ];
### **2. 'ACTIONS' ARE JS OBJECTS they TRIGGER A STATE CHANGE 
      const addNewSong = {
         type: 'songs/addSong',            MUST HAVE TYPE PROP
         payload: 'Halo'
       };
       const removeSong = {
         type: 'songs/removeSong',
         payload: 'Take Five'
       };
       const removeAll = {
         type: 'songs/removeAll'
       }

### **3. REDUCERS Carry out the changes to the state
 - JS functions: They accept state and action object as arguments, and return the next state
 - They define how to convert to a new state</br>
 
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
 ### **Actions Syntax
 
     const actionIsAnObject = {
         type: 'actionTypeAsAString', //What are we doing -type of action
         payload: 'addtional info about how to perform the action' // How are we doing it
       }   
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

      - Contains the reducer and state, it provides a way to dispatch actions, and it calls the reducer when actions are dispatched.</br>
      - An action is dispatched to the store which calls the reducer with the action and current state.</br>
      
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
