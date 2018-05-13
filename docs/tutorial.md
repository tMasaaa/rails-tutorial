# note
理解度確認、疑問
- Ruby gemの選定方法
- bundle install, bundle updateの実行方法
- ローカルwebサーバが動かなくなった時の再起動方法
- MVC
- REST
- ジェネレータ
- マイグレーション
- ルーティング
- ERB
- モックアップ
- テスト駆動開発TDD
- 統合テスト
- DSL ドメイン固有言語
- MVC分からん(他のと比較すればいいのかな)
- ルーティングは何をしているのか？: コントローラにブラウザからのリクエストを振り分ける役割
- gemfileのそれぞれのやつらの意味
```
source 'https://rubygems.org'

git_source(:github) do |repo_name|
  repo_name = "#{repo_name}/#{repo_name}" unless repo_name.include?("/")
  "https://github.com/#{repo_name}.git"
end

gem 'rails', '5.1.4'
gem 'puma', '3.9.1'
gem 'sass-rails', '5.0.6'
gem 'uglifier', '3.2.0'
gem 'coffee-rails', '4.2.2'
gem 'jquery-rails', '4.3.1'
gem 'turbolinks', '5.0.1'
gem 'jbuilder', '2.7.0'

group :development, :test do
  gem 'sqlite3', '1.3.13'
  gem 'byebug', '9.0.6', platforms: mri
end

group :development do
  gem 'web-console', '3.5.1'
  gem 'listen', '3.1.5'
  gem 'spring', '2.0.2'
  gem 'spring-watcher-listen', '2.0.1'
end

group :production do
  gem 'pg', '0.20.0'
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
```
- モデル設計がしっくりこない、何がわかってないのかわからない
- migrateとは？
- resourceとは？コンポーネントとの違いはなに？(コード化されているということ？): リソースとは、HTTPプロトコル経由で自由にCURDできる、分類されたデータ群のこと。(コンポーネントを扱いやすい形に変換したもの)
- 本筋ではないが、アドレスバーにURLを入力してどんなプロトコルでどこを通ってroutes.rbが処理するに至るのかその過程が知りたい

Roadmap
- hello app(1)
- toy app(2): scaffold
    - Railsアプリの構造
    - RESTアーキテクチャ
- sample app(3-14):like twitter

困ったときは？
- https://railsguides.jp/ Railsガイド
- https://railstutorial.jp/help Help

Unixコマンド
- ls -a: dotfile含めて表示
- ls -l: 権限含めて表示
- mv <移動元> <移動先>: ファイル移動
- mv <現在の名前> <変更後の名前>: リネーム
- cp <コピー元> <コピー先>: ファイルコピー

Rails applicationのディレクトリ構造
- app/assets: CSS,JS,画像などのアセット
- lib/assets: libraryで使うCSS,JS,画像などのアセット
- public/: エラーページなど、一般に直接公開するデータ
- vendor/: サードパーティのプラグイン、gem
- Rakefile: rakeコマンドで使えるタスク(makeっぽい、タスク実行)
- Gemfile: Gemの定義ファイル

gem version 意味
> 通常はがっちり固定させる(gemのバージョンが少しでも違うとエラー吐くことがあるため)
- ">=1.0.0" 1.0.0以上であれば、最新バージョンをインストール
- "~>1.0.0" 1.0.xの最新版をインストール

コマンド一覧
- サーバー立ち上げ
```
rails new
bundle update
bundle install
rails server # server立ち上がる
```

- 現在あるコントローラの確認
```
ls app/controllers/*_controller.rb
```

- 本番用のgemを除いたローカルgemのインストール
```
bundle install --without production
```

- rails scaffold
```
# rails generate scaffold [option]
rails generate scaffold User name:string email:string
```

- git
```
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/tMasaaa/rails_toy_app.git
git push -u origin master
```

# 1章
- ハードスキル(操作方法:定型的)、ソフトスキル(デバッグ:定型化しにくい)の両方が必要。
- scaffoldは便利だけど、それだけに頼っていては実力がつかないのでsample appでは使わない。
- bundlerはrailsによって自動的に実行される。(bundle install)
- app/以下、models, views, controllersがある(MVC)
- MVC: アーキテクチャパターン(システム全体の基本的な構造のパターン)のひとつ
- コントローラとブラウザがリクエスト/HTMLの送り返しをする。
- config/routes.rb でルーティングを行う

## 演習
1.gemはどこか
- https://rubygems.org/

2.Rails version
- https://rubyonrails.org/
- 5.2.0(2018/4/9)

3.download数
- GitHubのフォークの数？でもそれより絶対多いはず
- わからん

---

