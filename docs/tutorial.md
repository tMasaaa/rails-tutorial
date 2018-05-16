# note
理解度
5.2.1 C

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
  - Embedded Ruby 埋め込みRuby
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
- HTTPS化はどうやってするのか？
- 以下の二つの"#"と"/"はどう違うのか？どういうときに#でどういうときに/なのか
```
  get 'static_pages/help'
  root 'application#hello'
```
- テストでshared_folder由来のエラーが出るのを解消する
- 使い方がわかるが、仕組みがわからない状態になっているので何がわからないのかわからない。エラーに遭遇して調べて少しずつ知っていくのだろうか？
- Guardファイルの中身解読
- 「Railsの組み込み関数」「かっこを使わないメソッド呼び出し」「シンボル」「ハッシュ」
- モジュール
- メソッド定義
- 任意のメソッド引数
- コメント
- ローカル変数の割り当て
- 論理値
- 制御フロー
- 文字列の結合
- 戻り値
- interactive rubyとは？どういう仕組みでインタラクティブになっているんだ
- hashを複数宣言しよう！→`a={},b={},c={}`,区切りはRubyでは配列になってしまう。hashを複数宣言するには改行するしかないのかな…？
  - `a={} b={} c={}`これはシンタックスエラーになる。
  - `a,b,c={},{},{}`が正解。
  - `a={};b={};c={}`も正解。`;`で文を区切れる。
- `s = String.new("foobar")`これ、foobarの""で暗黙のリテラルコンストラクタが呼ばれているのか？Stringオブジェクトを生成して、newはいったい何をしているのか？それともこの場合の""はコンストラクタではない？？
  - そもそも、`""`と`String.new`はまったくの別物。前者は文法(メソッドではない。コンパイル時に構文解析で処理される)後者はメソッド(オブジェクトを引数にとり、オブジェクトを返すメソッド)`""`が何やってるのかとか詳しく知りたくなったらRuby処理系の実装コードを読まないといけないかも。
- Rubyってプロトタイプベースじゃないよね？？プロトタイプベースとクラスベースの違いが分からなくなってきた…(一度JSで理解したので復習しないと)
- ブラウザから見たとき、assets/images/rails.pngがassets/rails-83491319.pngになっているのはどういう仕組み？何が起きているのかわからない。
- アセットパイプラインがどういう仕組みになっているのかわからない。どこが指示してどのCSSがどこにまとめられているんだろうか
- HTTPの標準として、リダイレクトの時に完全なURLが要求される→ソースは？
- `get 'help', to: 'static_pages#help'`これは、`get('help', 'to'=>'static_pages#help')`と同じか？ruby,railsの記法に慣れない…
- hoge_urlとhoge_pathは組み込みなのか？
- これいちいちcontrollerとかviewとか更新する必要があってつらいんだけどリスト作ったほうがいいな？

Roadmap
- hello app(1)
- toy app(2): scaffold
    - Railsアプリの構造
    - RESTアーキテクチャ
- sample app(3-14):like twitter
  - 静的なページ
  - 自動化テスト

困ったときは？
- https://railsguides.jp/ Railsガイド
- https://railstutorial.jp/help Help
- http://ruby-doc.org/ API
- https://docs.ruby-lang.org/ja/ ja API
- https://docs.ruby-lang.org/ja/search/ search ja


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
# rails db:migrate
rails generate scaffold User name:string email:string
rails db:migrate
```

- rails console
```
rails console
exit
```

- 短縮形
```
rails server # rails s
rails console # rails c
rails generate # rails g
rails test # rails t
bundle install # bundle
```

- 失敗したとき
```
# generate
rails destroy controller <name>
# migrate
rails db:rollback
rails db:migrate VERSION=0 # 最初の状態に戻す
```

- git
```
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/tMasaaa/rails_toy_app.git
git push -u origin master
```
- git checkout 新しく作る
```
git checkout -b <name>
```

- test guideline
- アプリケーションのコードよりテストコードのほうが短くシンプル→先にテストを書く
- 仕様がまだ→後でテストを書く
- セキュリティ周りのエラー、課題→先にテスト
- バグを見つけたら→先にテスト
- HTMLなど、すぐ変更しそうなコード→後でテスト
- リファクタリングする→先にテスト
> 現実的には、最初にコントローラ、モデルのテスト→統合テスト(モデル/ビュー/コントローラにまたがる機能テスト)を書く。
> 統合テストはユーザーがwebブラウザでやり取りする操作をシュミレートできる

- Unixのプロセス
- `ps aux` : システム上で動いているプロセスの確認
- `ps aux | grep spring` : spring関連のを表示
- `kill [killcode] [pid]` : プロセスのkill
- `spring stop` : springプロセスを停止
- `pkill -15 -f spring` : 一括

- curl
```

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
- Usersリソースの欠点:
- 課題でもあったように、テキトーな名前とかが通ってしまう。また、認証が行われていないなど他にもよくない点がある。
- REST構造は同じ。リソースに同じように反映されている。
- modelのとこからvalidatesで指定→文字数制限できる(簡単)
- 異なるデータモデル同士の関連付けはRailsの強力な機能(ここでは、UserモデルとMicropostモデル)
- rails console:
- オブジェクト指向っぽくいける
- モデルの継承構造
- User < ApplicationRecord < ActiveRecord::Base
- Micropost < ApplicationRecord < ActiveRecord::Base
- ActiveRecord::Baseは、RailsのActive Recordというライブラリが提供しているコントローラの基本クラス
- コントローラの継承構造
- UsersController < ApplicationController < ActionController::Base
- MicropostsController < ApplicationController < ActionController::Base
- ActionController::BaseはRailsのAction Packというライブラリが提供しているコントローラの基本クラス
- まとめ
- RailsのRESTには、URLセット、コントローラアクションが含まれる
- dataのvalidationで、データモデルの属性の値に制限をかけられる
- 組み込み関数が多い
- コンソールをつかうとコマンドラインから扱えてちょっと確かめる分にはいちいちGUIやんなくていいので楽

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

1.p#noticeの挙動
- リロードで消える

2.空作成
- できる

3.141文字以上のマイクロポスト
- できる

4.削除: やる

1.制限後のふるまい
- エラーが出る

2.CSSは
- #error_explanation,#field_with_errorsが出現
- リロードするとmicroposts/に戻る

1.showページ編集し、ユーザーの最初のマイクロポストを表示
```
<p>
  <strong>Micropost:</strong>
  <%= @user.microposts.first.content %>
</p>
```

