## Functional Component

#### Defining props, setting default value for props, enforce type for the props & make prop mandatory

```js
import React from 'react'
import PropTypes from 'prop-types'

const Header = ({title, description}) => {
    return (
        <>
            <h1>{title}</h1>
            <h2>{description}</h2>
        </>
    )
}

Header.defaultProps = {
    title : "Vicky"
}

Header.propTypes = {
    title : PropTypes.string.isRequired,
    description : PropTypes.string
}
export default Header
```

#### Creating Style in Functional component

```
import React from 'react'
import PropTypes from 'prop-types'

const Header = ({title, description}) => {
    return (
        <>
            <h1 style={{color: "red", backgroundColor: "black"}}>{title}</h1>
            <h2 style={descriptionStyle}>{description}</h2>
        </>
    )
}

Header.defaultProps = {
    title : "Vicky"
}

Header.propTypes = {
    title : PropTypes.string.isRequired,
    description : PropTypes.string
}

const descriptionStyle = {
    color : "red",
    backgroundColor : "black"
}
export default Header
```
