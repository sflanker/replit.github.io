# Repl Auth

We will go over how to use Repl.it Auth API.

## Good to know the following before you start:

- Basic knowledge of Python/Flask
- Basic knowledge of Jinja2 (Flask templating)
- Basic knowledge of HTML

## Steps

- We'll start off with a basic Flask template (main.py)

	from flask import Flask, render_template, request
	app = Flask('app')

	@app.route('/')
	def hello_world():
		return render_template('index.html')

	app.run(host='0.0.0.0', port=8080)
	(/templates/index.html)

	<!doctype html>
	<html>
	<head>
		<title>Repl Auth</title>
	</head>
	<body>
		Hello!
	</body>
	</html>

## The authentication script.

	<div>
		<script authed="location.reload()" src="https://auth.turbio.repl.co/script.js"></script>
	</div>

This can be placed anywhere in the document body and will create an iframe in its parent element. Additionally, any JavaScript placed in the authed attribute will be executed when the person finishes authenticating, so the current one will just reload when the user authenticates.
If you run it now, you will notice a big Let (your site url) know who you are? with a small version of your profile and an Authorize button.
You can click the button but nothing will happen.

The headers

Now, let's make something happen.
Go back to your main.py file; we will be grabbing the Repl.it specific headers for the request and extracting data from them.
The main ones we care about are: X-Replit-User-Id, X-Replit-User-Name, and X-Replit-User-Roles. The username one will probably be the most useful for now.
With this information, we can let our HTML template be aware of them.
(main.py)

	@app.route('/')
	def hello_world():
		return render_template(
			'index.html',
			user_id=request.headers['X-Replit-User-Id'],
			user_name=request.headers['X-Replit-User-Name'],
			user_roles=request.headers['X-Replit-User-Roles']
		)
	(templates/index.html)

	<body>
		{% if user_id %}
		<h1>Hello, {{ user_name }}!</h1>
		<p>Your user id is {{ user_id }}.</p>
		{% else %}
		Hello! Please log in.
		<div>
			<script authed="location.reload()" src="https://auth.turbio.repl.co/script.js"></script>
		</div>
		{% endif %}
	</body>

Success!

Now, run your code. It should display a big Hello, (your username)! along with your user ID.

If you want to port this to other languages or frameworks like NodeJS + Express, just be aware of how you can get specific request headers.

Warning
Also, be aware that if you're going to be using an accounts system, PLEASE do all the specific logic for checking users on the BACKEND, that means NOT doing it with JavaScript in your HTML. That is all.

## Example Repl
- https://repl.it/@mat1/repl-auth-example.

Show some love on Repl.it talk for [mat1](https://repl.it/@mat1) on his [post](https://repl.it/talk/learn/Authenticating-users-with-Replit-Auth/23460) as he is the mind behind this!