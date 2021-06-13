# **What is the most clean way to implement your CSS styles in React**

## **Styling in React**

There are countless ways to implement styling in React. Because it is a 'platform' that runs entirely on JavaScript, the way of styling does not matter. This can be vanilla CSS, SCSS/SASS, LESS, Bootstrap, Tailwind-CSS or whatever. There are several cons of using these options. When you’re using vanilla CSS you have to manually put a specific class name on each HTML element, or in SCSS/SASS on the parent of the relevant component. Hoping you haven't even used this name before.

When you’re working with a component based design system, such as Atomic Webdesign, you want to code reusable components. However, the styling of this can sometimes be different. For example, you don't want to write the same button component three times, but you want to adjust the styling on the basis of a property.

## **Why styled-components?**

**Styled-components** is perfect for component based coding. It has been developed specifically for React, and has an easy learning curve. It is intended to write within the same JavaScript file, but also possible to import a file with styles. By writing your styles on this way, it makes your code much simpler and clear. For example, it is not necessary to manually assign a class name to every HTML element, and you can write the code in a SCSS/SASS way.

### **How to get started?**

To get started with styled components, you only need to perform two steps:

1. Install package to your dependencies with the following NPM command:

   - _npm install -save styled-components_

2. Start using it with opening up a component and import the package
   - _import styled from 'styled-components'_

It was that easy! Now it's just a matter of getting started adding the styling. Write code!

### **How does it look?**

You can use it in several ways. For example, it is an option to write the styling within your component, although this file can already become quite large if a lot of code is involved. This makes exporting the file a neater solution. Below are two examples of how you can implement **styled-components** within your React component.

#### **Styling inside your component**

By rendering the styling inside your React component, everything is in one place. Because there is only one html element within this file, it is still clear. This would be a lot less if there are about 5 to 6 elements, including styling.

```javascript
// React components & imports
import React from 'react'
import styled from 'styled-components'

const Button = styled.div`
   	display: block;
	width: ${(props) => props.width || '284px'};
	max-height: 48px;
	font-weight: 700;
	text-align: center;
	padding: 0.75em 0;
	background-color: yellow;
	border: 0.15em solid black;
	color: black;
	transition: 0.2s;
	&:hover {
		cursor: pointer;
		opacity: 0.7;
	}
	&[disabled] {
		opacity: 0.4;
	}
`

// Component
const ButtonPrimary = ({ type, text, linkTo, width, _callback, height, id, disabled }) => {
		return (
			<Button onClick={_callback}	disabled={disabled} >
				{text}
			</Button>
		)
	}
}

export default ButtonPrimary

```

_button.jsx_

#### **External styling**

By separating the styling and component, the file becomes much clearer. When multiple child elements are present, this can also be styled in a well-arranged way, in the SASS/SCSS way. As a result, you often only need to create one styled component. By importing all elements from a file with an alias, you are obliged to prefix Styles here. This also makes it immediately clear that it is a styled-component.

```javascript
// React components & imports
import React from 'react'
import * as Styles from './buttonPrimary.styles.js'


// Component
const ButtonPrimary = ({ type, text, linkTo, width, _callback, height, id, disabled }) => {
		return (
			<Styles. Button onClick={_callback} disabled={disabled} >
				{text}
			</Styles.Button>
		)
	}
}

export default ButtonPrimary

```

_button.jsx_

```js
import styled from 'styled-components';
import * as colors from 'styles/colors';

export const Button = styled.div`
  display: block;
  width: ${(props) => props.width || '284px'};
  max-height: 48px;
  font-weight: 700;
  text-align: center;
  padding: 0.75em 0;
  background-color: yellow;
  border: 0.15em solid black;
  color: black;
  transition: 0.2s;
  &:hover {
    cursor: pointer;
    opacity: 0.7;
  }
  &[disabled] {
    opacity: 0.4;
  }
`;
```

_button.styling.js_

```other
button/
+-- button.jsx
+-- button.styles.js
```

_Folder structure_
