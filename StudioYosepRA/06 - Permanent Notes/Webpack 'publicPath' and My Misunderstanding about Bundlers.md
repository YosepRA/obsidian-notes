
*Monday, September 9, 2024 - 17:50*

Status:

Tags: [[afternoon pages]] [[software engineering]]

---

You know what's the most frustrating part of solving problems? No, it's not when I solve difficult problems that it leaves me frustrated. But rather, it's when I'm facing a "simple" problem which result should be easy to predict, and yet it doesn't produce the desired simple result. It's like you would expect putting an egg on top of frying pan with oil. You would easily expect fried eggs to come out of the pan. But what would happen if it produces boiled eggs instead? Yes, you would be frustrated because you have followed the procedure, yet it doesn't produce the expected results.

I encounter such problem when I use Webpack in my code to read *You Don't Know JS* books. I don't know if this short 15 minutes is enough for me to elaborate on what was happening, but I'll try to be concise.

It was a problem with `publicPath` configuration, which results in `webpack-dev-server` unable to live reload on code changes. The problem is caused by the dev server unable to find the compiled JavaScript files. Or to be more precise, I didn't know *where* the JavaScript files are served by the dev server.

```js
const path = require('path');  

module.exports = {
  entry: {
    index: path.join(__dirname, 'src/index.js'),s
  },
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist/public'),
    publicPath: '/public',
  },
  module: {
    rules: [
      {
        test: /\.(?:js|mjs|cjs)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [
              [
                '@babel/preset-env',
                {
                  targets: 'defaults',
                  useBuiltIns: 'usage',
                  corejs: '3.37',
                },
              ],
            ],
          },
        },
      },
    ],
  },
  mode: 'development',
  devServer: {
    static: {
      directory: path.join(__dirname, 'dist'),
    },
    compress: true,
    port: 8000,
  },
  devtool: 'eval-source-map',
  resolve: {
    alias: {
      Utilities: path.resolve(__dirname, '../utils'),
    },
  },
  // optimization: {
  //   runtimeChunk: 'single',
  // },
};
```

Here is my latest Webpack configuration. Please do note that I've found the solution of my problem, and the config above is the result of said solution.

The problem lies in `output.publicPath` property. At first, I don't know exactly what it does. Up to this point, I assume that `publicPath` is just a way for my HTML file to find the compiled file. Therefore, since the `publicPath` is set to `/public`, then I can find  the compiled file from my HTML file using `/public/index.bundle.js`. Up to this day, this is my simplistic view of the property as I don't question it further.

However, the problem occurred when some time ago, I removed the `publicPath` from the `output` config. My `webpack-dev-server` is failing as its live-reload function is no longer working. I mean, who could stand a manual reload on development these days? You must be a masochist.

When I recall that I removed the `publicPath` property, I add it back to the `output` config with the same configuration as before. And voila, the dev server is working once more.

Of course, it makes me curious as to why this all happened. I won't lie, before I realize about the missing `publicPath`, I was frustrated and thinking that there must be a breaking change somewhere. Again, it was such a simple problem that shouldn't be a concern for me. Yet when something simple isn't working, then it was easier for me to get frustrated than facing an actually tough problem. I don't know why it is like that for me.

Long story short, after going round and round on Webpack documentation, I found a blog post written by a developer who had an exact same question as I do. His name is Ravi Roshan, and here is the [blog post](https://medium.com/@raviroshan.talk/webpack-understanding-the-publicpath-mystery-aeb96d9effb1).

There is this behavior that if `output.path` isn't defined (and `publicPath` isn't defined either), then the default value is the root of the project, according to where `webpack.config.js` is located. So, the location for the compiled JavaScript file should be `./bundle.js`, which is again, down in the root of the server. But then again, even if `output.path` is defined with a proper path, the dev server somehow still uses project's root as its serving point, which doesn't make any sense to me. Because I think, if the `output.path` is clear, then should it be obvious that the dev server is also taking this path as a reference as to where to serve the compiled files?

The 15 minutes timer has long gone, and I still haven't talked about my misunderstanding of Webpack and the concept of bundler tools such as it. The fact that it isn't simply bundling JavaScript files, but also it's possible to bundle other static files such as CSS, images, and fonts. Then there is correlation between the diverse type of file which can be bundled and how Webpack output and serve those files.

However, I have a few points worth of reminding about today:

1. `output.path` and `output.publicPath` must be the same. 
   If the compiled file is going to `public` folder, then the `publicPath` should direct to the same `public` folder. This way, the path that is used in the HTML file would remain consistent between development and production.
2. Webpack isn't only for bundling JavaScript, but also other files such as CSS, images, and fonts.
   The idea of a bundler is to bundle a bunch of source files into distributed folder which can then be served. The entry point might be a JavaScript file, but said JavaScript file could import many different file types.

This was a fruitful day. I would like to talk more about the second point from the list above, especially my misunderstanding about bundlers in general. But alas, I want to play games. I'm tired. Give me a break already, haha. Thank you for reading.
   

---
## References
