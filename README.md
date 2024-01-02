# Server-Side Rendering (SSR) in React

## Introduction to SSR

Server-Side Rendering (SSR) is a technique in web development that enhances the performance and SEO of React applications. SSR involves rendering React components on the server before sending them to the client.

## Benefits of SSR

- **Improved SEO**: SSR enhances search engine visibility by providing fully rendered content.
- **Faster Initial Page Load**: Users experience quicker page rendering, especially on slower connections.
- **Accessibility**: SSR ensures a more consistent experience for users across diverse devices.

### Real-World Use Cases

- E-commerce websites with dynamic content.
- Any platform where SEO is crucial.

## How SSR Works in React

In SSR, React components are rendered on the server, producing fully formed HTML. This HTML is then sent to the client, reducing the initial load time. 

## Implementing SSR in React

Follow these steps to implement SSR in your React application:

1. **Create a Simple React App:**

   ```bash
   npx create-react-app app-name
   ```
2. **Update index.js:**\
Replace the rendering method in `index.js` file:

    ```
    // Before
    ReactDOM.render(<App />, document.getElementById('root'));

    // After
    ReactDOM.hydrate(<App />, document.getElementById('root'));
    ```
1. **Install Express:**

   ```bash
   npm install express
   ```
2. **Install Babel:**

   ```bash
   npm install @babel/register @babel/preset-env @babel/preset-react ignore-styles
   ```
3. **Create Server Folder:**\
Create new folder called **server**. Inside it, create a file named `server.js` & paste following code.

    ```server/server.js
    // Copy following
    
    import path from 'path';
    import fs from 'fs';
    import express from 'express';
    import React from 'react';
    import ReactDOMServer from 'react-dom/server';
    import App from '../src/App';
    const PORT = 8080;
    const app = express();

    const serverRenderer = (req, res, next) => {
      fs.readFile(path.resolve('./build/index.html'), 'utf8', (err, data) => {
        if (err) {
          console.error(err);
          return res.status(500).send('An error occurred');
        }
        return res.send(
          data.replace(
            '<div id="root"></div>',
            `<div id="root">${ReactDOMServer.renderToString(<App />)}</div>`
          )
        );
      });
    };

    app.use('^/$', serverRenderer);
    app.use(express.static(path.resolve(__dirname, '..', 'build'), { maxAge: '30d' }));

    app.listen(PORT, () => {
      console.log(`SSR running on port ${PORT}`);
    });
    ```
1. **Create an Entry Point:**\
Create an entry point in server/index.js,
Create a new file `index.js` in **server**.

   ```server/index.js
    require('ignore-styles');
    require('@babel/register')({
      ignore: [/(node_modules)/],
      presets: ['@babel/preset-env', '@babel/preset-react'],
    });
    require('./server');
   ```
1. **Build and Run:**

   ```bash
   npm run build
   node server/index.js
   ```
## **Folder Structure:** (Just to be safe)
   Your final folder structure will be

   ```
    node_modules/
    public/
    src/
        |-- components/
        |-- App.js
        |-- index.js
    server/
        |-- server.js
        |-- index.js
    package.json
    .gitignore
    README.md
    other_files_and_folders...
   ```

   ---

🚀 **Congratulations!** You've successfully implemented Server-Side Rendering (SSR) in your React application. We hope this guide enhance your application's performance and SEO.

## Support

If you find this guide helpful, consider giving it a ⭐ to show your support.\
**Your support means a lot**!


## Issues and Feedback

Found a bug or want to suggest an improvement? Feel free to [open an issue](https://github.com/Arslan2214/SSR-with-React/issues). Your feedback is valuable and helps us improve this guide.


## License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.

Happy coding! 👩‍💻👨‍💻


---  
