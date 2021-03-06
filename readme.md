**html5_package with grunt.js**  
====================================================================
**Windows環境用batファイル/Mac環境用commandファイル付**  

update 2013.10.22  
**tsukasa-web**  
https://github.com/tsukasa-web  

***
  
###**概要**

簡単にgrunt.jsの設定・起動ができるファイル一式です。
また、html5の雛形となるhtmlとnormalize.css、modernizr.jsも同梱しています。
Gruntfile.jsを変更することで設定の変更やディレクトリの変更が可能です。

**※2013.10.22以降の更新は[generator-giraffe](https://github.com/tsukasa-web/generator-giraffe)で行われています。**

***

###**機能**  

* ディレクトリの初期構築・初期構築後の不要ファイル削除
* CoffeeScriptのコンパイル
* TypeScriptのコンパイル
* Sassのコンパイル
* css/jsファイルの結合＆圧縮
* jsHintによるデバッグ
* watchによるファイル更新の監視→コンパイル・結合・圧縮・デバッグの自動化
* 自動ブラウザリロード
* 画像圧縮
* config.rb連動によるスプライト画像のランダム文字列消去
* Macパッケージのみcssプロパティの並び替え追加
* Macパッケージのみwebfont作成機能の追加

###**次期追加予定機能**  
* yeoman,bowerとの連携

###**更新**  
* 2013.10.17 grunt-contrib-watchのメモリ消費が激しいため、grunt-este-watchとlivereloadxに変更 
* 2013.10.22 変更ファイルのみをコンパイルするように変更

***

###**諸注意**  

Gruntfileを設定せずにディレクトリをいじると基本的に動きません。  
  
※プラグイン等の著作権記述が必要なjsファイルはコメントのライセンス表記の前に必ず@licenseを記述してください。
これを記述することで圧縮時にライセンス記述コメントのみ残るようになります。

（例：  
    /* @license  
    * Bootstrap.js by @fat & @mdo  
    *  
    * plugins: bootstrap-transition.js, bootstrap-dropdown.js, bootstrap-carousel.js  
    * Copyright 2012 Twitter, Inc.  
    * http://www.apache.org/licenses/LICENSE-2.0.txt  
    */  

***

###**設定手順**  

※順番を必ず守りましょう。  

###**①Node.jsをインストール**  
http://nodejs.org/  

###**②gruntをインストール**  
Windowsは、キーボードで [win]+[r]を押して、「ファイル名を指定して実行」で cmd を入力。コマンドプロンプトが起動するはずです。  
Macは、ターミナルを開いてください。Macintosh HD>アプリケーション>ターミナルで開きます。
起動したらすかさず  
`npm install -g grunt-cli`  
と入力してgruntをインストールしてください。  
Win環境の人で管理権限等でエラーが出た人は管理者権限でcmdを起動してください。  
gruntのインストールを確認後、  
`npm install -g livereloadx`  
と入力してlivereloadxをインストールしてください。 

###**③ディレクトリ作成**  
パッケージ内に入っているgrunt_filesをルートディレクトリとなる階層に配置します。

###**※Compassについて（Sassを使わない人は読み飛ばしていただいて大丈夫です）**  
Compass自体は通常通り@import "compass";で使えます。  
Compassのイメージディレクトリが/common/images/に設定されています。  
そのため、スプライトシートのインポートはディレクトリ通りにすると  
@import "sprite/*.png";になります。  

###**④プラグインのインストール+ベースとなるディレクトリの生成**  
grunt_files/cmd_bat内のgrunt_install.batまたはgrunt_install.commandを叩いてください。  
プラグイン等のインストールが始まります。node_modulesがgrunt_files内に生成されるはずです。  
その後、しばらくするとベースとなるディレクトリがgrunt_filesと同階層に生成されます。  
この時にlibフォルダに入っている雛形のhtmlファイルとnormalize.cssとmodernizr.custom.jsが配置されます。

###**⑤Gruntfileの調整**

Gruntfile.jsの調整を行います。

* バーチャルホスト名（xamppのVH名です）  
* docs  
* 共通リソースの配置先
* コンパイル言語ファイルの格納先 

を設定してください。  
ここで決めた名称がそのままディレクトリのフォルダ名として後々生成されます。

	// パスの設定
	var pathConfig = {
		vh: 'Please input VH',		// バーチャルホストのサーバー名
		root: '../docs',				// project root
		src: 'common',				// 共通リソースの配置先
		compile: 'common/compile'	// コンパイル言語ソース類の配置先
	};

###**CoffeeScriptのコンパイル**  

CoffeeScript/TypeScriptファイルは⑤で設定したコンパイル言語ファイルの格納先に入れることになります。CoffeeScriptを使う人でtop-levelのfunctionで包括したい方はoptionの部分を消してください。

###**js,cssファイルの結合** 

Gruntfile.jsを開き、結合したいcss,jsのパスを通します。  
上から順に結合されていくので、順番を間違えないようにしてください。  
ちなみにGrunt.jsにおいてルート相対・絶対パスは認識されません。   

    concat: {
    	style: {
    		src: [
    			'<%= path.root %>/<%= path.src %>/css/hogehoge.css',
    			'<%= path.root %>/<%= path.src %>/css/hogehoge2.css',
    			'<%= path.root %>/<%= path.src %>/css/hogehoge3.css'
    		],
    		dest: '<%= path.root %>/<%= path.src %>/all/style-all.css'
    	},
    	run: {
    		src: [
    			'<%= path.root %>/<%= path.src %>/js/hogehoge.js',
    			'<%= path.root %>/<%= path.src %>/js/hogehoge2.js',
    			'<%= path.root %>/<%= path.src %>/js/hogehoge3.js',
    			'<%= path.root %>/<%= path.src %>/js/hogehoge4.js'
    		],
    		dest: '<%= path.root %>/<%= path.src %>/all/run-all.js
    	}
    },

###**⑥タスクを走らせる**  

もしすでに制作が進んでいる状態でscss/css/coffee/jsが作成されている場合は、  
ファイルがディレクトリ通りに配置されているかを確認したうえでgrunt_command.batまたはgrunt_command.comandを叩いてください。  
一度コンパイル・結合・圧縮・デバッグが行われます。  
src:で設定したパスフォルダ/all/配下に結合されたcss/jsファイルが入っていれば成功です。  

###**⑦ファイル監視を起動**

①～⑥が終わったら準備完了です。grunt_watch.batまたはgrunt_watch.commandを叩いてください。  
Grunt.jsで設定したVH名でページが開き、ファイルの監視が始まります。
Sublime Text2でlivereloadのプラグインを入れてる人は、バッティングするのでプラグインをremoveしてから使ってください。  
この後、コンソールは出したままにしておいてください。最小化しても大丈夫です。  
以降はscss/coffee/js(Sassのみの時)が更新される度に自動的にコンパイル・結合・圧縮・デバッグが行われます。  
さらに、htmlとcss(sassを使っている人はscss更新時)の更新時に自動でブラウザがリロードされます。  
コンソールは消さずに出したままにしておいてください。監視をやめたい場合はコンソール上でCtrl+Cを押してください。　　
任意のタイミングでコンパイル・結合・圧縮・デバッグを行いたい場合はgrunt_command.batまたはgrunt_command.commandを叩くか、コンソール上で「grunt」と打ち込んでください。  　　

###**⑧SVN等のバージョン管理ソフトから設定ファイルを除外する**

レポジトリから各種設定ファイルを除外します。  
**※SVNの場合**  
「grunt_filesフォルダを右クリック→TortoiseSVN→バージョン管理から除外し、無視リストに追加」  
  

###**⑨firefoxまたはchromeに自動リロード用のアドオンorエクステンションを入れる**

**Firefox**  
http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions-  
「Firefox extension」というやつです。  

**Chrome**  
https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei  


あとは追加されたアドオンのマークを押して、丸の中が赤くなれば成功です。  
⑦のファイル監視を行っている最中に行ってください。  
後はhtmlまたはcss(sassの人はscss)を編集して保存した際にブラウザがリロードされればok。

###**⑩仕上げの時に画像圧縮を行う**

batフォルダの中にあるgrunt_imagemin.batまたはgrunt_imagemin.commandを叩くと画像圧縮が始まります。  
現状第3階層までのフォルダの中の画像を圧縮しますが、さらに階層を掘り下げたい時は

    imagemin: {
        dist: {
            options: {
                    optimizationLevel: 3
                },
            files: [{
                expand: true,
                src: [
                    '<%= path.root %>/**/*.{png, jpg, jpeg}','<%= path.root %>/**/**/*.{png, jpg, jpeg}','<%= path.root %>/**/**/**/*.{png, jpg, jpeg}'
                ]
            }]
        }
    },

上記の記述のsrcの中を追記していただけると追加することができます。  
optimizationLevelを変更することで圧縮レベルを変更できます。（0～7）

###**⑪webfontの作成（Macのみ）**

batフォルダの中にあるgrunt_webfontを叩くとwebfontの作成が始まります。初期設定では/common/fonts/iconsフォルダにaiファイルを格納してください。

    webfont: {
    			icons: {
    				src: '<%= path.root %>/<%= path.src %>/fonts/icons/*.svg',
    				dest: '<%= path.root %>/<%= path.src %>/fonts',
    				destCss: '<%= path.root %>/<%= path.compile %>',
    				options: {
    					font: 'custom-fonts',
    					stylesheet:'scss',
    					htmlDemo: false,
    					relativeFontPath: '/<%= path.src %>/fonts'
    				}
    			}
    		},


***

**html5_packageについて**
====================================================================  
2013.09.30 tsukasa-oneslocus  
https://github.com/tsukasa-oneslocus  

***

backbone.jsを使うために作成した基本パッケージにhtml5のひな形とよく使われる基本ライブラリを格納したパッケージです。  
modenizrはカスタムで全ての機能を包括しているので、最終的に洗い出した機能を元にカスタムビルドし直してください。  
カスタムは http://modernizr.com からグレーのボタン「DEVELOPMENT」を押して、スクリプト作成ページに移動します。  

***

**Modernizrについて**
----------------------------------------
jsライブラリ。フィーチャーディテクションができます！！  
http://modernizr.com/  

ブラウザによってサポートされている機能は毎回調べないと分かりません。  
しかし、このライブラリを使うことでブラウザで何が使えて、何が使えないかが分かります。  
html要素などでクラス"no-js"を使えば、今見ているブラウザでどれが使えてどれが使えないのかがhtml上に吐き出してくれます！  
css属性に目印をつけてくれるので、  

    .sample{
         box-shadow...
    }

    html .no-boxshadow .sample{
         ….
    }


と記述することで、属性非対応のものに対応することができます。  
しかも対応させる属性をカスタマイズしてビルドすることができるのです。  
使う属性だけチェックを入れれば大丈夫です。  

※IE8以下にもhtml5の要素を表示させることができるようになるライブラリ、「htmlshiv」も入っています。  

***

**Normalize.cssについて**
----------------------------------------

デフォルトCSSの不揃いを慣らしてくれるcssです。  
http://necolas.github.io/normalize.css/  

さらにデフォルトの矛盾を解消し、IE9において発生するSVGバグ等を解決してくれます。  
また、新要素にCSSのデフォルト値を設定してくれます。  
つまり、リセットの前段階の濾過掃除をしてくれるのです。  

あとは必要に応じてリセットしていけば効率的です。  