## Getting Started Locally

Create an Amazon S3 bucket. Copying settings_example.py to settings.py,
configure the Heroku application with your bucket name and AWS access
credentials.

  % cp settings_example.py settings.py

Add the following CORS configuration to the bucket.

  <?xml version="1.0" encoding="UTF-8"?>
  <CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
      <CORSRule>
          <AllowedOrigin>*</AllowedOrigin>
          <AllowedMethod>GET</AllowedMethod>
          <AllowedMethod>POST</AllowedMethod>
          <AllowedMethod>PUT</AllowedMethod>
          <AllowedHeader>x-requested-with</AllowedHeader>
          <AllowedHeader>*</AllowedHeader>
      </CORSRule>
      <CORSRule>
          <AllowedOrigin>http://localhost:5000</AllowedOrigin>
          <AllowedMethod>GET</AllowedMethod>
          <AllowedMethod>POST</AllowedMethod>
          <AllowedMethod>PUT</AllowedMethod>
      </CORSRule>
  </CORSConfiguration>

## Getting Started on Heroku

Create a Heroku application. Configure the application with a title, which
will be displayed in the header and title bar, and a subtitle, which will
be displayed below the header.

  % heroku create eclubfront
  % git push heroku master
  % heroku config:set SITE_TITLE='E-Club Front' --app=eclubfront
  % heroku config:set SITE_SUBTITLE='front page' --app=eclubfront

Set up the database and fixtures. Make sure to promote the specific database
URL that Heroku created for you.

  % heroku addons:add heroku-postgresql:dev --app=eclubfront
  % heroku pg:promote HEROKU_POSTGRESQL_VIOLET_URL --app=eclubfront
  % heroku pg:psql --app=eclubfront < schema.sql
  % heroku pg:psql --app=eclubfront < fixtures.sql

Create a random secret key of sufficient length (32 alphanumeric characters
should be enough for just about anyone).

  % heroku config:set SECRET_KEY='11235813' --app=eclubfront

Create an Amazon S3 bucket. Go to https://aws.amazon.com/s3/, and click on
manage, then Amazon S3, then create a bucket with the name of your site.
Configure the Heroku application with your bucket name and AWS access credentials.

  % heroku config:set AWS_ACCESS_KEY_ID='AKIAJVSRYJVERQRL54HA'--app=eclubfront
  % heroku config:set AWS_SECRET_ACCESS_KEY='m7KknJU38R0vnRgzP/QtmJE1Tsk0q54toZ4+4xzh' --app=eclubfront
  % heroku config:set S3_BUCKET='eclubucket' --app=eclubfront

Add a CORS configuration to the bucket, replacing localhost:5000 with the
domain your site will be hosted on. (See the first section of this guide.)

Set up a new user. [TODO]

Set up a background for the home page. You can link to an existing image, such
as a cover photo for another collection, either directly on on your server.

  % heroku config:set FRONT_BACKGROUND='http://yourapp.amazon.com/...' --app=yourapp
  % heroku config:set FRONT_BACKGROUND='/collection/some-collection/cover' --app=yourapp