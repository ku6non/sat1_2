# 手順書
必要なソフトウェア
以下のソフトウェア上で開発、動作確認済みです。
あらかじめ導入しておいてください。
・Docker バージョン20.10.7
・Docker-compose バージョン1.29.2

構築手順
1.ソースコードの設置
githubより任意のファイル内にcloneしてください
urlは[link](git@github.com:ku6non/sat1_2.git)です。

2.dbの構築
・まず一度docker-composeをbuildし、起動する必要があるので
以下のコマンドでbuild及びupしてください。

`docker-compose build`
`docker-compose up`

・次に以下のコマンドを実行してmysqlを起動し、
4つのテーブルを作成してください。
`docker exec -it mysql mysql techc`
`MariaDB[techc]>>CREATE TABLE 'koki02_users' (`
                `'id' INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,`
		`'name' TEXT NOT NULL,`
		`'email' TEXT NOT NULL,`
    	 	`'password' TEXT NOT NULL,`
    		`'created_at' DATETIME DEFAULT CURRENT_TIMESTAMP`
		`);`
		
`MariaDB[techc]>>CREATE TABLE 'users' (`
    		`'id' INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,`
   		`'name' TEXT NOT NULL,`
    		`'email' TEXT NOT NULL,`
    		`'password' TEXT NOT NULL,`
    		`'created_at' DATETIME DEFAULT CURRENT_TIMESTAMP,`
    		`'icon_filename' TEXT DEFAULT NULL,`
    		`'cover_filename' TEXT DEFAULT NULL,`
    		`'birthday' DATE DEFAULT NULL,`
    		`'introduction' TEXT DEFAULT NULL`
		`);`
		
`MariaDB[techc]>>CREATE TABLE 'bbs_entries' (`
    		`'id' INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,`
    		`'user_id' INT UNSIGNED NOT NULL,`
    		`'body' TEXT NOT NULL,`
    		`'image_filename' TEXT DEFAULT NULL,`
    		`'created_at' DATETIME DEFAULT CURRENT_TIMESTAMP`
		`);
		
`MariaDB[techc]>>CREATE TABLE 'user_relationships' (`
    		`'id' INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,`
    		`'followee_user_id' INT UNSIGNED NOT NULL,`
    		`'follower_user_id' INT UNSIGNED NOT NULL,`
    		`'created_at' DATETIME DEFAULT CURRENT_TIMESTAMP`		
		`);`\
3.docker再構築
・mysqlの変更を反映させるために一度ctrl+cでdocker-composeをstopさせて
以下のコマンドで再構築してください。
`docker-compose build`
`docker-compose up`


4.確認
掲示板のページは/login.phpです。
動作確認をお願いします。
