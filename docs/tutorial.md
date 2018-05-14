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