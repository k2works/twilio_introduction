Twilio入門
===================

# 目的 #
HerokuにTwilioアプリケーションをデプロイする

# 前提 #
| ソフトウェア   | バージョン   | 備考        |
|:---------------|:-------------|:------------|
| OS X           |10.8.5        |             |
| ruby           |1.9.3-p392    |             |
| rvm            |1.24.0        |             |
| heroku-toolbelt   |3.1.1      |             |

+ [Herokuにサインアップしている](https://id.heroku.com/signup/devcenter)
+ [Heroku Toolbeltをインストールしている](https://toolbelt.heroku.com/)

# 構成 #
+ [セットアップ](#chap1)
+ [ログイン](#chap2)
+ [アプリケーションのデプロイ](#chap3)

# 詳細 #

## <a name="chap1">セットアップ ##

    $ rvm use ruby-1.9.3-p392
    $ rvm gemset create heroku
    $ rvm use ruby-1.9.3-p392@heroku
    $ gem install bundler
    $ bundle init
    $ bundle

## <a name="chap2">ログイン ##

    $ heroku login

## <a name="chap3">アプリケーションのデプロイ ##

### アプリケーションの作成 ###
+ [twiml-quickstart.rb](twiml-quickstart.rb)

        require 'sinatra'
        require 'twilio-ruby'

        get '/hello-monkey' do
          Twilio::TwiML::Response.new do |r|    
            r.Say 'Hello Monkey'
          end.text
        end

### Gemfileの作成 ###
+ [Gemfile](Gemfile)

        source "https://rubygems.org"

        ruby "1.9.3"
        gem 'sinatra'
        gem 'twilio-ruby'

+ bundle installを実行
    
### Procfileの作成 ###

+ [Procfile](Procfile)

        web: bundle exec ruby web.rb -p $PORT

+ ローカルで動作を確認する

        $ foreman start

### Gitレポジトリの作成 ###

    $ git add .
    $ git commit -a -m "セットアップ"

### Herokuにデプロイ ###

    $ heroku create
    $ git push heroku master
    Fetching repository, done.
    Counting objects: 15, done.
    Compressing objects: 100% (10/10), done.
    Writing objects: 100% (10/10), 2.04 KiB, done.
    Total 10 (delta 3), reused 0 (delta 0)

    -----> Ruby app detected
    -----> Compiling Ruby/Rack
    -----> Using Ruby version: ruby-1.9.3
    -----> Installing dependencies using Bundler version 1.3.2
           Running: bundle install --without development:test --path vendor/bundle --binstubs vendor/bundle/bin --deployment
           Fetching gem metadata from https://rubygems.org/..........
           Fetching gem metadata from https://rubygems.org/..
           Installing builder (3.2.2)
           Installing multi_json (1.8.2)
           Installing jwt (0.1.8)
           Using rack (1.5.2)
           Using rack-protection (1.5.1)
           Using tilt (1.4.1)
           Using sinatra (1.4.4)
           Installing twilio-ruby (3.11.4)
           Using bundler (1.3.2)
           Your bundle is complete! It was installed into ./vendor/bundle
           Bundle completed (6.49s)
           Cleaning up the bundler cache.
    -----> Discovering process types
           Procfile declares types -> web
           Default types for Ruby  -> console, rake

    -----> Compressing... done, 11.6MB
    -----> Launching... done, v4
           http://shrouded-wave-8087.herokuapp.com deployed to Heroku

    To git@heroku.com:shrouded-wave-8087.git
       2b1ae01..8fbd12f  master -> master

### アプリケーションの確認 ###

    $ heroku ps:scale web=1
    $ Scaling dynos... done, now running web at 1:1X.

    $ heroku ps
    === web (1X): `bundle exec ruby web.rb -p $PORT`
    web.1: up 2013/12/12 11:01:48 (~ 7m ago)

    $ heroku open

# 参照 #

[Heroku](https://www.heroku.com/)

[Twilio Docs - クイックスタート](https://jp.twilio.com/docs/quickstart)
