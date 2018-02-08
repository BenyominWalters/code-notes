# Making Apps with Ionic

## A Step by Step Checklist 

### Step 1: Install Your Development Framework 

(If you haven’t already) install Node JS from [Node.js Website](https://nodejs.org/en/download/)
To verify you have everything installed correctly, you can run `npm --version` and `node --version`.

(If you haven’t already) install Ionic CLI with `npm install -g cordova ionic` 

### Step 2: Create a new App 

Setup a new project: Create a new Ionic project with `ionic start myApp tabs` (replace "myApp" with the name of your app). This command will create a new project folder using the "tabs" template. To use a different template change the template name at the end of the command, such as "blank", or "sidemenu". You can find more designs in the [Market] (https://market.ionicframework.com/starters/)

Go to that folder directory with `cd myApp` (replace "myApp" with the name of you app).

Open your app in a browser, so that you can see what it looks like with `iconic serve` At first you will see a default template page. This view should update automatically when you save changes to your code, to give you live updates.

Sometimes you will have to manually close the server and restart. Close the server from your terminal with [Ctrl] C then reopen with `ionic serve` 

Open your project folder in your development environment (e.g. Atom). Right click on the navigation bar on left and select add project folder, to add your project. 

Your project comes pre-populated with default folders and files. 

### Step 3: Create Pages (Components) 

Create a new page: To automatically generate a new folder with generic HTML, CSS, and TS files for you component use this command (replace “name” with whatever you want to name your new component) `ionic generate pages name`. (More generally, you can generate anything you want with `ionic generate [<type>] [<name>]`, for example, you can generate a component with `ionic generate componenet name`.  

Add your pages to the app main HTML page (or whichever page you want this component on). You do this by adding the name of your pages as an HTML element (replace the “name” in app-name with the name of your component) `<ion-name></ion-name>` 

Edit the HTML, CSS, and TS for your component to give it the structure, functionality and look you want. 

### Step 4: Wire Things Up so that Data Can Flow 

Make a Class / Model 

Make a class file: If your component will need to get or receive data from an API, or from a user input form, create a class (model or schema). This will define which kinds of data you are expecting to make sure that everything flows properly. Create a new TS file in the src/app or wherever is logical to you. (Convention is to use the singular for this, or you can add “class” or “model” or “schema” to its name for clarity.) For example, you could name this user.ts or user-class.ts 

Define and export class: Open this file. Define and export your new class, adding whatever data fields you expect. It should look something like this: 

```js
export class User { 

    id: number; 

    username: string; 

    email: string 

}
```

Each pair of values includes the variable name and then the type of data (number, string, boolean, or any). 

Import your new class: Now that this class is available, you need to import it to your component. Go back to your component’s TS file and at the top of the file add  

`import { User } from '../user';` 

Inside of the curly brackets is the name of your new class (first letter uppercase to show that it is an object ???) then add the directory of your “class” TS file. Use ../ to move up one directory (../../ for two directories, and so on). The file name is case sensitive, so keep everything lowercase when naming your file.  

Displaying Your New Class 

If you want to display data from your new class add the Angular two-way binding double curly brackets to your component’s HTML page. For example:

```HTML
<h2>{{ user.username }} Details</h2>  

<div><span>id: </span>{{user.id}}</div>  

<div><span>username: </span>{{user.username}}</div> 

<div><span>email: </span>{{user.username}}</div> 
```

Each double curly brackets includes the name of your class (dot) the tag-name of the data you want to show. So use `{{classname.dataname}}` 

Receiving User Input To Create or Edit a Member of a Class 

If you want a user to be able to create a new user, or edit a user (or any class), you need enable two-way binding. 

Import Modules: To make new functionality available to your app, you first need to import the relevant modules. These modules include prepackaged libraries of JavaScript that give you advanced functions without having to write the code from scratch. 

Open your module file (app.module.ts) 

For two-way binding import the FormsModule by adding to the following to the top of your app.module.ts file (together with the other imports). Be sure there is a semicolon after each import. 

```js
import { FormsModule } from '@angular/forms'; // <-- NgModel lives here 
```
Next add this module to the Array of imports lower in the app.module.ts file. Be sure there is a comma after each item. 
```js
imports: [ 

  BrowserModule, 

  FormsModule 

],
```

Now that things are wired up, you can add a form to your HTML page with two way binding. This will create a form that will edit your class. The changes will immediately appear in the data called by the double curly brackets. 

```HTML
<div> 

    <label>name: 

      <input [(ngModel)]="user.username" placeholder="username"> 

    </label> 

</div> 
```

For this to actually work, we need one more thing. A member of the class needs to be defined in the component’s TS file. This can be  

A static object such as:

```js
user: User = {  

    id: 1001,  

    username: 'JohnDoe', 

    email: ‘john@example.com’  

};
```

This means define “user” as a member of the class “User” and give him the following attributes `{ id: 1001, username: ‘JohnDoe’, email: ‘john@example.com }` 

A list of objects in a separate TS file. You would create this file somewhere with an Array of users and then import it at the top of your component using:  

```js
import { USERS } from ‘../users-list’; 
```

Then, add the imported array as a variable users = USERS; 

Now you can call a user from the array of users. 

Or if you want to import data from a server’s database, you will need to connect to an API. The next section covers that. 

### Step 5: Create a Service to connect to an API 
