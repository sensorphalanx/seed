# ![logo](media/logo.png) Qlovaseed [![Godoc](https://godoc.org/github.com/qlova/seed?status.svg)](https://godoc.org/github.com/qlova/seed)  

Qlovaseed is a cross-platform Go framework for building apps.

**Please Note:** Qlovaseed is currently very unstable and in heavy development.

An app written in Qlovaseed spins up a http server to host the app, 
the executable can be dropped on a public facing web server in order to serve it as a progressive webapp.
Alternatively, the executable can be distributed to users directly and run
 as a local application (users must have a compatiable web-browser such as Chrome).

## Features

* Automatically manages pwa service workers, manifests and offline state.
* Seamless client-server communication.
* Generates minified & gzipped html, css and javascript.
* Server-rendered by default.
* **Optional** javascript/html/css (but you don't need it!)

## Installing

You can install Qlovaseed using go get.
```
	go get -u -v github.com/qlova/seed
```

## Getting started

Create a file called HelloWorld.go and paste in the following contents:

```
	package main

	import "github.com/qlova/seed"

	func main() {
		//Create a new app with Hello World as both the title and the content.
		seed.NewApp("Hello World", "Hello World").Launch()
	}
```

In the same folder, run go build to create an executable of the app that you can run to see the app in action!

## Widgets and Logic

Create a file called MyApp.go and paste in the following contents:

```
	package main

	import "github.com/qlova/seed"
	
	//Import a widget to use it, a list of widgets can be found in the widgets directory.
	import "github.com/qlova/seed/widgets/button"

	func main() {
		var App = seed.NewApp("My App")

		//In order to add a widget to your app, or container, use the package's AddTo method.
		var ClientPowered = button.AddTo(App, "My callback runs on the client")
		
			ClientPowered.OnClick(func(q seed.Script) {
				ClientPowered.Script(q).SetText(q.String("You clicked me!"))
			})
		
		
		var ServerPowered = button.AddTo(App, "My callback runs on the server")
		
			//You can style widgets with methods of the style package.
			ServerPowered.SetColor(seed.RGB(100, 100, 0))
		
			ServerPowered.OnClick(seed.Go(func(user seed.User) {
				ServerPowered.For(user).SetText("You clicked me!")
			}))

		App.Launch()
	}
```

This example shows a quick glimpse on how powerful Qlovaseed can be. 

Please remember, this framework is in development, it does not have a stable API and features are currently implemented as needed.
