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

### User.jsx

```jsx
import { useEffect, useState } from "react";

  

function Users() {

const [users, setUsers] = useState([]);

useEffect(() => {

	fetch("https://jsonplaceholder.typicode.com/users")
	
	.then((res) => res.json())
	
	.then((data) => setUsers(data));

}, []);

return (

	<div>
	
		{users.map((user, index) => {
		
			return (
			
				<div key={index}>
				
					<h1>
					
						{user.id},{user.name},{user.address.street}
					
					</h1>
				
				</div>
			
			);
		
		})}
	
	</div>

);

}

  

export default Users;
```