2.contentが存在しているか検証
- やる

3.nameとemailが存在していることを検証
```
    validates :name, presence: true
    validates :email, presence: true
```
1.ActionController::base where?
- app/controllers/application_controller.rb

2.ActiveRecord::Base where?
- app/models/application_record.rb

# 3章
- まずdef helloとかして確かめるのが大事。
- ずっとmasterブランチではなく、その都度topicブランチで作業するのが良い習慣。
- rails generate では、コントローラ名とアクション名を決められる
- controller内のgetはHTTPのgetと結びついている。
```
get 'static_pages/help'
```
- RailsはHTTPの4つの操作(GET/POST/PATCH/DELETE)に対応している。PATCH,DELETEはサーバー上の操作に対応していて、ブラウザがネイティブには対応していない。しかし。Railsはこれらのリクエストを送信しているかのように見せかける技術を使って、PATCH,DELETEをサポートできるようになった。
- RESTはあらゆるものに対して最適ではない(ref.静的なページの集合)
- 下のコードはRubyだと何も実行しないメソッド。しかしRailsでは、継承によりデフォルトの動作が決まっている。def以下実行→ビューを出力という流れなので、今回はhome.html.erbビューが出力されるだけとなる。
```
  def home
  end
```
- まとめ: ブラウザがURLでGETリクエストを送る→routes.rbが受け取り、URLに対応するcontrollerが、def以下のメソッド実行し、その後ビューを出力。ブラウザにhtmlが表示される。
- テストから始める
- 変更を行うときは「自動化テスト」を作成しよう
- テスト作成が上達すれば、バグを追う時間が減る→全体でみると、開発速度が上がる。
- テストには時間がかかる
- Springサーバーを起動してRails環境を事前読み込みするのに時間がかかる
- Rubyそのものの起動に時間がかかる
- テスト失敗をRED, 成功をGREENと表す
- まずAboutページ用に失敗するテストを書く→RED→Aboutページを書く→GREEN
- [error] rails test で`3 runs, 2 assertions, 0 failures, 1 errors, 0 skips`が出てこない
- rails test -dで出てくる
- 謎のエラーが出る(guestとhostでファイル共有しているのが原因？)
```
[vagrant@localhost sample_app]$ rails test -d
Running via Spring preloader in process 14913
rails aborted!
ActiveRecord::Tasks::DatabaseAlreadyExists: ActiveRecord::Tasks::DatabaseAlreadyExists
/home/vagrant/rails-tutorial/project/sample_app/bin/rails:9:in `require'
/home/vagrant/rails-tutorial/project/sample_app/bin/rails:9:in `<top (required)>'
/home/vagrant/rails-tutorial/project/sample_app/bin/spring:15:in `require'
/home/vagrant/rails-tutorial/project/sample_app/bin/spring:15:in `<top (required)>'
bin/rails:3:in `load'
bin/rails:3:in `<main>'

Caused by:
Errno::ETXTBSY: Text file busy @ apply2files - /home/vagrant/rails-tutorial/project/sample_app/db/test.sqlite3
/home/vagrant/rails-tutorial/project/sample_app/bin/rails:9:in `require'
/home/vagrant/rails-tutorial/project/sample_app/bin/rails:9:in `<top (required)>'
/home/vagrant/rails-tutorial/project/sample_app/bin/spring:15:in `require'
/home/vagrant/rails-tutorial/project/sample_app/bin/spring:15:in `<top (required)>'
bin/rails:3:in `load'
bin/rails:3:in `<main>'
Tasks: TOP => db:test:load => db:test:purge
(See full trace by running task with --trace)
Run options: -d --seed 49899

# Running:

Run options: -d --seed 49899

# Running:

..EE..

Finished in 3.358941s, 0.8931 runs/s, 0.5954 assertions/s.

  1) Error:
StaticPagesControllerTest#test_should_get_about:
NameError: undefined local variable or method `static_pages_about_url' for #<StaticPagesControllerTest:0x00007f2f77e33db8>
    test/controllers/static_pages_controller_test.rb:15:in `block in <class:StaticPagesControllerTest>'

3 runs, 2 assertions, 0 failures, 1 errors, 0 skips



Finished in 3.603273s, 0.8326 runs/s, 0.5551 assertions/s.

  1) Error:
StaticPagesControllerTest#test_should_get_about:
NameError: undefined local variable or method `static_pages_about_url' for #<StaticPagesControllerTest:0x00007f2f77e33db8>
    test/controllers/static_pages_controller_test.rb:15:in `block in <class:StaticPagesControllerTest>'

3 runs, 2 assertions, 0 failures, 1 errors, 0 skips

Failed tests:

Traceback (most recent call last):
        18: from -e:1:in `<main>'
        17: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/2.5.0/rubygems/core_ext/kernel_require.rb:59:in `require'
        16: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/2.5.0/rubygems/core_ext/kernel_require.rb:59:in `require'
        15: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/spring-2.0.2/lib/spring/application/boot.rb:19:in `<top (required)>'
        14: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/spring-2.0.2/lib/spring/application.rb:135:in `run'
        13: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/spring-2.0.2/lib/spring/application.rb:135:in `loop'
        12: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/spring-2.0.2/lib/spring/application.rb:141:in `block in run'
        11: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/spring-2.0.2/lib/spring/application.rb:171:in `serve'
        10: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/spring-2.0.2/lib/spring/application.rb:171:in `fork'
         9: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/minitest-5.11.3/lib/minitest.rb:63:in `block in autorun'
         8: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/minitest-5.11.3/lib/minitest.rb:141:in `run'
         7: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/minitest-5.11.3/lib/minitest.rb:808:in `report'
         6: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/minitest-5.11.3/lib/minitest.rb:808:in `each'
         5: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/railties-5.1.4/lib/rails/test_unit/reporter.rb:37:in `report'
         4: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/railties-5.1.4/lib/rails/test_unit/reporter.rb:41:in `aggregated_results'
         3: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/railties-5.1.4/lib/rails/test_unit/reporter.rb:41:in `map'
         2: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/railties-5.1.4/lib/rails/test_unit/reporter.rb:41:in `block in aggregated_results'
         1: from /home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/railties-5.1.4/lib/rails/test_unit/reporter.rb:70:in `format_rerun_snippet'
/home/vagrant/.anyenv/envs/rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/railties-5.1.4/lib/rails/test_unit/reporter.rb:70:in `method': undefined method `test_should_get_about' for class `Minitest::Result' (NameError)
```
- 次のRED
```
  1) Error:
StaticPagesControllerTest#test_should_get_about:
AbstractController::ActionNotFound: The action 'about' could not be found for StaticPagesController
    test/controllers/static_pages_controller_test.rb:15:in `block in <class:StaticPagesControllerTest>'

