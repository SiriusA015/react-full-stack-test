<div align="center">
  <p>
    <img src="assets/logo_bcw.png" width="250" />
  </p>
  <p>
    Transforming the DLT Ecosystem
  </p>
</div>

# Take Home Test (Fullstack)

## Overview

This is a take-home test for candidates applying for a full-stack developer
position at BCW Technologies. It contains three sections: "Frontend" and "Backend" which
together include a series of tests involving React, Typescript, and Node.js.

Feel free to solve these questions however you see fit, using whatever coding
style or third-party libraries you think are appropriate.

To start the test, simply clone this repo and make your edits locally. Once you are done, please push your changes to this repo and create a pull request.

NOTE: We expect more than one commit in the PR, do not spend time overthinking the commit messages or squashing your commits together.

## Frontend

For the frontend portion of the test, use the `/frontend` folder. There are 7 features we'd like to add:

1. Fetch and display the list of cryptocurrencies available from CoinStats (see endpoint below).
2. **Create a responsive layout** that will display these currencies and their respective image, URLs, and data.
3. Add a dropdown menu to fetch the list in one of the following currencies: HKD, KRW, SGD, and USD.
4. Add a button to sort the list of currencies by the rank of the currencies.
5. Add a button to sort the list of currencies by alphabetical order using the name of the currencies.
6. Add a field to display the exchange a user should use to minimize the amount of a _selected currency_ they would need to spend on a trade 

    6a. _selected currency_ is the currency the user has selected in #3.

    6b. The correct exchange(s) should be returned by the backend server you are tasked to create below.

### Tips

- Please make the app be served on port `:3000`.

- **Please use React-Typescript for this task**, but feel free to structure the code however you prefer and use any other third-party libraries at your discretion. 

- Do not spend too much time making it beautiful. Basic aesthetics are expected, please try to balance your time between function and aesthetics.

### API Information

- **CoinStats Public API `GET /public/v1/coins` endpoint:** 

    - https://api.coinstats.app/public/v1/coins

- **Parameters:**

    - `currency`: `string` - one of `HKD`, `KRW`, `SGD`, and `USD`.

- **Example:**

    - `curl --location --request GET 'https://api.coinstats.app/public/v1/coins?currency=USD'`

## Backend

For the backend portion of the test, use the `/backend` folder. Feel free to structure the code however you prefer and use third-party libraries at your discretion. We'd like to write some code that achieves the following:

1. Create a JSON API (REST or GraphQL) using Node.js which will return which cryptocurrency exchange a user should use to buy a cryptocurrency to minimise the amount of the _selected currency_ they would spend on this trade.

### Tips


1. You'll need to filter out `pair`s that do not support the _selected currency_.
2. You may perform this operation once per query, or once for each cryptocurrency - you may need to justify your decision at a later time.
3. If only one exchange supports the _selected currency_, you can simply return that exchange's name.
4. You should use the following CoinStats endpoint below to help achieve this task.

NOTE: Please make the server listen on port `:4000`.

### API Information

- **CoinStats Public API `GET /public/v1/markets` endpoint:** 

    - https://api.coinstats.app/public/v1/markets

- **Parameters:**

    - `coinId`: `string`

- **Example Request:**

    - `curl --location --request GET 'https://api.coinstats.app/public/v1/markets?coinId=bitcoin'`

- **Example Response:**

```json
[
    {"price":57000,"link":"https://www.kraken.com","exchange":"Kraken","pair":"BTC/USD","pairPrice":57000,"volume":161168912.22402},
    {"price":56915.26,"link":"https://gemini.com/","exchange":"Gemini","pair":"BTC/USD","pairPrice":56915.26,"volume":64963739.7345771}
]
```

### Example Implementations

- Request:

    - `curl http://localhost:4000/exchange-route?coinId=BTC&currency=USD`

- Response:

```json
{
    "exchange": "Kraken",
}
```

**or...**

- Request:

    - `curl http://localhost:4000/exchange-route?&currency=USD`

- Response:

```json
[
    { "coinId": "BTC", "exchange": "Kraken" },
    { "coinId": "ETH", "exchange": "Gemini" },
]
```

## Docker (optional)

The test contains a basic `docker-compose.yml` file. It uses the latest official NodeJS
Docker image and creates two containers - one for backend and one for frontend.

The respective folder is mounted in `/app` directory inside the container.

It isn't a requirement to use Docker, but may be convenient.

## Submitting Your Code

Once you've completed the test, please send a pull request to the same repository.

**Do not include node_modules or .git in your submission.**

We will then review it and get back to you as soon as possible.

Thanks!