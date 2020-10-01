---
layout: post
title:      "Making a the event of a button scroll to an html element with React"
date:       2020-10-01 22:23:25 +0000
permalink:  making_a_the_event_of_a_button_scroll_to_an_html_element_with_react
---


I'm going to show you how to make the onClick event of a button scroll down to an especific html element. This is actually surprisingly easy, it only takes about ten minutes at most. 

**1. Import useRef from react and create a variable for reference**

```
import React, { useRef } from 'react';

const HomePage = (props) => {
    const section = useRef(null);
		
		....
}
```
Import useRef so we can have acces to the function useRef().

**2. Place that variable in a html tag**

```
	  	...
		  <div ref={section}>
			....
			</div>
			...
}
```

This is the desired tag you want to scroll to.

**3. Write the function for the event**

```
const goToSection = () => window.scrollTo({ 
        top: section.current.offsetTop - 50,
        behavior: "smooth"
        })
```

`window.scrollTo()` accepts an object with two keys: `top: ` which recieves an integer so you can add or subtract from it depending on where extactly you want to scroll. and `behavior` which is just a string that tells it the behavior of scroll.

**4. Create a button and give it onClick event**

```

	  	...
		  <button onClick={goToSection}> 
			 Go to section
			</button>
			...
```

**The result should look something like this:**

```
import React, { useRef } from 'react';
​
const HomePage = (props) => {
    const section = useRef(null);
		
const goToSection = () => window.scrollTo({ 
        top: section.current.offsetTop - 50,
        behavior: "smooth"
        });
    ....
	return (
	     ...
			 <button onClick={goToSection}> 
			 Go to section
			</button>
			...
			<div ref={section}>
			Section
			</div>
			...
	)
}
```

That's it! Super easy and fast to implement.