3 runs, 2 assertions, 0 failures, 1 errors, 0 skips
```
- 次のRED
- template(ビューのこと)がないよ
```
  1) Error:
StaticPagesControllerTest#test_should_get_about:
ActionController::UnknownFormat: StaticPagesController#about is missing a template for this request format and variant.

request.formats: ["text/html"]
request.variant: []

NOTE! For XHR/Ajax or API requests, this action would normally respond with 204 No Content: an empty white screen. Since you're loading it in a web browser, we assume that you expected to actually render a template, not nothing, so we're showing an error to be extra-clear. If you expect 204 No Content, carry on. That's what you'll get from an XHR or API request. Give it a shot.
    test/controllers/static_pages_controller_test.rb:15:in `block in <class:StaticPagesControllerTest>'

3 runs, 2 assertions, 0 failures, 1 errors, 0 skips
```
- GREEN
```
3 runs, 3 assertions, 0 failures, 0 errors, 0 skips
```
- リファクタリングの習慣は早めにつけておいたほうがよい。
- error(RED): 前の、謎エラーは出るけどともかくテストスイートはREDになった。
```
3 runs, 6 assertions, 3 failures, 0 errors, 0 skips
```
- html.erb変更して`rails test -d`
```
3 runs, 6 assertions, 0 failures, 0 errors, 0 skips
```
- テストの共通化: 各テストが実行される直前で実行されるメソッド、setupを使う
```
def setup
  @hoge="hogehoge"
end
```
- レイアウトの共通化
```
<% provide(:title, "Home) %>
```
- Railsのprovideメソッドを呼び出し。
- <% %>はコード実行、出力なし。
- <%= %>はコード実行、出力がテンプレート(ビュー)に挿入される。
- 実行
```
3 runs, 6 assertions, 0 failures, 0 errors, 0 skips
```
- ERBでも問題なくテストをパス。残りの二つもERBにして、それも問題なくパス。
- ERBに加え、layoutを活用して同じ構造をまとめた。これもパス。
```
3 runs, 6 assertions, 0 failures, 0 errors, 0 skips
```
- テスト用設定
  - minitest reporters
  - 色付きにしてくれる
- Guardによる自動化
  - ファイル変更時に自動的にテストを走らせる。
- initする
```
[vagrant@localhost sample_app]$ bundle exec guard init
05:51:19 - INFO - Writing new Guardfile to /home/vagrant/rails-tutorial/project/sample_app/Guardfile
05:51:20 - INFO - minitest guard added to Guardfile, feel free to edit it
```
- Guardファイルの変更
- コピペした。その中の一文
```
guard :minitest, spring: "bin/rails test", all_on_start: false do
```
- Springサーバ(railsの機能)を使って読み込み時間を短縮する。
- Springは若干不安定なので、テストが遅いなと感じたらSpringをkillする。

- 2つteraterm立ち上げて、片方がGuard用、片方が開発用にする。
```
[vagrant@localhost sample_app]$ bundle exec guard
06:00:57 - INFO - Guard::Minitest 2.4.4 is running, with Minitest::Unit 5.11.3!
06:01:01 - INFO - Guard is now watching at '/home/vagrant/rails-tutorial/project/sample_app'
[1] guard(main)>
```
- Ctrl+Dで終了

## 演習
1.README
- やる

2.Heroku
- とばす

1.Contact
- まずテストの作成
- テスト走らせる
```
4 runs, 6 assertions, 0 failures, 1 errors, 0 skips
```
- routes.rb, contact.html.erbの生成
```
4 runs, 8 assertions, 0 failures, 0 errors, 0 skips
```
- テストをパス。完了。

1.rootルーティングのテスト
- rootのテストを書いて、rootコメントアウトして走らせる
```
5 runs, 8 assertions, 0 failures, 1 errors, 0 skips
```
- OK, error出てる。
- コメントアウトを戻して、テスト
```
5 runs, 9 assertions, 0 failures, 0 errors, 0 skips
```
- パスした。

