Creating an app with Rails API backend VueJS frontend, handling CORS and pushing a working app to Heroku.

Working demo app: https://limitless-inlet-24308.herokuapp.com/#/contacts


Create Rails API backend.

Because our Rails app and VueJS app will be hosted on two separate servers, one of the first things we’ll need to handle is Cross-Origin Resource Sharing, (or CORS). Luckily Rails makes this easy to do. Under Config>Initializers you’ll find cors.rb. Comment the existing text out, and add your domain in the Origin and Resource. Add the rack-cors Gem.

Create Vue app that makes axios request for json data from the backend API.

Navigate to backend and create Heroku app.

npm run build in the public folder of the front end. Take the generated dist folder and put it in the public folder of the back end. 

Remember that Heroku works as a git repo. That means that any files you wish to deploy (including your front-end) must be commited to the repo. So you can do this if you want and just use the git push heroku master command to deploy, but I think this is a bad idea because you don’t want front-end builds in your back-end git repo or history.

However, Heroku’s decision to use git was not necessarily one for version-control management. Since you already have a back-end repo, you don’t care about the Heroku repo’s history or state as much. As such, I suggest the following alternative approach, which is the one I use.

Navigate to your back-end and create a new branch.

$ cd ../backend
$ git checkout -b heroku-deploy
$ git add public
$ git commit -m "deploy"
$ git push -f heroku heroku-deploy:master
$ heroku run rake db:migrate
$ git checkout master
$ git branch -D heroku-deploy
$ heroku open

Sources: 
For a full stack app tutorial: https://medium.com/@sfcooper/creating-an-app-with-rails-api-backend-vuejs-frontend-403d2df61dab
For deployment: https://michaelmeli.com/deployment/2017/09/11/deploying-rails-and-vue-to-heroku.html

