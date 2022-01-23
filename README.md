# 手順書

以下のソフトウェア上で開発、動作確認済みです。

・Docker バージョン20.10.7

・Docker-compose バージョン1.29.2

・git バージョン2.25.1

上記docker及びdocker-compose、gitの導入手順は以下の通りです。(amazon linux2の場合)

1.dockerを使えるようにする

`sudo yum install -y docker`

`sudo systemctl start docker`

`sudo systemctl enable docker`

`sudo usermod -a -G docker ec2-user`

2.docker-composeを使えるようにする

`sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`

`sudo chmod +x /usr/local/bin/docker-compose`

3.gitを入れる

`sudo yum update`

`sudo yum install git`

4.入ったか確認

`docker -v`

`docker-compose -v`

`git --version`

構築手順

1.ソースコードの設置

githubより任意のディレクトリにcloneしてください

`git clone git@github.com:ku6non/sat1_2.git`


2.dbの構築

・まず一度docker-composeをbuildし、起動する必要があるので

以下のコマンドでbuild及びupしてください。

`docker-compose build`

`docker-compose up`

・次に以下のコマンドを実行してmysqlを起動し、
4つのテーブルを作成してください。

`docker exec -it mysql mysql techc`


`CREATE TABLE 'koki02_users' (
                'id' INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
		'name' TEXT NOT NULL,
		'email' TEXT NOT NULL,
    	 	'password' TEXT NOT NULL,
    		'created_at' DATETIME DEFAULT CURRENT_TIMESTAMP
		);`
		
		
`CREATE TABLE 'users' (
    		'id' INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
   		'name' TEXT NOT NULL,
    		'email' TEXT NOT NULL,
    		'password' TEXT NOT NULL,
    		'created_at' DATETIME DEFAULT CURRENT_TIMESTAMP,
    		'icon_filename' TEXT DEFAULT NULL,
    		'cover_filename' TEXT DEFAULT NULL,
    		'birthday' DATE DEFAULT NULL,
    		'introduction' TEXT DEFAULT NULL
		);`
		
		
`CREATE TABLE 'bbs_entries' (
    		'id' INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    		'user_id' INT UNSIGNED NOT NULL,
    		'body' TEXT NOT NULL,
    		'image_filename' TEXT DEFAULT NULL,
    		'created_at' DATETIME DEFAULT CURRENT_TIMESTAMP
		);`
		
		
`CREATE TABLE 'user_relationships' (
    		'id' INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    		'followee_user_id' INT UNSIGNED NOT NULL,
    		'follower_user_id' INT UNSIGNED NOT NULL,
    		'created_at' DATETIME DEFAULT CURRENT_TIMESTAMP
		);`
		

3.docker再構築

・mysqlの変更を反映させるために一度ctrl+c(もしくはコマンド`docker-compose down`)で

docker-composeを落として以下のコマンドで再構築してください。

`docker-compose build`

`docker-compose up`



4.確認

掲示板のページは http://34.198.92.38/login.php です。

webページにて動作確認をお願いします。

