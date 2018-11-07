Let's look at a minimal webpack setup.

Installation: 

-> Assuming we're in a directory with a package.json file, we can add webpack and the development server to a project with
   npm install --save-dev webpack webpack-dev-server
   This installs webpack and the development server as a dev dependency. In other words, this implies: webpack is necessary to build        your project during development, but not when the project is already built for production or when consuming the project as a library.
   
Scripts: 

-> We'll add two scripts to our package.json file in the scripts section:
-> package.json
  {
    ...
    "scripts": {
      "dev": "webpack-dev-server --env.dev",
      "build": "webpack"
    },
    ...
  }
-> The dev script will start our development server, passing the options {env: 'dev'} to our config file. The build script will save a      single .js file on the filesystem for serving from a production server. We'll use these scripts shortly to bundle and test our app.
   Configuration
-> Webpack is most commonly configured using a separate config file: webpack.config.js. This file must export a configuration object, or    a function which returns a configuration object, which the webpack compiler will use when run from the command line as webpack. 
-> Let's add a webpack.config.js now:
    webpack.config.js
    module.exports = options => {
      return {
        entry: './index.js',
        output: {
          filename: 'bundle.js',
        },
      }
    }
-> There are only two essential fields: the entry point file, and the output file. Later, we can use options to specify a different        configuration for development/production (remember, we pass {env: 'dev'} as options in our dev script).
   Essential files
   
-> Let's add the bare minimum files needed to see something on the screen. We'll create an index.js and an index.html:
  index.js: 
    // index.js
    document.write('Hello World!')
  index.html: 
    <!-- index.html -->
    <script src="./bundle.js"></script>
    
Running the development server:

-> Now we can run 'npm run dev' to run the script we set up in the package.json.
-> This will start the development server.
-> If we navigate to localhost:8080 in a browser, we should see our index.html file, which will run our index.js bundled into bundle.js,    displaying Hello World! on the screen.
