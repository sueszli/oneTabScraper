# OneTab Web-Scraper

A simple tool to scrape all your links into a list from a [OneTab](https://www.one-tab.com/) collection.\
Alternatively this could also be done directly in your console as in this [tutorial](https://www.youtube.com/watch?v=rlv7ueX4Yjc).

1. Request temporary access here: https://cors-anywhere.herokuapp.com/corsdemo
2. Access scraper here: https://sueszli.github.io/oneTabScraper/

(Note: Another alternative would be not using a proxy at all and installing a browser add-on that turns off CORS restrictions in your browser)

&nbsp;

## How to use
![1](https://user-images.githubusercontent.com/61852663/147303293-2a3c8321-9a0f-4f7f-95dd-eebb3c3f6f9f.gif)

&nbsp;
&nbsp;

## How it works
By only using a single fetch via a proxy.

I initially wanted to test whether I could make a lightweight webscraper that only works with vanilla javascript in your browser but I totally forgot about CORS.\
Solution: using the [CORS-Anywhere-reverse-Proxy](https://github.com/Rob--W/cors-anywhere) to bypass it.

```js
let URL = ''; // <-- Your URL will be stored here
const proxy = 'https://cors-anywhere.herokuapp.com/';

fetch(proxy + URL)
    .then(response => response.text())
    .then(htmlText => {                
        // parse html text
        const parser = new DOMParser();
        const doc = parser.parseFromString(htmlText, "text/html");

        // get anchor nodes
        const links = doc.querySelectorAll('a');
        
        // get strings from anchor nodes
        const RESULT = Array.from(links).map(link => link.href);
    });
```
