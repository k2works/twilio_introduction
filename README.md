Heroku入門
===================

# 目的 #
HerokuにRubyアプリケーションをでプロイする

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
+ [web.rb](web.rb)

        require 'sinatra'
    
        get '/' do
            "Hello, world"
        end


### Gemfileの作成 ###
+ [Gemfile](Gemfile)

        source "https://rubygems.org"

        ruby "1.9.3"
        gem 'sinatra' 

+ bundle installを実行
    
### Procfileの作成 ###

+ [Procfile](Procfile)

        web: bundle exec ruby web.rb -p $PORT

+ Rack appから直接デプロイする場合はconfig.ruを用意してProcfileは以下の内容になる。

        web: bundle exec rackup config.ru -p $PORT

+ ローカルで動作を確認する

        $ foreman start

### Gitレポジトリの作成 ###


### Herokuにデプロイ ###

### アプリケーションの確認 ###

### ログを確認する ###

### コンソール ###

### Rake ###

### データベースを使う ###

# 参照 #

[Heroku](https://www.heroku.com/)

[Getting Started with Heroku](https://devcenter.heroku.com/articles/quickstart)

[Getting Started with Ruby on Heroku](https://devcenter.heroku.com/articles/getting-started-with-ruby)
