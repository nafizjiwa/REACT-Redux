# REDUX CORE CONCEPT
- Redux, a Library to manage state with tools to update state through the STORE.
- The state object (initialState) and the state management logic (stateReducer)
- Actions trigger the reducer function and then change state
#### Apps have 3 parts
- State - apps current data
- View - for user
- Actions - events to change state
#### In React Components, these part overlap. Render and mange state

#### Redux separates all 3
A views components request state changes using actions
### **1. STATE - SET OF DATA NEEDED BY OR DESCRIBES AN APPLICATION
- State values - any js type: string, boolean, array, object;

      const initialApplicationState = [ 'array', 'of', 'Strings', 'Values' ];
### **2. 'ACTIONS' ARE JS OBJECTS they TRIGGER A STATE CHANGE 
- Actions are events with info about how to update state
- Action trggered by UI to change state
- Actions are dispatched to notify parts of an app.

      const addNewSong = {      ACTION OBJECT NAME
         type: 'songs/addSong',    TYPE --> DESCRIBES THE type of ACTION
         payload: 'Halo'        PAYLOAD --> INFO ABOUT ACTION
       };
  
       const removeAll = {    NOT ALL ACTIONS REQUIRE PAYLOAD
         type: 'songs/removeAll'   
       }

### **3. REDUCERS Carry out the changes to the state
 - JS functions: Accept the state and action object as arguments, and returns the next state
 - They define how to create the new state</br>
 
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
