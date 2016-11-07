# Cursory Setup Instructions w/ Bash History

## plain-text instructions

```
@@@@@@@@@@@@@@@@@
@  BASIC SETUP  @
@@@@@@@@@@@@@@@@@

1. put the following in .railsrc

-d postgresql #Use postgres
-T #Skip Test-Unit
--skip-turbolinks #Skip turbolinks gem
-B #Skip bundle install upon rails new

2. rails new YOURPROJECTNAME

3. comment out coffee-rails gem

4. include the following gems 

  ######################
  # non-rails-new gems #
  ######################

  # Use devise for user auth
  gem 'devise'

  # Formatters for ease of debugging
  gem 'awesome_print'
  gem 'better_errors'
  gem 'binding_of_caller'

  # Bootstrap sass gems
  gem 'bootstrap-sass', '~> 3.3.6'

  # Faker for seeding data
  gem 'faker' 

5. bundle install

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@  OPTIONAL BOOTSTRAP SETUP  @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

* go to assets/javascripts/application.js and make sure you require bootstrap-sprockets like so:

  //= require jquery
  //= require bootstrap-sprockets
  //= require jquery_ujs

  so that it appears in that order

* go to assets/stylesheets

  * add a file called main.scss, and put the following code inside:

  @import "bootstrap-sprockets";
  @import "bootstrap";

@@@@@@@@@@@@@@@@@
@  GENERATIONS  @
@@@@@@@@@@@@@@@@@

1. implement user registration and authentication
  See: https://github.com/plataformatec/devise
  can specify attributes other than devise defaults by adding options to rails g devise model (see line 509)

2. for each of your resources, type rails g model YOURRESOURCE
  feel free to declare your resource's attributes in this step, e.g.
  rails g model park name:string description:text creator:references city:references
  HOWEVER when doing this, don't forget to take out the foreign_key options in the migration files for the references columns (see lines 513 and 514)

3. for each of your resources that you require a controller for, type rails g controller YOURRESOURCE
  this will create a view folder for each controller you make
  if you fuck up, you can destroy a controller and all associated files by doing rails destroy controller NAME

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@ OPTIONAL DEVISE CUSTOMIZATION @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

* change minimum password length
  Go to config/initializers/devise.rb
  Change the 6 in config.password_length = 6..128

* permit additional parameters upon registration
  See: https://github.com/plataformatec/devise#strong-parameters

  Basically, in controllers/application_controller.rb, under protected, add:

  def configure_permitted_parameters
    devise_parameter_sanitizer.permit(:sign_up, keys: [:username])
  end

  and above protected, add:

  before_action :configure_permitted_parameters, if: :devise_controller?

* permit additional parameters upon update

  Basically, in controllers/application_controller.rb, under protected, add:

  def upon_update_permitted_parameters
    devise_parameter_sanitizer.permit(:account_update, keys: [:username, :biography])
  end

  and above protected, add:

  before_action :upon_update_permitted_parameters, if: :devise_controller?

* edit the view so that the user can enter these parameters upon registrations
  See: https://github.com/plataformatec/devise#configuring-views
  Go to views/users/registrations/new.html.erb

* add errors upon login failure (after configuring views)
  See: http://stackoverflow.com/a/35376583/7015790
  Go to views/users/registrations/sessions/new.html.erb

@@@@@@@@@@@@@@@@@@@@@@
@ ROUTES AND ACTIONS @
@@@@@@@@@@@@@@@@@@@@@@

* for custom root, type root 'CONTROLLER#ACTION'

* to implement routes the rails way:
  resources :RESOURCE
  this will give you all seven routes

  if you want to implement only certain routes, do (e.g.):
  resources :RESOURCE, only: [:index, :show]

  if you want to implement all routes except some, do (e.g.):
  resources :RESOURCE, except: [:index, :show]
 
  NOTE: the restriction name must match the controller action name, not the verb name from rails routes.
  e.g. except: :delete IS WRONG! you do except: :destroy, since the action in the controller is called destroy
  Thanks Ilaria :D

* to implement nested routes the rails way:
  resources :RESOURCE do
    resources :NESTEDRESOURCE
  end

  this will give you all seven routes for both RESOURCE and NESTEDRESOURCE. you can further restrict by doing (e.g.):

  resources :cities, only: :index do 
    resources :parks, except: [:index, :show]
  end
```

## bash history

NOT SHOWN: `rails routes` was run many times between these

```
503  rails new parkr
505  cd parkr/
506  subl .
507  bundle install
508  rails g devise:install
509  rails g devise user username:string bio:text
512  rails g model city name:string
513  rails g model parks name:string description:text creator:references city:references
514  rails g model review title:string body:text reviewer:references park:references
516  rails db:create
517  rails db:migrate
522  git init
523  git add .
524  git commit -m "Initial commit with models and migrations"
525  git remote add origin https://github.com/parkyngj/parkr.git
526  git push origin master
527  gcob controllers-views-init
537  rails g controller cities
538  rails g controller parks
539  rails g controller reviews
541  rails g controller users
542  git add .
543  git commit -m "Generate controllers for users, cities, parks, reviews"
544  gcob routes-actions-init
507  rails g devise:views users
511  git commit -m "Implement username sanitization for user registration"
504  git commit -m "Make basic routes, actions, views for retrieving info from db"
```
