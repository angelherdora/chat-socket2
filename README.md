<h1>RealtimeChat</h1>
<p>This is a source code of powerful private chat built with Node.js and Socket.io</p><hr />
<h3>The code</h3>
<p>You can grab the source code from the download button above. It has plenty of comments and is easy to follow. Start with the <b>app.js</b> file and read from there. Here are a few things to look for:</p>
<ul><li>All dependencies are declared in the <b>package.json</b> file. They are not included in the zip and you will have to run <code>npm install</code> to get them.</li>
<li>We are using separate JavaScript files for the configuration and routes, to make the code more manageable.</li>
<li>In the routes file, <b>socket.io</b> stores the username, avatar and room of the person as properties of the socket object itself. This saves us a lot of code and makes managing rooms easy.</li>
<li>We use <b>socket.io</b>‘s <a href="https://github.com/LearnBoost/socket.io/wiki/Rooms">rooms</a> feature to isolate one chat from another, which is exactly what that feature was developed for.</li>
</ul><hr /><h3>Running the Chat</h3>
<p>To run the chat, you need to have node.js installed, so that the <code>node</code> and <code>npm</code> commands can be called from your terminal. Download the code and unzip the archive to a folder called nodejs-private-webchat. After this, navigate to the folder you’ve created from your terminal:</p>
<pre>cd nodejs-private-webchat/</pre>
<p>Running the ls (or dir if you are on windows) command should show <b>app.js</b>, <b>package.json</b> and the other files from the archive. Then, run this command to download all the libraries that the chat system uses:</p>
<pre>npm install</pre>
<p>This will install all the dependencies that are described in <b>package.json</b>. This may take one or two minutes. When it’s done, run the following command to start your very own local chat, which you can see on http://localhost:8080</p>
<pre>node app.js</pre>
<p>Hit <b>ctrl+c</b> to stop it. The bad news is that you can’t invite your friends to your chat, since it is running on your own computer. To fix this, you need to run it on a web server. Setting up a web server by yourself to run node is not a very straightforward process and involves a good deal of server administration skills. Luckily, it is very easy to get started with cloud platforms like Heroku, which is what I will show you next.</p><hr />
<h3>Hosting the Chat on Heroku</h3>
<p>Heroku is a cloud hosting platform that automates the deployment and scaling of web apps. It offers a free plan, which is sufficient for less busy apps like our chat. Here is what you need to do:</p>
<ol><li><a href="https://id.heroku.com/signup">Create an account</a>, if you don’t have one already.</li>
<li>Install the <a href="https://toolbelt.heroku.com/">heroku toolbelt</a> for your operating system. It will give you access to the <code>heroku</code> command from a terminal window.</li>
<li>Initialize an empty git repository (explained below)</li>
<li>Push your code to heroku. This will deploy it and give you a URL which you can share with your friends.</li></ol>
<h4>Creating a git repo</h4>
<p>The heroku toolbelt installs the <code>heroku</code> command and the <code>git</code> version control system. You need to create a git repo in order to be able to deploy your app to heroku (there is no ftp here). To do this, run this command:</p>
<pre>git init</pre>
<p>Then, we need to tell git not to include the <b>node_modules</b> folder to your repo. This folder can grow quite large and it simply does not belong in git. To ignore the folder, create a new empty text file named <b>.gitignore</b> with the following content:</p>
<pre>node_modules/</pre>
<p>Now you can commit your code to your fresh new repo! Write these commands:</p>
<pre>git add .
git commit -m 'Initial commit'</pre>
<p>There is one last thing that we have to do. Heroku requires that your application has a text file named <b>Procfile</b>, which contains the command used to start your node.js app. Create it, and add the following content:</p>
<pre>web: node app.js</pre>
<p>Then commit the changes with these commands:</p>
<pre>git add Procfile
git commit -m 'Added a procfile'</pre>
<p>We are now ready to push the application to heroku!</p>
<h4>Pushing to Heroku</h4>
<p>The following two commands are only done the first time you start using the <b>heroku</b> utility. First you need to login to heroku from the command line tool:</p>
<pre>heroku login</pre>
<p>Then, you need to add your ssh key, so you can push code without entering a password:</p>
<pre>heroku keys:add</pre>
<p>Next, you need to create a new heroku application from the code in this folder:</p>
<pre>heroku create</pre>
<p>And finally, we are ready to push code! Type this command:</p>
<pre>git push heroku master</pre>
<p>This line will send your application code to heroku, where their servers will process your package.json file and install all libraries that your app needs. Do this every time you need to upload a new version of the code (you must have made a commit beforehand). All that is left, is to enable websockets so that our real-time chat can work:</p>
<pre>heroku labs:enable websockets</pre>
<p>To open your very own web chat in your browser run this command:</p>
<pre>heroku open</pre>
<p>This will open it in a tab in your default browser.</p><hr />
<h3>Hope you like our little chat!</h3>
<p>But there is much more that can be improved on it. You may implement alerts of new messages with HTML5 audio, make it possible for more than two people to join the same room, to require passwords before joining and more. </p>
