# puppeteer-stream

Skribe's fork of the [Extension for Puppeteer](https://www.npmjs.com/package/puppeteer-stream) to retrieve audio and/or video streams of a page

<a href="https://www.npmjs.com/package/@skribe/puppeteer-stream">
	<img src="https://img.shields.io/npm/v/@skribe/puppeteer-stream">
</a>

## Installation

```
npm i @skribe/puppeteer-stream
```

## Usage

ES5 import

```js
const { launch, getStream } = require("puppeteer-stream");
```

or ES6 import

```js
import { launch, getStream } from "puppeteer-stream";
```

### Launch

The method `launch(options)` is just a slightly changed puppeteer [launch](https://pptr.dev/#?product=Puppeteer&version=v7.1.0&show=api-puppeteerlaunchoptions) function to start puppeteer in headful mode with this extension.

## Example

### [Save Stream to File:](/examples/file.js)

```js
const { launch, getStream } = require("puppeteer-stream");
const fs = require("fs");

const file = fs.createWriteStream(__dirname + "/test.webm");

async function test() {
	const browser = await launch({
		defaultViewport: {
			width: 1920,
			height: 1080,
		},
	});

	const page = await browser.newPage();
	await page.goto("https://www.youtube.com/watch?v=dQw4w9WgXcQ");
	const stream = await getStream(page, { audio: true, video: true });
	console.log("recording");

	stream.pipe(file);
	setTimeout(async () => {
		await stream.destroy();
		file.close();
		console.log("finished");
	}, 1000 * 10);
}

test();
```

### [Stream to Discord](/examples/discord.js)

### [Stream Spotify](https://www.npmjs.com/package/spotify-playback-sdk-node)

### [Use puppeteer-extra plugins](/examples/puppeteer-extra.js)
