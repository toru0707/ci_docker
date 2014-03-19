CI環境構築プロジェクト

# Gitlabサーバ

user: admin@local.host
pass: 5iveL!fe

# こんなエラーが出た時は

## Q: gitlabのインストール中に以下のエラーが発生する

``` 
================================================================================
Error executing action `run` on resource 'execute[gitlab-bundle-install]'
================================================================================


Mixlib::ShellOut::ShellCommandFailed
------------------------------------
Expected process to exit with [0], but received '17'
---- Begin output of /srv/git/bin/bundle install --deployment --without development test postgres aws && touch /srv/git/gitlab/vendor/bundle/.success ----
STDOUT: Fetching source index from https://rubygems.org/
```

## A: httpsの通信が出来ていないので、gemの取得先をhttpにしましょう

具体的には、以下の様にhttpスキーマでgemfileを取得するように修正を加えます。

/srv/git/gitlab/Gemfile
```
source "http://rubygems.org"
```
