# codr.academy-step-by-step-guide
A step-by-step guide on how codr.academy was built


## Create New
`rails new codr.academy -d postgresql`

## Config Database

Update config/database.yml

```
default: &default
  host: localhost
  port: 5432
  username: <%= Rails.application.credentials.dig(:db, :username) %>
  password: <%= Rails.application.credentials.dig(:db, :password) %>
```

`EDITOR="nano" rails credentials:edit`

```
db:
  username: [username]
  password: [password]
```

- `rails db:setup`
- `rails db:migrate`

## Home Page with Title Bar

`rails g controller HomePage index`

config/routes.rb

```
root 'home_page#index'
```

cp irvan-smith-5eBW5GomfhY-unsplash to app/assets/images

app/views/layouts/application.html.erb

```
    <h1>codr.academy</h1>
```

app/assets/stylesheets/application.css

```
@import url('https://fonts.googleapis.com/css2?family=Anonymous+Pro:wght@700&display=swap');

body {
    margin: 0;
}

h1 {
    background-image: url("irvan-smith-5eBW5GomfhY-unsplash.jpg"); /* Photo by Irvan Smith on Unsplash */
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    color: white;
    font-family: 'Anonymous Pro', monospace;
    text-shadow: 0px 0px 1rem orange;
    font-size: 3.5rem;
    margin: 1rem 0rem;
    padding: 1rem 3rem;
}
```

app/views/home_page/index.html.erb

```
<h2>HomePage#index</h2>
```

## Deploy to Heroku

- `brew tap heroku/brew && brew install heroku `
- `heroku autocomplete`
- `printf "$(heroku autocomplete:script zsh)" >> ~/.zshrc; source ~/.zshrc`
- `compaudit -D`
- `heroku create codr.academy` 
- `git push heroku master`

### Fix missing images

config/environments/production.rb

```
config.assets.initialize_on_precompile = false
  config.assets.compile = true
```

## VerbalMark normalization

```ruby
/^([a-z]{1,30}){1}([]{1}[a-z]{1,30}){,1}([]{1}[a-z]{1,30}){,1}\Z/
```

<!-- (lowercase, snake_case, at most 3 words sperated by underscore '_', each word at most 30 letters) -->