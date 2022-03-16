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

- If you want a diffrent style for a indivual page add this logic at the bottom

``` _app.js```

```
import "../styles/globals.css";
import Footer from "../components/Footer";
import Header from "../components/Header";
function MyApp({ Component, pageProps }) {
  if (Component.getLayout) {
    return Component.getLayout(<Component {...pageProps} />);
  }
  return (
    <>
      <Header />
      <Component {...pageProps} />
      <Footer />
    </>
  );
}

export default MyApp;

```


```
import React from "react";
import Footer from "../components/Footer";

const about = () => {
  return <div>about</div>;
};

export default about;

about.getLayout = function PageLayout(page) {
  return (
    <>
      {page}
      <Footer />
    </>
  );
};

```
