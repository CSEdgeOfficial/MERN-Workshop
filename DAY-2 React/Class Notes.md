Simple count app
```jsx
import { useState } from "react";

  
function App() {

	const [count, setCount] = useState(0);

	return (

		<>

			<h1>Hello World</h1>

			<div>

				<p className="text-6xl">{count}</p>
	
				<button
	
				onClick={() => {
				
				setCount(count + 1);
				
				}}
	
				className="px-2 py-1 bg-gray-400 rounded-lg"			
				>
				
				Increment count
				
				</button>
				
				<button
				
				onClick={() => {
				
				setCount(count - 1);
				
				}}
				
				className="px-2 py-1 bg-gray-400 rounded-lg"
				>
				Decrement count
				</button>

			</div>

		</>

	);

}

  

export default App;
```