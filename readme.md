# prompt-skeleton

This project aims to bring a **consistent behavior to CLI apps**.

[![npm version](https://img.shields.io/npm/v/prompt-skeleton.svg)](https://www.npmjs.com/package/prompt-skeleton)
[![dependency status](https://img.shields.io/david/derhuerst/prompt-skeleton.svg)](https://david-dm.org/derhuerst/prompt-skeleton#info=dependencies)
![ISC-licensed](https://img.shields.io/github/license/derhuerst/prompt-skeleton.svg)
[![chat on gitter](https://badges.gitter.im/derhuerst.svg)](https://gitter.im/derhuerst)

Instead of letting prompts parse user input by themselves, *prompt-skeleton* provides a [standard set of actions like `submit`](#actions), which prompts can act on by exposing methods. The key bindings are [readline](https://de.wikipedia.org/wiki/GNU_readline)-inspired.


## Prompts using *prompt-skeleton*

- [`sms-cli`](https://github.com/derhuerst/sms-cli)
- [`date-prompt`](https://github.com/derhuerst/date-prompt)
- [`mail-prompt`](https://github.com/derhuerst/mail-prompt)
- [`multiselect-prompt`](https://github.com/derhuerst/multiselect-prompt)
- [`number-prompt`](https://github.com/derhuerst/number-prompt)
- [`range-prompt`](https://github.com/derhuerst/range-prompt)
- [`select-prompt`](https://github.com/derhuerst/select-prompt)
- [`text-prompt`](https://github.com/derhuerst/text-prompt)
- [`tree-select-prompt`](https://github.com/derhuerst/tree-select-prompt)
- [`cli-autocomplete`](https://github.com/derhuerst/cli-autocomplete)
- [`switch-prompt`](https://github.com/derhuerst/switch-prompt)

Use [`cli-prompter`](https://github.com/ahdinosaur/cli-prompter) if you want to have batteries included of if you want to chain prompts.


## Installing

```
npm install prompt-skeleton
```


## Usage

```js
wrap(prompt) // Promise
```

To render to screen, [`write`](https://nodejs.org/api/stream.html#stream_writable_write_chunk_encoding_callback) to `prompt.out`. Because `prompt.out` is a [`ansi-diff-stream`](https://www.npmjs.com/package/ansi-diff-stream#usage), you can also clear the screen manually be calling `prompt.out.clear()`.

### Actions

You can process any of these actions by exposing a method `prompt[action]`.

- `first`/`last` – move to the first/last letter/digit
- `left`/`right`
- `up`/`down`
- `next` - for tabbing
- `delete` – remove letter/digit left to the cursor
- `space`
- `submit` – success, close the prompt
- `abort` – failure, close the prompt
- `reset`

### Example

This renders a prompt that lets you pick a number.

```js
const wrap = require('prompt-skeleton')

const prompt = wrap({
	value: 0,
	up: function () {
		this.value++
		this.render()
	},
	down: function () {
		this.value--
		this.render()
	},
	render: function () {
		this.out.write(`The value is ${this.value}.`)
	}
})

prompt
.then((val) => {
	// prompt succeeded, do something with the value
})
.catch((val) => {
	// prompt aborted, do something with the value
})
```


## Contributing

If you **have a question**, **found a bug** or want to **propose a feature**, have a look at [the issues page](https://github.com/derhuerst/prompt-skeleton/issues).