1.ruby ver
- 2.5.0

2.rails ver
- 5.1.4

---

1.2.アクション内の文字変更するだけ

3.アクション追加とルートルーティング変更
- app/controllers/application_controller.rb
```
class ApplicationController < ActionController::Base
  protect_from_forgery with: :exception

  def hello
    render html: "¡Hola, mundo!"
  end

  def goodbye
    render html: "goobye, world!!"
  end
end
```

- config/routes.rb
```
Rails.application.routes.draw do
  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
  root 'application#goodbye'

end
```

# 2章
- error
```
[!] There was an error parsing `Gemfile`: Undefined local variable or method `mri' for Gemfile. Bundler cannot continue.

 #  from /home/vagrant/rails-tutorial/project/toy_app/Gemfile:19
 #  -------------------------------------------
 #    gem 'sqlite3', '1.3.13'
 >    gem 'byebug', '9.0.6', platforms: mri
 #  end
 #  -------------------------------------------
```
- mriの前の":"忘れでした

```
An error occurred while installing pg (0.20.0), and
Bundler cannot continue.
Make sure that `gem install pg -v '0.20.0'` succeeds before
bundling.
```
- 原因不明。
```
bundle install --without production
bundle update
bundle install --without production
```
でうまくいった。

- ユーザーのモデル設計
  - users: table
  - id/name/email: column
- マイクロポストのモデル設計
  - microposts
  - id/content/user_id
- ユーザー用のモデル＋Webインターフェイス→Usersリソース(ユーザーがオブジェクトとして扱えるようになる)
- このUsersリソースはscaffold generatorで生成する
- なんだかよくわからない。いわれたままに動かすとユーザーの生成、edit、destroyができた。
- MVCの挙動
- /userにあるindexページをブラウザで開く

1.ブラウザ→Rails serverへURL:/usersへのリクエスト
2.RailsのルーターがリクエストをUserコントローラ内のindexアクションに割り当てる
3.indexアクションの実行→UserモデルにUser.all(すべてのユーザーを取り出せ)問い合わせ
4.Userモデルは問い合わせを受けてUser.all
5.Userモデル→コントローラ: ユーザー一覧
6.Usersコントローラ: ユーザー一覧を@users変数に保存。indexビューに渡す
7.indexビュー起動。ERB実行、HTML生成(レンダリング)
8.ビュー→コントローラ: HTMLの受け渡し。コントローラ→ブラウザ: HTMLの受け渡し

- リクエストはアドレスバーにURLを入力したりリンクをクリックしたときに発生
- ディスパッチ: URLに基づいてコントローラのアクションが割り当てられること
- ルーティング rootの後にapp/[any]_controller.rbの[any]を書く。すると、root(/)にアクセスしたときにどのアクションを起こすのか決められる
routes.rb
```
resources :users
root 'users#index'
```
これは、users_controller.rbにルーティングしますよ、そしてindexアクションを起こしますよという意味。
- アクションはページ表示だけでなく、ただデータベースの操作するだけのものもある。
- RESTはアーキテクチャのひとつ。
- RailsのRESTは、コンポーネントをリソースとしてモデル化することを指す。リソースは、CRUD操作とHTTP requestメソッド(GET/POST/PATCH/DELETE)にたいおう。 
- routes.rb:resources.usersはなにしてるの？
  - resourcesで定義すると、index,show,new,create,edit,update,destroyの七つのルーティングが定義される
  - resourceでまとめてドン！はあまりやらない
  - デフォルト動作がある。設定より規約の精神(rails)裏のルールがあるので、気にせず先に進んでOK
- ここは継承で多くの機能が備わっている(裏のルールってこれ？)
```
@users = User.all
```
これに対し、RubyライブラリのActive RecordによってUser.allリクエストに対し、DB上のすべてのユーザーを返すことができる。

## 演習
1.User Createで文字のCSS
- p#noticeが緑になってた(assetにあるCSS)
- 更新するとp#noticeのcontentがなくなった

2.emailなし
- 名前だけになる

3.invalid email address
- 普通に入力できる

4.消すときの挙動
- 変わらない。Are you sure?からのUser was successfully destroyedになる

1./users/1/editについて
- def editは何も書かれていないが、ApplicationControllerクラス(これは空)からUsersControllerに継承し、フィルタbefore_actionでonly[:edit]しているので、そのbefore_actionでかけられたフィルターを実行する。
- アクションの実行前にset_userを行う→editアクション実施前にset_user

2.databaseからユーザー情報取得しているコード
- editで行っているset_user
```
def set_user
  @user = User.find(params[:id])
end
```

3.editページ
- views/users/edit.html.erb

