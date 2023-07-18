# Rails7 + React + Tailwind CSS + Docker


## Project folder

```
mkdir foldername && cd foldername
```

## Create .ruby-gemset & .ruby-version

```
echo "rails7" >> .ruby-gemset
echo "ruby-3.2.2" >> .ruby-version
```


## New Rails
```
rails new . -d postgresql -a propshaft --css=tailwind --javascript=esbuild --skip-action-mailer --skip-action-mailbox --skip-action-cable
```

## Modify Gemfile 
```
# A Ruby gem to load environment variables from `.env`.
gem 'dotenv-rails'
```

## Create .env file

```
# ./env

POSTGRES_USER='postgres'
POSTGRES_PASSWORD='railspsql'

POSTGRES_PORT='5600'
POSTGRES_HOST='localhost'

POSTGRES_DB='BootstrapRails_production'
POSTGRES_DEV_DB='BootstrapRails_development'
POSTGRES_TEST_DB='BootstrapRails_test'
```


## Modify database.yml file
file path ‘/config/database.yml’

```
default: &default
  adapter: postgresql
  encoding: unicode
  
  username: <%= ENV['POSTGRES_USER'] %>
  password: <%= ENV['POSTGRES_PASSWORD'] %>
  host: <%= ENV['POSTGRES_HOST'] %>
  port: <%= ENV['POSTGRES_PORT'] %>

  # For details on connection pooling, see Rails configuration guide
  # https://guides.rubyonrails.org/configuring.html#database-pooling
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  timeout: 5000

development:
  <<: *default
  database: <%= ENV['POSTGRES_DEV_DB']%>
  
test:
  <<: *default
  database: <%= ENV['POSTGRES_TEST_DB']%>

production:
  <<: *default
  database: <%= ENV['POSTGRES_DB']%>
  # username: BootstrapRails
  # password: <%= ENV["BOOTSTRAPRAILS_DATABASE_PASSWORD"] %>
```

## Update bundle and database
```
bundle update
bin/rails db:create
bin/rails db:migrate
```

## Add React libs
```
yarn add react react-dom @types/react @types/react-dom typescript
```

## Create tsconfig.json in Rails root folder

tsconfig.json files in Rails
```
{
  "compilerOptions": {
    "module": "commonjs",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true,
    "jsx": "react",
  }
}
```