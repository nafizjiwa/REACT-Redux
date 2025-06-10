# REACT-Redux

### **1. State Defined
      const initialState = [ 'Take Five', 'Claire de Lune', 'Respect' ];
### **2. 'ACTIONS' are a request to change the state 
      const addNewSong = {
         type: 'songs/addSong',
         payload: 'Halo'
       };
       const removeSong = {
         type: 'songs/removeSong',
         payload: 'Take Five'
       };
       const removeAll = {
         type: 'songs/removeAll'
       }

### **3. Reducers Carry out the changes to the state
 Are JS functions: Define how the current state and action are converted to a new state</br>
 
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
Reducer functions make immutable update to arguments by creating a copy and modifing that copy.</br>
Pure functions always have the same outputs given the same inputs.</br>
 `Redux manages and upates state with redux Actions`</br>
 `Actions in Redux are JS Objects`</br>
 'Actions describe an occuring event and provide info about what needs to be updated in state'</br>
 ### Actions Syntax
 
     const actionIsAnObject = {
         type: 'actionTypeAsAString', //What are we doing -type of action
         payload: 'addtional info about how to perform the action' // What are we doing it to 
       }   
 ### Immutable Updates and Pure Functions
 #### Immutable - no changes to original argument
 #### Pure Functions - always the same outputs given the same inputs
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
            
            export const generateUniqueId = (timestamp, random) => {
              return timestamp + random;      //PURE FUNCTION
            };
            const App = () => {
              const result = removeItemAtIndex(['a', 'b', 'c', 'd'], 1);
              //Make function calls here
              const timestamp = Date.now();
              const random = Math.floor(Math.random() * 1000);
              
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
