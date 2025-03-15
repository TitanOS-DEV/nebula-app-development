# App Development for TitanOS Nebula
> [!IMPORTANT]
> If you want to put your app on the Store<sup>BETA</sup>, you will need to apply for a TitanOS Developer account.

Apps in TitanOS Nebula are JavaScript files.
In this demonstration, we will be creating a simple Hello World TitanOS application, then sideloading it into the web client.

First, we need to create the file. Make a new file. Call it "HelloWorldApp.js".

Next, we need the boilerplate code. Copy the below into your file:

```javascript
import App from '/static/scripts/app.js';

class HelloWorldApp extends App {
// This is where the app's code will go.
}

export default HelloWorldApp;
```

To make your app actually work, we first need to define a constructor.
Let's add one.

Inside your HelloWorldApp class:

```javascript
class HelloWorldApp extends App {
    constructor() {
        super("HelloWorldApp", "My New App", 400, 300, 'https://picsum.photos/64', 'block');
    }
}
```

What this does is:
1. `"HelloWorldApp"` - Tells the system to call your app, internally, "HelloWorldApp".
2. `"My New App"` - This is the text the user will see the app as, for example in the title of the window.
3. `400, 300` - This tells the system the default width and height of the window.
4. `'https://picsum.photos/64'` - This provides the system with the taskbar icon for the app.
5. `'block'` - This tells the system whether to use `flex` or `block` style for rendering the app's content.

Next, we need to render the actual app.

Let's add a render function to the app.

```javascript
class HelloWorldApp extends App {
    constructor() {
        super("HelloWorldApp", "My New App", 400, 300, 'https://picsum.photos/64', 'block');
    }

    render() {
        const appContent = this.container.querySelector(".appContent");
        appContent.innerHTML = `
            <h1>Hello World!</h1>
            <h2>Your name is ${username}</h2>
        `;
    }
}
```

What this does is:
1. Define the appContent.
<!-- TODO: MAKE `appContent` THE FIRST POSITIONAL PARAMETER PASSED TO RENDER, OR DEFINE `this.appContent` !-->
2. Set the appContent to a HTML template.
> [!NOTE]
> The `username` variable is global and can be accessed anywhere from your app.


Now that we have a working (albeit basic) app, we need to sideload it.

First, you need to enter the browser's Console.

After opening up TitanOS, use F12 or CTRL+SHIFT+I to open up DevTools, then in the top bar, select "Console".

Next, you'll need to host your HelloWorldApp.js somewhere (localhost is fine).

The easiest way to do this would be setting up a simple Flask app, putting your script into the `static/` directory, then hosting it on port 8000 for example.

Now, we need to load the app.

In the console, type the following command:

```javascript
await appManager.installApp(`/path/to/your/file.js`)
```

For example, if your file is hosted at `http://localhost:8000/static/HelloWorldApp.js`, you would type:
```javascript
await appManager.installApp(`http://localhost:8000/static/HelloWorldApp.js`)
```

Before you hit enter, your console should look something like this:
![image](https://github.com/user-attachments/assets/d7b0996c-13b2-4f3a-82f9-915c536fa569)

Now, hit enter, and wait for it to install.

It should end up like this:

![image](https://github.com/user-attachments/assets/f3f1a882-70b0-43e3-a6cd-19aef3e7ec26)

And your app will be ready in the taskbar!

![image](https://github.com/user-attachments/assets/4dc53194-5ef4-4bdc-b8e0-c9829b9cdeb2)

When you open it:

![image](https://github.com/user-attachments/assets/2c12a665-8a40-42ed-944d-84b7879de2c4)
