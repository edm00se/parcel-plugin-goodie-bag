# parcel-plugin-goodie-bag

A polyfill for `Promise` and `fetch` to keep Parcel working for those without it.

[Looking at you Internet Explorer](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-perils-of-using-Internet-Explorer-as-your-default-browser/ba-p/331732).

## Why This Is Needed

TL;DR: multiple bundle support in Parcel, such as using the ability to require html partial files, makes direct use of both the `Promise` and `fetch` APIs, directly.

This plugin is born of my frustaration with the scenario outline in [parcel issue #2364](https://github.com/parcel-bundler/parcel/issues/2364). This requires additional intervention, since the native requirement of the potentially un-polyfilled APIs is prior to any polyfill via `babel-polyfill` and isn't something that can be influenced inside the application source itself; at least not without convoluted efforts.

## Installation

- `npm install --save-dev parcel-plugin-goodie-bag`

## Usage

No additional configuration required. If your app is being bundled by parcel and you have this plugin installed, the processed application will build with:

- the `*.html` containing a `script` tag in its head pointing to the "goodie bag` script (the two polyfills)
- a "goodie bag" script file, placed in the destination directory (`outDir` to parcel, defaults to `dist`)
- the script tag will respect your configured `publicUrl` option with Parcel (e.g.- prefixed with default `/` or no root slash in the case of `.`)

Note: If you're not processing your `index.html` file through parcel, for example merely bundling the JS directly, I believe you're missing out on some of the super powers of parcel. However, if that's your workflow and you're missing out on this plugin's functionality, please consult the discussion and resolution outlined [in this issue][non-html-support].

## In Action

I made use of [a simple reproducible repository](https://github.com/edm00se/parcel-ie11-issue-demo) I had set up for tracking this issue.

| Before                         | After                        |
|--------------------------------|------------------------------|
| ![before](assets/before.jpg)   | ![after](assets/after.jpg)   |

## Contributing

If you have something to contribute, please do. If you're uncertain as to whether or not to open a PR, feel free to ask; just open an issue and mark that it's a question.

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
<table>
  <tr>
    <td align="center"><a href="https://edm00se.codes/"><img src="https://avatars3.githubusercontent.com/u/622118?v=4" width="100px;" alt="Eric McCormick"/><br /><sub><b>Eric McCormick</b></sub></a><br /><a href="#blog-edm00se" title="Blogposts">📝</a> <a href="https://github.com/edm00se/parcel-plugin-goodie-bag/issues?q=author%3Aedm00se" title="Bug reports">🐛</a> <a href="https://github.com/edm00se/parcel-plugin-goodie-bag/commits?author=edm00se" title="Code">💻</a> <a href="#content-edm00se" title="Content">🖋</a> <a href="https://github.com/edm00se/parcel-plugin-goodie-bag/commits?author=edm00se" title="Documentation">📖</a> <a href="#example-edm00se" title="Examples">💡</a> <a href="#ideas-edm00se" title="Ideas, Planning, & Feedback">🤔</a> <a href="#maintenance-edm00se" title="Maintenance">🚧</a> <a href="#review-edm00se" title="Reviewed Pull Requests">👀</a> <a href="#userTesting-edm00se" title="User Testing">📓</a></td>
    <td align="center"><a href="https://github.com/Joe-Withey"><img src="https://avatars3.githubusercontent.com/u/12202750?v=4" width="100px;" alt="Joe Withey"/><br /><sub><b>Joe Withey</b></sub></a><br /><a href="https://github.com/edm00se/parcel-plugin-goodie-bag/commits?author=Joe-Withey" title="Code">💻</a> <a href="#ideas-Joe-Withey" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://v01.io"><img src="https://avatars0.githubusercontent.com/u/32771?v=4" width="100px;" alt="Klaus Breyer"/><br /><sub><b>Klaus Breyer</b></sub></a><br /><a href="https://github.com/edm00se/parcel-plugin-goodie-bag/issues?q=author%3Aklausbreyer" title="Bug reports">🐛</a> <a href="#ideas-klausbreyer" title="Ideas, Planning, & Feedback">🤔</a></td>
  </tr>
</table>

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!

## History

Parcel is an amazing bundler with superpowers. The fact that my ability to support IE(11), a requirement for my day job, was hampered by this limitation of a multiple bundle scenario meant that I had to solve the problem myself. It is my hope that one day the configuration of Parcel will allow for the surfacing of base level APIs, such as `Promise` and `fetch` to make this plugin unnecessary. Until then, I'll keep this available to provide some sanity.

## Credits
- [parcel](https://parceljs.org/)

## License

MIT

[non-html-support]: https://github.com/edm00se/parcel-plugin-goodie-bag/issues/2#issuecomment-502219004
