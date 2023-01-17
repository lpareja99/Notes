## How to add Bootstrap to an RoR app
 
---
 *Ruby version: 3*

 *Rails version: 7*

---

Bootstrap sass gem page: [link](https://github.com/twbs/bootstrap-sass)

Add the following gem to your gemfile above the gem 'sass-rails':

    gem 'bootstrap-sass', '~> 3.3.5'

To install the gem to your app run:

    bundle install --without production

Create a file called `custom.css.scss` under `app/assets/stylesheets` folder and add the following lines to the file:

    @import "bootstrap-sprockets";
    @import "bootstrap";

Add the following line under  `app/assets/application.js` add to teh bottom of the file:

    //= require jquery_ujs:
    //= require bootstrap-sprockets

Reboot the project in the console

