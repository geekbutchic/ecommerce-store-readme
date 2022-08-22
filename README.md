# E-Commerce Store Readme

### Package Installs for Frontend

> npx create-react-app e-commerce-store-frontend

> npm install react-router-dom@6

- - Require in Browser Router in index.js and wrap < App/> with < Browser Router/>

- Import Browser Router and wrap <App/> in index.js

```javascript
import { BrowserRouter } from "react-router-dom";

// wrap <APP/> with <BrowserRouter />
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);
```

- Adds Favicon and changes store name to reflect on URL tab.
- Font Awesome for favicons.
- Adds Favicon Png.
- Remove unnecessary files.
  > npm run start

### Create Header and Footer Installs React Bootstrap.

- Create Component File.
- Adds Header Functional Component and Footer Functional Component.
- Installs React Bootstrap for Styling and !(https://bootswatch.com/) for color themes.
- Bootswatch - Click on download bootstrap.min.css bring in source file, require file into index.js.
- Adds Footer styling with React Bootstrap
- Adds Header styling using a combination of Bootswatch and React Bootstrap.
- Adds awesome font icons for cart and sign-in.

### Create HomeScreen component for display of product images.

- Uses map function to loop through the images in an array. By using React Bootstrap the Row of columns can display the number of images based on screen height.
- Passes in the Product Component through props.
- This allows access to the product json file, prior to mongoDB database.

### ### Create Product Component

- Once we have access to the product I used a destructured method to gain access to entire product ({ product }) vs using props. . I can now display the product title, name, image, reviews, etc.
- React Bootstrap has a Card which is a content container. Similar to a div <Card></Card>.
- I used React Router Dom for routing since React Router will conflict and not recognize the React Bootstrap.
- From here I display the product image, title, text, rating, price.
- Adds Styling to Card.

### Create Ratings Component

- Creating a rating component allows for static reviews to be displayed based on json created with product info. Ternary statement will either display the star value or skip it depending on value.

```javascript
<i
  style={{ color: "black" }}
  className={
    value >= 1
      ? "fas fa-star"
      : //Full Star
      value >= 0.5
      ? //If value is greater than or equal to 0.5
        "fas fa-star-half-alt"
      : //Half Star
        "far fa-star"
    //Full Star
  }
></i>
```

### Routes / Route

- Once Routes are established. Link Container from React Bootstrap will need to be implemented since React Router will not work.

```javascript
<Container>
  <Routes>
    <Route exact path="/" element={<HomeScreen />} />
    <Route path="/product/:id" element={<ProductScreen />} />
  </Routes>
</Container>
```

### Home Screen

- Now that the routes are established. The Home Screen will need to render all the products on the main page.
- useEffect and useState will be required to monitor the state changes.
- Using Axios but also tested with a Fetch call to get experience in two different http requests.

```javascript
// const urlEndpoint = "http://localhost:4000";
const urlEndpoint = process.env.REACT_APP_URL_ENDPOINT;

useEffect(() => {
  const fetchProducts = async () => {
    const apiResponse = await fetch(`${urlEndpoint}/server/api/products`);
    //.json all fetch responses - not parsed
    //axios does parse
    const apiJSON = await apiResponse.json();
    setProducts(apiJSON);
  };
  fetchProducts();
}, []);
// difference between fetch and axios
useEffect(() => {
  const fetchProducts = async () => {
    const { data } = await axios.get(`${urlEndpoint}/server/api/products`);
    setProducts(data.message);
  };
  fetchProducts();
}, []);

//data is now fetching form the backend - and eventually will fetch from the mongoDB.
```

To Note:
>  npm install axios

```javascript
const axios = require("axios");
```