# 4章
- Rubyについて学ぶ
- stylesheet_link_tagを使って、application.cssをすべてのメディアタイプで使えるようにしている。
```
<%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
```
- ここには、「Railsの組み込み関数」「かっこを使わないメソッド呼び出し」「シンボル」「ハッシュ」が含まれる
- 組み込み関数以外に、新しくメソッドを作ることができる(カスタムヘルパー)
- カスタムヘルパーを作り、テストする
```
5 tests, 9 assertions, 1 failures, 0 errors, 0 skips
```
- homeのprovideを消去
```
5 tests, 9 assertions, 0 failures, 0 errors, 0 skips
```
- 文字列とメソッド
- rails consoleを使う。
- railsコンソールはirb(Interactive RuBy)の拡張。
- `rails console`を使う
```
[vagrant@localhost sample_app]$ rails console
Running via Spring preloader in process 15085
Loading development environment (Rails 5.1.4)
irb(main):001:0>
```
- `"#{name}"`で変数を文字列に埋め込み
- `'#{name}'`では展開できない
- 逆に、\nを表したい！→`'\n'`で表示できる(エスケープされない)
- nil
```
nil.to_s # ""
nil.nil? # true
nil.to_s.nil? #false
!!nil # false
!!false # false
!!0 # true
```
- puts if
```
puts "Yes" if x.empty?
```
- メソッドの定義
- defでできる。デフォルト引数を決められる
```
irb(main):034:0> def string_message(str='')
irb(main):035:1>   if str.empty?
irb(main):036:2>     "empty"
irb(main):037:2>   else
irb(main):038:2>     "nonempty"
irb(main):039:2>   end
irb(main):040:1> end
=> :string_message
irb(main):041:0> puts string_message("of")
nonempty
=> nil
irb(main):042:0> puts string_message
empty
=> nil
```
- full_titleメソッド
```
module ApplicationHelper

  # ページごとの完全なタイトルを返します。                   # コメント行
  def full_title(page_title = '')                     # メソッド定義とオプション引数
    base_title = "Ruby on Rails Tutorial Sample App"  # 変数への代入
    if page_title.empty?                              # 論理値テスト
      base_title                                      # 暗黙の戻り値
    else 
      page_title + " | " + base_title                 # 文字列の結合
    end
  end
end
```
- module includeメソッドを使ってmoduleを読み込むことができる。(mixed in)
- full_titleはrailsの機能により自動的にヘルパーモジュールが読み込まれるため、includeせずにすべてのビューで使用可能になっている。
- データ構造
- 配列: 添え字はマイナスもOK
```
irb(main):001:0> "f a h".split
=> ["f", "a", "h"]
irb(main):002:0> "gxhxjxk".split('x')
=> ["g", "h", "j", "k"]
irb(main):003:0> a = [1,2,3]
=> [1, 2, 3]
irb(main):004:0> a[1]
=> 2
irb(main):005:0> a[-1]
=> 3
irb(main):006:0> a.last==a[-1]
=> true
irb(main):007:0> a
=> [1, 2, 3]
irb(main):008:0> a.empty?
=> false
irb(main):009:0> a.include(2)?
irb(main):010:0*
irb(main):011:0* ^C
irb(main):011:0> a.include?(2)
=> true
irb(main):012:0> a.sort
=> [1, 2, 3]
irb(main):013:0> a.reverse
=> [3, 2, 1]
irb(main):014:0> a.shuffle
=> [2, 3, 1]
irb(main):015:0> a
=> [1, 2, 3]
```
- 破壊的メソッド
```
irb(main):018:0> a.reverse!
=> [3, 2, 1]
irb(main):019:0> a
=> [3, 2, 1]
```
- 追加
```
irb(main):020:0> a.push(2)
=> [3, 2, 1, 2]
irb(main):021:0> a<<"foo"
=> [3, 2, 1, 2, "foo"]
```
- 結合
```
irb(main):022:0> a.join
=> "3212foo"
irb(main):023:0> a
=> [3, 2, 1, 2, "foo"]
irb(main):024:0> a.join('/')
=> "3/2/1/2/foo"
```
- range
```
irb(main):025:0> (0..100).to_a
=> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
irb(main):026:0> b = %w[a b c d]
=> ["a", "b", "c", "d"]
irb(main):028:0> b[0..2]
=> ["a", "b", "c"]
```
- a[0..-1]ですべてを指定できる
- ブロック:eachメソッド(それぞれに対応する処理)mapメソッド(配列を新しく生み出す処理)
```
(1..5).each { |i| puts 2 * i }

(1..5).each do |i|
  puts 3*i
end
```
- ハッシュ: 連想配列`{"a"=>"b", "x"=>"y"}`
- シンボル: `:name`
- ハッシュ`{:a => "b", :x => "y"}`
- 未定義のハッシュ値は`nil`
- `{:a => "b", :x => "y"} == {a:"b", x:"y"} # true`
- JSのJSON的な書き方ができる(キーはシンボルであることに注意)
```
irb(main):001:0> flash = {success: "worked", danger: "failed"}

=> {:success=>"worked", :danger=>"failed"}
irb(main):002:0> flash.each do |key, value|
irb(main):003:1*   puts "key #{key.inspect} has value #{value.inspect}"
irb(main):004:1> end
key :success has value "worked"
key :danger has value "failed"
=> {:success=>"worked", :danger=>"failed"}
```
- Rubyでは、丸かっこはなくてもよい。さらに、メソッド呼び出しの最後の引数のハッシュは波かっこを省略できる
- 次の二つはどちらも合法で、同じ。
```
a1('x1', {y1: 'z1', 'w-r': 'z2'})
a1 'x1', y1: 'z1', 'w-r':'z2'
```
- Rubyは改行と空白を区別していない
- コンストラクタのとこ、すごくjavascriptっぽい
- コンストラクタ: インスタンスを生成したタイミングで実行されるメソッドのこと。メソッド(関数)なのでオブジェクトではない。
- インスタンス: 値。クラスの実体化したもの。これはオブジェクト。
- `""`は文字列(Stringクラス)のインスタンスを作成するコンストラクタ。
- `String.new()` `Array.new()`JSっぽくやれる。
- 注意: ハッシュは少し違う
- `Hash.new`はデフォルト値がnilなので、範囲外キーに対応するのは`nil` `Hash.new(10)`とすると、範囲外キーに対応するのが`10`になる。
- `Class.method`の形で呼び出されるメソッドをクラスメソッドという。`Class.new()`はそのクラスのオブジェクトなので、クラスのインスタンスという。
- それに対し、`hoge.length`のlengthのようにインスタンスに対して呼び出されるメソッドをインスタンスメソッドという。
- クラス継承
- `superclass`メソッドでたどっていける(JSと同じ。nilに行き着くのも同じ。)
- nil->BasicObject->Object->String
- 自作すると、自作クラス < Objectになってる
```
irb(main):032:0> class Wordd
irb(main):033:1>   def p
irb(main):034:2>     puts 1
irb(main):035:2>   end
irb(main):036:1> end
=> :p
irb(main):037:0> w=Wordd.new
=> #<Wordd:0x00007f913de7eac0>
irb(main):038:0> w.p
1
=> nil
irb(main):039:0> w.superclass
Traceback (most recent call last):
        1: from (irb):39
NoMethodError (undefined method `superclass' for #<Wordd:0x00007f913de7eac0>)
irb(main):040:0> w.class
=> Wordd
irb(main):041:0> w.class.superclass
=> Object
```
- Stringを継承
```
irb(main):042:0> class Word < String
irb(main):043:1>   def p?
irb(main):044:2>     self == self.reverse
irb(main):045:2>   end
irb(main):046:1> end
=> :p?
irb(main):047:0> s=Word.new("hogegoh")
=> "hogegoh"
irb(main):048:0> s.p?
=> true
irb(main):049:0> s.length
=> 7
```
- `self==reverse`のように、selfを省略してもよい
- classはCamelCase。_はつかってはいけない
- 組み込みクラスの変更
- Stringに新しくメソッドを追加する
- 普通はダメだけど、railsは組み込みクラスを変更している(もちろん正当な理由があってのこと)
- `blank?`メソッド
- StaticPagesController
```
irb(main):040:0> con=StaticPagesController.new
=> #<StaticPagesController:0x00007fc858d40828 @_action_has_layout=true, @_routes=nil, @_request=nil, @_response=nil>
irb(main):041:0> con.class
=> StaticPagesController
irb(main):042:0> con.class.superclass
=> ApplicationController
irb(main):043:0> con.class.superclass.superclass
=> ActionController::Base
irb(main):044:0> con.class.superclass.superclass.superclass
=> ActionController::Metal
irb(main):045:0> con.class.superclass.superclass.superclass.superclass
=> AbstractController::Base
irb(main):046:0> con.class.superclass.superclass.superclass.superclass.superclass
=> Object
irb(main):047:0> con.class.superclass.superclass.superclass.superclass.superclass.superclass
=> BasicObject
irb(main):048:0> con.class.superclass.superclass.superclass.superclass.superclass.superclass.superclass
=> nil
```
- Railsのアクションには戻り値がない。
- newしなくてもインスタンスが作成されている→Railsはrubyと別物
- `attr_accessor :name, :email`
  - attributeとaccessorの作成。
  - アクセサーを作成すると、getterとsetterが定義される→インスタンス変数@name,@emailにアクセスするためのメソッドが用意される。(要はもろもろの宣言)
- `initialize`
  - User.newを実行すると自動的に呼び出されるメソッド
```
irb(main):001:0> require './example_user'
=> true
irb(main):002:0> e = User.new
=> #<User:0x00007f44e2724e98 @name=nil, @email=nil>
irb(main):003:0> e.name
=> nil
irb(main):004:0> e.name="hiro"
=> "hiro"
irb(main):005:0> e.email="a@b.com"
=> "a@b.com"
irb(main):006:0> e.formatted_email
=> "hiro <a@b.com>"
```


## 演習
1.2.3.4.変数とクォーテーションの違い
```
irb(main):008:0> city = "heroku"
=> "heroku"
irb(main):009:0> prefecture = "barr"
=> "barr"
irb(main):010:0> puts "#{prefecture}県 #{city}町"
barr県 heroku町
=> nil
irb(main):011:0> puts "#{prefecture}県\t#{city}町"
barr県  heroku町
=> nil
irb(main):012:0> puts '#{prefecture}県\t#{city}町'
#{prefecture}県\t#{city}町
=> nil
```
1.2.3.4.回文
```
irb(main):027:0> "racecar".length
=> 7
irb(main):028:0> "racecar".reverse
=> "racecar"
irb(main):029:0> s = "racecar"
=> "racecar"
irb(main):030:0> s == s.reverse
=> true
irb(main):031:0> puts "It's a palindrome!" if s == s.reverse
It's a palindrome!
=> nil
irb(main):032:0> s = "onomatopia"
=> "onomatopia"
irb(main):033:0> puts "It's a palindrome!" if s == s.reverse
=> nil
```
1.2.3.メソッド定義
```
irb(main):043:0> def paindrome_tester(s)
irb(main):044:1>   if s == s.reverse
irb(main):045:2>
Display all 512 possibilities? (y or n)
irb(main):045:2>
irb(main):046:2>     puts "p"
irb(main):047:2>   else
irb(main):048:2>     puts "np"
irb(main):049:2>   end
irb(main):050:1> end
=> :paindrome_tester
irb(main):051:0> paindrome_tester("racecar")
p
=> nil
irb(main):052:0> paindrome_tester("onomatopoeia")
np
=> nil
irb(main):053:0> paindrome_tester("racecar").nil?
p
=> true
```
1.2.3.4.配列
```
irb(main):030:0> "A man,a plan,a canal,Panama".split(',')
=> ["A man", "a plan", "a canal", "Panama"]
irb(main):031:0> a = "A man,a plan,a canal,Panama".split(',')
=> ["A man", "a plan", "a canal", "Panama"]
irb(main):032:0> a
=> ["A man", "a plan", "a canal", "Panama"]
irb(main):033:0> s=a.join
=> "A mana plana canalPanama"
irb(main):034:0> s.split.join
=> "AmanaplanacanalPanama"
irb(main):035:0> def p(s)
irb(main):036:1>   if s==s.reverse
irb(main):037:2>     puts "p"
irb(main):038:2>   else
irb(main):039:2>     puts "nonp"
irb(main):040:2>   end
irb(main):041:1> end
=> :p
irb(main):042:0> s
=> "A mana plana canalPanama"
irb(main):043:0> s.split.join!
Traceback (most recent call last):
        1: from (irb):43
