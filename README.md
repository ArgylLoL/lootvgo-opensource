# LootVGO has been opened sourced!

Great news is LootVGO.com has become open sourced! Before we get started, letting anyone using this know. This won't be a heavily maintained Repo if at all.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

## Prerequisites

You will need to have these software below setup, these are required to run the site.

Requirements:

![](https://i.imgur.com/5QUNxfG.jpg)
![](https://i.imgur.com/fGdDyTc.png)
![](https://i.imgur.com/OPsaR0f.png)

Those all can be found with a quick google search how to setup.

## Installing

### Backend Setup

I highly suggest reading these if you have not already!

![https://wax.io](https://i.imgur.com/NYursLn.png)
![https://opskins.com](https://i.imgur.com/OQukGYM.png)

OPSkins API - [HERE](https://docs.opskins.com/public/en.html)\
OPSkins Trade API - [HERE](https://github.com/OPSkins/trade-opskins-api)

First you will need to move into the backend directory and run

```
npm install
```

![](https://i.gyazo.com/b4166e72256ac776e4438266b484f4b5.png)

While that's running lets update our config with some initial info. So first lets update domain object with your domains, then you can change ports if needed. After that you will need to update the rethinkDB object with your own RethinkDB credentials.

```js
const domain = {
  production: 'CHANGE ME', //Change to your production domain
  development: 'CHANGE ME', //Change to your development domain
  localhost: 'localhost:8085',
}[process.env.NODE_ENV]

module.exports = {
	port: { //Change these to what you want
		production: 8123,
		development: 8124,
		localhost: 8124,
	}[process.env.NODE_ENV],
	maxSpam: 100,
	rethinkDB: {
		host: 'localhost',
		port: 28015,
		db: {
			production: 'lootvgo', //Change these to what you want the DB to be named.
			development: 'lootvgo_dev',
			localhost: 'lootvgo_dev',
		}[process.env.NODE_ENV],
		user: 'admin',
		password: {
			production: '',
			development: '',
			localhost: ''
		}[process.env.NODE_ENV],
		silent: true,
	},
	...
}
```

Once that's all done, lets setup our tables that are needed to run the site! This is where you may run into some issues with RethinkDB not being configured properly.

Inside the backend directory you will need to run the following command
```
npm run db-setup
```

Alright now that we have setup the DB and all the tables. We can look at running the app for the first time. It won't work properly yet, we will need to further update the config. So all you will need to do is go through the config and update all the commented areas.

There are some spots that you will need to run some request to OPSkins API OAuth with you API key to register a OAuth client. It will tell you what do in those docs.

Once you have completely updated the config, this is the time we get to fire up the app.
```
WINDOWS - npm run start-windows
LINUX - npm run start
```

That will be it for the backend. I would suggest to deploy this to a server with domain as the backend can be finicky.

So assuming that the backend is running its time to get the frontend up and running. This is a pretty straight forward process.

### Frontend Install

So now onto the getting the frontend working. First we need to move directories to /frontend. Then we will need to run this command.
```
npm install
```

After that's all done we can run the command to get it running.
```
npm run start
```

Then it will fire right up, and open a tab in your browser showing the site!

Just in case it doesn't the URL is: http:localhost:8085

## Deployment

### Backend Deployment

When you go to run the backend in production you will run:
```
npm run start-production
```

This will run the app with NODE_ENV=production, thus using the production configs!

### Frontend Deployment

To deploy the frontend isn't very hard, you will need to have some know how on Apache or Nginx web servers.

First command you will need to run is npm run build, this will build the frontend and save it in /dist.
```
npm run build
```

**Then**

![](https://i.gyazo.com/72552491525e1c9fc45f70937951dc92.png)

```
Move files from /dist to where they can be served over HTTP
```

**Note: index.html in dist, needs to be served over HTTP for it to work properly**

![](https://i.gyazo.com/2926231f2db45bea175a843a54fcdbb4.png)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
