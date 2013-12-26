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
    $ git commit -a -m "init"

### Herokuにデプロイ ###

    $ heroku create
    $ git push heroku master

### アプリケーションの確認 ###

    $ heroku ps:scale web=1
    $ Scaling dynos... done, now running web at 1:1X.

    $ heroku ps
    === web (1X): `bundle exec ruby web.rb -p $PORT`
    web.1: up 2013/12/12 11:01:48 (~ 7m ago)

    $ heroku open

# 参照 #

[Heroku](https://www.heroku.com/)