NoMethodError (undefined method `join!' for ["A", "mana", "plana", "canalPanama"]:Array
Did you mean?  join)
irb(main):044:0> s
=> "A mana plana canalPanama"
irb(main):045:0> s.split.join
=> "AmanaplanacanalPanama"
irb(main):046:0> s.split.join.p
Traceback (most recent call last):
        2: from (irb):46
        1: from (irb):35:in `p'
ArgumentError (wrong number of arguments (given 0, expected 1))
irb(main):047:0> s.split.join.downcase.p
Traceback (most recent call last):
        2: from (irb):47
        1: from (irb):35:in `p'
ArgumentError (wrong number of arguments (given 0, expected 1))
irb(main):048:0> s = s.split.join
=> "AmanaplanacanalPanama"
irb(main):049:0> s
=> "AmanaplanacanalPanama"
irb(main):050:0> s.downcase.p
Traceback (most recent call last):
        2: from (irb):50
        1: from (irb):35:in `p'
ArgumentError (wrong number of arguments (given 0, expected 1))
irb(main):051:0> p(s.downcase)
p
=> nil
irb(main):052:0> ("a".."z").to_a[6]
=> "g"
irb(main):053:0> ("a".."z").to_a[-7]
=> "t"
```
1.2.3.4.ブロック
```
irb(main):005:0> (0..16).each do |i|
irb(main):006:1*   puts i**2
irb(main):007:1> end
0
1
4
9
16
25
36
49
64
81
100
121
144
169
196
225
256
=> 0..16
irb(main):008:0> def yeller(s)
irb(main):009:1>   return s.map{|char| char.upcase}.join
irb(main):010:1> end
=> :yeller
irb(main):011:0> yeller(['o', 'l', 'd'])
=> "OLD"
irb(main):012:0> def random_subdomain(s)
irb(main):013:1>   return ('a'..'z').shuffle[0..7].join
irb(main):014:1> end
=> :random_subdomain
irb(main):015:0> random_subdomain
Traceback (most recent call last):
        2: from (irb):15
        1: from (irb):12:in `random_subdomain'
ArgumentError (wrong number of arguments (given 0, expected 1))
irb(main):016:0> random_subdomain()
Traceback (most recent call last):
        2: from (irb):16
        1: from (irb):12:in `random_subdomain'
ArgumentError (wrong number of arguments (given 0, expected 1))
irb(main):017:0> def random_subdomain()
irb(main):018:1> end
=> :random_subdomain
irb(main):019:0> puts random_subdomain

=> nil
irb(main):020:0> def random_subdomain()
irb(main):021:1>   return ('a'..'z').shuffle[0..7].join
irb(main):022:1> end
=> :random_subdomain
irb(main):023:0> puts rand
rand              random_subdomain
irb(main):023:0> puts random_subdomain
Traceback (most recent call last):
        2: from (irb):23
        1: from (irb):21:in `random_subdomain'
NoMethodError (undefined method `shuffle' for "a".."z":Range)
irb(main):024:0> def random_subdomain()
irb(main):025:1>   return ('a'..'z').to_a.shuffle[0..7].join
irb(main):026:1> end
=> :random_subdomain
irb(main):027:0> puts random_subdomain
vbdoipwg
=> nil
irb(main):028:0> def string_shuffle(s)
irb(main):029:1>   s.split('').shuffle.join
irb(main):030:1> end
=> :string_shuffle
irb(main):031:0> string_shuffle("foobar")
=> "orbofa"
```
1.one,two,three
```
irb(main):001:0> hash = { 'one'=>'uno', 'two'=>'dos', 'three'=>'tres'}
=> {"one"=>"uno", "two"=>"dos", "three"=>"tres"}
irb(main):002:0> hash.each{|key, value| puts "#{key.inspect},#{value.inspect}"}
"one","uno"
"two","dos"
"three","tres"
=> {"one"=>"uno", "two"=>"dos", "three"=>"tres"}
```
2.hash-hash
```
irb(main):007:0> person1={:first=>"a1",:last=>"a2"}
=> {:first=>"a1", :last=>"a2"}
irb(main):008:0> person2={:first=>"b1",:last=>"b2"}
=> {:first=>"b1", :last=>"b2"}
irb(main):009:0> person3={:first=>"c1",:last=>"c2"}
=> {:first=>"c1", :last=>"c2"}
irb(main):010:0> params={}
=> {}
irb(main):011:0> params[:father]=person1
=> {:first=>"a1", :last=>"a2"}
irb(main):012:0> params[:mother]=person2
=> {:first=>"b1", :last=>"b2"}
irb(main):013:0> params[:child]=person3
=> {:first=>"c1", :last=>"c2"}
irb(main):014:0> params[:father][:first]
=> "a1"
```
3.user
```
irb(main):016:0> user[:name]="kaito"
=> "kaito"
irb(main):017:0> user[:email]="sample@example.com"
=> "sample@example.com"
irb(main):018:0> user[:password_digest] = "qwertyuiopasdfgh"
=> "qwertyuiopasdfgh"
irb(main):019:0> user
=> {:name=>"kaito", :email=>"sample@example.com", :password_digest=>"qwertyuiopasdfgh"}
```
4.merge
- 予想: `{"a"=>100, "b"=>300}`
```
irb(main):020:0>   { "a" => 100, "b" => 200 }.merge({ "b" => 300 })
=> {"a"=>100, "b"=>300}
```
1.範囲オブジェクトのリテラルコンストラクタ
- .. (1..10のように使う)
2.Rangeとnew
- Range.new(1,10)
3.==で比較
```
irb(main):029:0> s=1..10
=> 1..10
irb(main):030:0> a=Range.new(1,10)
=> 1..10
irb(main):031:0> s==a
=> true
```
1.Range, Hash, Symbol
- Range < Object < BasicObject < nil
- Hash < Object < BasicObject < nil
- Symbol < Object < BasicObject < nil
2.省略記法
- 確認するだけ
1.回文
```
irb(main):003:0> class String
irb(main):004:1>   def p
irb(main):005:2>     self==reverse
irb(main):006:2>   end
irb(main):007:1> end
=> :p
irb(main):008:0> "deified".p
=> true
irb(main):009:0> "racecar".p
=> true
irb(main):010:0> "onomatopoeia".p
=> false
irb(main):011:0> "Malayalam".downcase.p
=> true
```
2.shuffle
```
irb(main):027:0> class String
irb(main):028:1>   def shuffle3
irb(main):029:2>     self.split('').shuffle.join
irb(main):030:2>   end
irb(main):031:1> end
=> :shuffle3
irb(main):032:0> "asdfg".shuffle3
=> "afsdg"
irb(main):033:0> "asdfg".shuffle3
=> "fsgda"
```
3.self削除
```
irb(main):034:0> class String
irb(main):035:1>   def shuffle4
irb(main):036:2>     split('').shuffle.join
irb(main):037:2>   end
irb(main):038:1> end
=> :shuffle4
irb(main):039:0> "foobar".shuffle4
=> "raoobf"
```
1.2.User(toy_app)
```
irb(main):002:0> User.new
=> #<User id: nil, name: nil, email: nil, created_at: nil, updated_at: nil>
irb(main):003:0> a=User.new
=> #<User id: nil, name: nil, email: nil, created_at: nil, updated_at: nil>
irb(main):004:0> a.class
=> User(id: integer, name: string, email: string, created_at: datetime, updated_at: datetime)
irb(main):005:0> a.class.superclasss
Traceback (most recent call last):
        1: from (irb):5
NoMethodError (undefined method `superclasss' for #<Class:0x00007f0808066438>
Did you mean?  superclass)
irb(main):006:0> a.class.superclass
=> ApplicationRecord(abstract)
irb(main):007:0> a.class.superclass.superclass
=> ActiveRecord::Base
irb(main):008:0> a.class.superclass.superclass.superclass
=> Object
```
1.2.3.User
```
irb(main):001:0> require './example_user'
=> true
irb(main):002:0> u=User.new
=> #<User:0x00007f44e2918a38 @first_name=nil, @last_name=nil, @email=nil>
irb(main):003:0> u.first_name="john"
=> "john"
irb(main):004:0> u.last_name="kelly"
=> "kelly"
irb(main):005:0> u.email="p@p.com"
=> "p@p.com"
irb(main):006:0> u.full_name.split==u.alphabetical_name.split(',').reverse ?
irb(main):007:0* ?
irb(main):008:0*
(irb):7: warning: invalid character syntax; use ?\n
Traceback (most recent call last):
SyntaxError ((irb):7: syntax error, unexpected '?')
irb(main):009:0> u.full_name.split==u.alphabetical_name.split(',').reverse
=> false
irb(main):010:0> u.full_name.split
=> ["john", "kelly"]
irb(main):011:0> u.alphabetical_name.split(',').reverse
=> [" john", "kelly"]
irb(main):012:0> u.alphabetical_name.split(', ').reverse
=> ["john", "kelly"]
```

# 5章
- パーシャル、Railsのルーティング、Asset Pipeline, Sassについて学ぶ。
- レイアウトファイル(application.html.erb)
- IE9より小さいものに対応(条件付きコメント、Railsではなく、IEの機能)
```
<!--[if lt IE 9]>
  <script src="//cdnjs.cloudflare.com/ajax/libs/html5shiv/r29/html5.min.js">
  </script>
<![endif]-->
```
- `link_to [リンクテキスト] [URL]` Railsヘルパー(アンカータグaが最終的に生成される)
  - この段階では#にしておく(後で置き換える、とりあえずの意味。)
- `image_tag`ヘルパー: アセットパイプラインを通してapp/assets/imagesディレクトリの中から探してくれる
- HTMLで見るとこんな感じ
- 文字列が追加されているのは、rails.pngを変更したとき、ブラウザのキャッシュにヒットさせないようにするため。
- `<img all="Rails logo" src="/assets/rails-c094bc3a4bf50e5bb477109e5cb0d213af27ad75b481c4df249f50974dbeefe6.png" alt="Rails">`
- さらに、assets/にあるように見せている→ファイルを高速にブラウザに渡すため
- Bootstrapはレスポンシブ
- BootstrapはLESSCSS言語、でもrailsではSass→LESSをSassに変換するgemを導入
- partialはレイアウトをまとめる機能(HTML importっぽい感じ)
- `render`rails helperを用いて、レイアウトを別のとこからもってくることができる。
- `render 'layouts/hoge'`に対応するのは`app/views/layouts/_hoge.html.erb`になる(アンダースコアに注意)
- Sass AssetPipeline
- アセットディレクトリ(置き場)、マニフェストファイル(置き場からどのコードを使うか)、プリプロセッサエンジン(コードをプリプロセッサエンジンを用いて実行、ブラウザに配信できるように結合)の三つが理解の対象。
- app/assets, lib/assets, vendor/assetsの3つのディレクトリがある。
- app/assets/stylesheets/application.cssの中身
```
*= require_tree .
*= require_self
```
- これが大事。sprocketsがファイルを読み込むときに使う。→ http://railsguides.jp/asset_pipeline.html も参照。
- プリプロエンジンは、js.erb.coffeeみたいなものも処理できる。
- AssetPipelineによってcssはapplication.css, JSはjavascripts.jsにまとめられ、高速化が図れる(本番環境用に、ファイルサイズを最小化する)
- Sass: nest, 変数→可読性高い(ネストは可読性低いのでは)
- #で代用していたリンクの置き換え
- `/hoge`と`hoge_path`が対応する
- RailsのルートURL
- pathとurlの違い→pathは相対、urlは絶対
- 基本pathを使う、リダイレクトのみurlをつかう。
- error: contact page
```
5 tests, 0 assertions, 0 failures, 5 errors, 0 skips
 1) Error:
StaticPagesControllerTest#test_should_get_about:
ActionView::Template::Error: undefined local variable or method `about_path' for #<#<Class:0x00007f0436ec2188>:0x00007f041800f4b0>
    app/views/layouts/_footer.html.erb:8:in `_app_views_layouts__footer_html_erb__2683407668703088844_69828063957440'
    app/views/layouts/application.html.erb:12:in `_app_views_layouts_application_html_erb__2030040032658899824_69828038746000'
    test/controllers/static_pages_controller_test.rb:27:in `block in <class:StaticPagesControllerTest>'

  2) Error:
StaticPagesControllerTest#test_should_get_help:
ActionView::Template::Error: undefined local variable or method `about_path' for #<#<Class:0x00007f0436ec2188>:0x00007f0439da38a8>
    app/views/layouts/_footer.html.erb:8:in `_app_views_layouts__footer_html_erb__2683407668703088844_69828063957440'
    app/views/layouts/application.html.erb:12:in `_app_views_layouts_application_html_erb__2030040032658899824_69828038746000'
    test/controllers/static_pages_controller_test.rb:21:in `block in <class:StaticPagesControllerTest>'

  3) Error:
StaticPagesControllerTest#test_should_get_root:
ActionView::Template::Error: undefined local variable or method `about_path' for #<#<Class:0x00007f0436ec2188>:0x00007f0439ccfe18>
    app/views/layouts/_footer.html.erb:8:in `_app_views_layouts__footer_html_erb__2683407668703088844_69828063957440'
    app/views/layouts/application.html.erb:12:in `_app_views_layouts_application_html_erb__2030040032658899824_69828038746000'
    test/controllers/static_pages_controller_test.rb:10:in `block in <class:StaticPagesControllerTest>'

  4) Error:
StaticPagesControllerTest#test_should_get_contact:
ActionView::Template::Error: undefined local variable or method `about_path' for #<#<Class:0x00007f0436ec2188>:0x00007f0439bb7198>
    app/views/layouts/_footer.html.erb:8:in `_app_views_layouts__footer_html_erb__2683407668703088844_69828063957440'
    app/views/layouts/application.html.erb:12:in `_app_views_layouts_application_html_erb__2030040032658899824_69828038746000'
    test/controllers/static_pages_controller_test.rb:33:in `block in <class:StaticPagesControllerTest>'

  5) Error:
StaticPagesControllerTest#test_should_get_home:
ActionView::Template::Error: undefined local variable or method `about_path' for #<#<Class:0x00007f0436ec2188>:0x00007f0439b1a168>
    app/views/layouts/_footer.html.erb:8:in `_app_views_layouts__footer_html_erb__2683407668703088844_69828063957440'
    app/views/layouts/application.html.erb:12:in `_app_views_layouts_application_html_erb__2030040032658899824_69828038746000'
    test/controllers/static_pages_controller_test.rb:15:in `block in <class:StaticPagesControllerTest>'
```
- 1.2.3.4.5.`about_path`がやばい
- 削除してみる
- about_pathは後で定義する？定義しないまま使うとエラー(それはそうだけど、組み込み化と思ってしまった)
- about_path, contact_pathを除くと`5 tests, 9 assertions, 0 failures, 0 errors, 0 skips`GREEN
- `root 'static_pages#home'`これは、rootURL"/"をコントローラのアクションに紐づけている。
- getルールを使ってルーティングを決める。testもルーティングの書き方を新しくする。
- `4 tests, 8 assertions, 0 failures, 0 errors, 0 skips`
- うまくいった…hoge_pathもhoge_urlと同じく組み込みっぽいな？
- routes.rbでhoge_pathが使えるようになった。→layoutのlink_toでhoge_pathが使えるようになった。
- リンクがちゃんと機能しているか調べる。
- すべてのリンクをポチポチ調べるのではなく統合テストを使って自動化する。
- 目的
  - HTML構造を調べて、レイアウトの各リンクが正しく動くか確認すること。
  - URLにGETリクエスト
  - 正しいページテンプレートが描画されてるか
  - その他のページも同様に調べる
- `assert_select`は強い。けど、複雑なことはしないほうがよい。
- `assert_select "a[href=?]", '/hoge'`は、`<a href="/hoge"></a>`を指す。
- `rails test:integration`が統合テスト。
- `1 tests, 5 assertions, 0 failures, 0 errors, 0 skips`
- 統合テスト通った。
- 全てのテストを流す。
- `5 tests, 13 assertions, 0 failures, 0 errors, 0 skips`GREEN
- User Sign up pageを作る
- ルーティングをやってきたけど、これからはアプリケーションの肉付け(認証など)をやっていくよ。 

## 演習
1.2.3.猫
```
[vagrant@localhost sample_app]$ curl -OL cdn.learnenough.com/kitten.jpg
[vagrant@localhost sample_app]$ mv kitten.jpg app/assets/images/kitten.jpg
```
```
<%= link_to image_tag("kitten.jpg", all: "kitten logo") %>
```
1.2.3.パーシャルの追加
- render→test red→partial→test green
- `rails test -d`
- `5 tests, 0 assertions, 0 failures, 5 errors, 0 skips`
- `5 tests, 9 assertions, 0 failures, 0 errors, 0 skips`OK
1.custom.scssをcss化
```
@import "bootstrap-sprockets";
@import "bootstrap";

/* mixins, variables, etc. */ 
$gray-medium-light: #eaeaea;
/* universal */
body {
    padding-top: 60px;
}

section {
    overflow: auto;
}

textarea {
    resize: vertical;
}

.center {
    text-align: center;
    h1 {
        margin-bottom: 10px;
    }
}

/* typography */

h1,h2,h3,h4,h5,h6 {
    line-height: 1;
}

h1 {
    font-size: 3em;
    letter-spacing: -2px;
    margin-bottom: 30px;
    text-align: center;
}

h2 {
    font-size: 1.2em;
    letter-spacing: -1px;
    margin-bottom: 30px;
    text-align: center;
    font-weight: normal;
    color: $gray-light;
}

p {
    font-size: 1.1em;
    line-height: 1.7em;
}

/* header */

#logo {
    float:left;
    margin-right: 10px;
    font-size: 1.7em;
    color: white;
    text-transform: uppercase;
    letter-spacing: -1px;
    padding-top: 9px;
    font-weight: bold;
    &:hover {
        color: white;
        text-decoration: none;
    }
}

img {
    display: none;
}

/* footer */
footer {
    margin-top: 45px;
    padding-top: 5px;
    border-top: 1px solid $gray-medium-light;
    color: $gray-light;

    a {
        color: $gray;
        &:hover {
            color: $gray-darker;
        }
    }

    small {
        float: left;
    }

    ul {
        float:right;
        list-style: none;
        
        li {
            float: left;
            margin-left: 15px;
        }
    }
}

```
1.2.3.helf
```
get '/help', to: 'static_pages#help', as: 'helf'
```
```
4 tests, 6 assertions, 0 failures, 1 errors, 0 skips
```
直す
test/controller/..
```
get helf_path
```
```
4 tests, 8 assertions, 0 failures, 0 errors, 0 skips
```
- GREEN
1.2.helf
- 確かめるだけ。特になし。
1.2.変更、full_title
- Errorはいた
```
Failure:
SiteLayoutTest#test_layout_links [/home/vagrant/rails-tutorial/project/sample_app/test/integration/site_layout_test.rb:10]:
Expected at least 1 element matching "a[href="/about"]", found 0..
Expected 0 to be >= 1.
```
- full_title helperのテスト
- FILL_INわからない
```
require 'test_helper'

class ApplicationHelperTest < ActionView::TestCase
    test "full title helper" do
        assert_equal full_title, "Ruby on Rails Tutorial Sample App"
        assert_equal full_title("Help"), "Help | Ruby on Rails Tutorial Sample App"
    end
end
```
1.2.signup RED
```
7 tests, 17 assertions, 0 failures, 0 errors, 0 skips
```
次の章の内容を先取りしていたのでGREENになった
1.2.3.テスト
```
7 tests, 17 assertions, 0 failures, 0 errors, 0 skips
```
- コメントアウト
```
7 tests, 8 assertions, 0 failures, 3 errors, 0 skips
```
- RED
```
require 'test_helper'

class SiteLayoutTest < ActionDispatch::IntegrationTest
  
  test "layout links" do
    get root_path
    assert_template 'static_pages/home'
    assert_select "a[href=?]", root_path, count: 2
    assert_select "a[href=?]", help_path
    assert_select "a[href=?]", about_path
    assert_select "a[href=?]", contact_path
    assert_select "a[href=?]", signup_path
    get contact_path
    assert_select "title", full_title("Contact")
    get signup_path
    assert_select "title", full_title("Sign up")
  end
end
```
- これでRED
```
7 tests, 8 assertions, 0 failures, 3 errors, 0 skips
```
- homepageのリンクのテストと、内容のテストを行った。
```
Error:
SiteLayoutTest#test_layout_links:
ActionView::Template::Error: undefined local variable or method `signup_path' for #<#<Class:0x00007f2a36231650>:0x00007f2a36220670>
    app/views/static_pages/home.html.erb:9:in `_app_views_static_pages_home_html_erb__3082552532222737662_69909636814120'
    test/integration/site_layout_test.rb:6:in `block in <class:SiteLayoutTest>
```
- はいーtypoー。sig nupてしてた。signup_pathを定めてるroutes.rbがおかしいと思って探せたのはよかった。
```
1 tests, 8 assertions, 0 failures, 0 errors, 0 skips
```
- GREEN