# Build Simple Crypto portfolio demo with using
* Moralis API
* Moralis account https://admin.moralis.io/login
* React
* Node.js
* Basic HTML, CSSS skills
## Getting Started with Create React App
Create new react-app in your terminal

```javascript
npx create-react-app portfolio-demo
```
In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

***Create new file in your project directory .evn***

inside the file add REACT_APP_MORALIS_API_KEY 

***Go to Moralis website sign up for your account in order to get your Moralis API_Key***
you should be able to get your Moralis API_Key. Copy and place in your .env file 

![Screenshot 2024-02-26 121320](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/d9c58558-e5c7-4c02-91ae-ebfe965fefb1)
copy your API_Key and paste in your .env file 


## Inside your code editor go to App.js file and replace with 
```javascript
import './App.css';
import React, { useState, useEffect } from "react";

function App() {

  const [assets, setAssets] = useState([]);
  // const [address, setAddress] = useState("")

  const fetchAssets = async (address) => {
    try {
      const response = await fetch(`URL`, {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          "X-API-Key": process.env.REACT_APP_MORALIS_API_KEY
        }
      })
      const data = await response.json();
      setAssets(data.result);

    } catch (error) {


    }
  }

 useEffect(() => {
    fetchAssets()
  }, [])
  return (
    <div className="App">
      <h1>My Crypto Portfolio</h1>
      <table>
        <thead>
          <tr>
            <th>Logo</th>
            <th>Name</th>
            <th>Price</th>
            <th>Value</th>
            <th>24h change</th>
          </tr>
        </thead>
        <tbody>
          {assets.map((asset) => (
            <tr key={asset.token_address}>
              <td><img src={asset.thumbnail} alt={asset.name} className='asset-logo' /></td>
              <td>{asset.name}</td>
              <td>{asset.usd_price}</td>
              <td>{asset.usd_value}</td>
              <td className={asset.usd_price_24hr_percent_change}>
              </td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}


export default App;
```

## Go to file App.css and replace with

```javascript

.App {
  text-align: center;
  margin: 20px 160px;
}

table {
  width: 100%;
}

th,
td {
  text-align: left;
  padding: 14px 8px;
  border-bottom: 1px solid #ddd;
}


.asset-logo {
  width: 40px;
  height: 40px;
}
```
## Go to Moralis website get URL 
got to Web3 API Data 

![Screenshot 2024-02-27 132959](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/30132ce1-72f8-40ed-aead-dca3bb30efd0)

choose true to both as shown on the pic 

![df](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/44d5319a-02f5-408d-8f67-7fa65f299cb0)

go to URL section and copy the link 

![Screenshot 2024-02-27 132959dff](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/a8e05ab4-5cb1-4443-bd4d-d4039eb2503d)

go back to your App.js and paste your URL link 

![Screenshot 2024-02-26 134235](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/716fae61-53a8-4541-bcab-380be3ca9d84)

update code line by paste your moralis account from URL link 

```shell
const [address, setAddress] = useState("0x0....")
```
go to line code with your URL please cut your moralis account address and replace with 

```shell
${address}
```


```shell
const response = await fetch(`https://deep-index.moralis.io/api/v2.2/wallets/${address}/tokens?chain=eth&exclude_spam=true&exclude_unverified_contracts=true`, {
```
in your terminal 
```shell
npm start
```
you should get this 

![Screenshot 2024-02-26 130920](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/d96c36ee-c7ec-4df5-acda-8f9e0f375bc1)

## Next go to App.css 
Please feel free to do any styling you wish here is very simple example 
In your App.css file please add above .App 

```shell

body,
html {
  margin: 0;
  padding: 0;
  background-color: #0c243e;
  color: #fff;
}
```
you should get this 

![Screenshot 2024-02-27 142057](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/f50487bb-d3c0-4981-9c65-ba83952b1ad9)

Please you can use whatever styling and background you wish here another example 

![Screenshot 2024-02-26 132434](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/18b02c4e-31e8-401b-b7d2-d45b465df51d)

## Go to App.js 
upgrade your code by adding 

```shell
 <tbody>
          {assets.map((asset) => (
            <tr key={asset.token_address}>
              <td><img src={asset.thumbnail} alt={asset.name} className='asset-logo' /></td>
              <td>{asset.name}</td>
              <td>{asset.usd_price?.toFixed(2)}</td>
              <td>{asset.usd_value?.toFixed(2)}</td>
              <td className={asset.usd_price_24hr_percent_change < 0 ? "negative" : "positive"}>
                {asset.usd_price_24hr_percent_change?.toFixed(2)}%
              </td>
            </tr>
          ))}
        </tbody>
```
also update another line of code by adding 

```shell
const handleInputChange = (e) => {
    setAddress(e.target.value);
  }

  const handleButtonClick = (e) => {
    fetchAssets(address);
  }
```
update and add 

```shell
 useEffect(() => {
    fetchAssets(address)
  }, [address])
```

updat and add

```shell

 const data = await response.json();
      setAssets(data.result);

    } catch (error) {
      console.error("Error fetching assets:", error);

    }
  }
```
go to index.css file and add 
```shell

.positive {
  color: #4fbf67;
}

.negative {
  color: #ff5c5c;
}
```

You should get this

![Screenshot 2024-02-27 143800](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/c359e13b-2950-49e0-a819-7cad4d22914d)

## The last thing 
Go to your App.js file and update your code by adding input in order to fetch account 
```shell
 <h1>My Crypto Portfolio</h1>
      <input
        type="text"
        value={address}
        onChange={handleInputChange}
        placeholder="Enter wallet address"
      />
      <button onClick={handleButtonClick}>Fetch assets</button>
      <table>
        <thead>
```

## Final Result 
![Screenshot 2024-02-27 145419](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/200df0ac-d722-4f5f-ab7f-31d46cd0bac4)

***If you get confused with the lines of coding, see my final code included in this repository*** 

Thank you 
# Happy coding 
![jj](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/85ee6a4b-7520-4a01-adc7-2275e013a7f1)

![Screenshot 2024-02-05 143817](https://github.com/DCVglobalnetwork/crypto-portfolio/assets/105791829/eaee1680-1ecc-4721-bc3d-42819be1f7bc)









