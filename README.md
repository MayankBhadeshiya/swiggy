# swiggy

# Folder Structure

->redux
	->example
		-exampleTypes.js
			export the different types so that we don’t face spalling mistakes.
			ex:-
			export const Show_example = ‘Show_example’;

		-exampleActions.js
			import the types and then define the function for every action and export that functions
			ex:-
			import {Show_example} from ‘./exampleTypes’
			export const show = () => {
				return {
					type: Show_example
				}
			}
		-exampleReducer.js
			import the types and then create initialState and then reducer function
			ex:-
			import {Show_example} from ‘./exampleTypes’
			const initialState = {isShow:false}
			const exampleReducer = (state = initialState, action) => {
				switch(action.type) {
					case Show_example: return {…state, isShow:true}
					default: return state
				}
			}
			export default exampleReducer

	-index.js
		export function which is created in the exampleActions.js
		ex:-
		export {show} from ‘./example/exampleActions’

	-rootReducer.js
		import {combineReducers} from ‘redux’
		import exampleReducer from ‘./example/exampleReducer’ 
		const rootReducer = combineReducers({
			example : exampleReducer,
		})
		export default rootReducer.
	-store.js
		import {createStrore} from ‘redux’;		(if you get error in above line use this :- import { legacy_createStore as createStore} from 'redux';)
		import rootReducer From ‘./rootRducer’;
		const strore = createStrore(rootReducer)
		export default store 
    
   # Steps to follow

-> Install the redux and react-redux packages.

-> First of all create all the file maintain in the folder structure
And then provide the store to the app by going to the App.js or Index.js File

-> Import following:

Import { Provider } from ’react-redux’;
Import store from ‘./redux/store’;

-> Then Wrap the app div with this code:

<Provider store={store}>
	<>
</ Provider>

-> Now in the project when ever you want to use any state in any file just follow this: (follow the example which is given in folder structure)

Import { useSelector } from ‘react-redux’;

Const isShow = useSelector(state => state.example.isShow)

-> Now if you want to dispatch any action then do this (follow the example which is given in folder structure)

Import { useDispatch } from ‘react-redux’;
Import {show} from ‘../redux’;  

and then in function component 

Const dispatch = useDispatch()

<button onClick={() => dispatch(show()) }></button>
  
  
  
  
  
  
  
  # Folder Structure (Redux Toolkit)

->redux
	-example.js

		first import createSlice and then create slice like below:-

		import { createSlice } from '@reduxjs/toolkit';
		const initialExampleState = { counter: 0, showCounter: true };
		const exampleSlice = createSlice({
  			name: ‘Example’,
  			initialState: initialCounterState,
  			reducers: {
    				increment(state) {
      					state.counter++;
    				},
   				 decrement(state) {
    					state.counter--;
    				},
    				increase(state, action) {
      					state.counter = state.counter + action.payload;
   				},
    				toggleCounter(state) {
      					state.showCounter = !state.showCounter;
    				},
  			},
		});
		export const exampleActions = exampleSlice.actions;
		export default exampleSlice.reducer;

	-store.js

		import { configureStore } from '@reduxjs/toolkit';
		import exampleReducer from './example';
		const store = configureStore({
  			reducer: { example: exampleReducer},
		});
		export default store; 
  
 # Steps to follow (Redux Toolkit);

-> Install the ReduxToolkit and react-redux packages.

-> First of all create all the file maintain in the folder structure
And then provide the store to the app by going to the App.js or Index.js File

-> Import following:

Import { Provider } from ’react-redux’;
Import store from ‘./redux/store’;

-> Then Wrap the app div with this code:

<Provider store={store}>
	<>
</ Provider>

-> Now in the project when ever you want to use any state in any file just follow this:

Import { useSelector } from ‘react-redux’;

Const Example = useSelector(state => state.example.counter) (as per example shown in folder Structure)

-> Now if you want to dispatch any action then do this

Import { useDispatch } from ‘react-redux’;
Import {exampleActions} from ‘../redux/example’;

and then in function component 

Const dispatch = useDispatch()

<button onClick={() => dispatch(exampleActions.increment()) }></button>
