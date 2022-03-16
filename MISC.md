# summary 

- [APP Layout](#APP-Layout)



# APP Layout 
- This will give your application a re-uable layout to be simply put in every page

## How to make a layout 

- Make a component for a ```Header```

```
import React from 'react'

const Header = () => {
  return (
    <div>Header</div>
  )
}

export default Header
```

- Make a ```Footer``` components

```
import React from 'react'

const Footer = () => {
  return (
    <div>Footer</div>
  )
}

export default Footer
```

- Now you have made you layoput for your app go to ```_app.js``` and add 

```
import '../styles/globals.css'
import Footer from "../components/Footer"
import Header from "../components/Header"
function MyApp({ Component, pageProps }) {
  return (
    <>
      <Header />
      <Component {...pageProps} />
      <Footer />
    </>
  );
}

export default MyApp

```
