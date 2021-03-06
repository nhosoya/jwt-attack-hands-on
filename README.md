## ハンズオンの環境構築
```zsh
cd none-attack // またはweak-secret
go run main.go
```

John the Ripperの環境構築
```
git clone https://github.com/magnumripper/JohnTheRipper // John the Ripperの公式リポジトリからclone
cd JohnTheRipper/src
./configure
make -s clean && make -sj4 // ビルド

// JWTのsecretをブルートフォースしたい場合
cd JohnTheRipper/run
vim jwt.txt // JWTをテキストファイルに書く
./john jwt.txt // jwt.txtの中身はさっきのJWT
```

## ハンズオンのゴール
- none-attack、weak-secret共に`user:admin`として`/admin`にアクセスすることがゴールとなります

## エンドポイントへのアクセス方法
- `curl http://localhost:5555/token`
- なお、どのハンズオンも`/`,`/token`, `/admin`の3つのエンドポイントしかありません


## JWTをAuthorizationヘッダに入れてHTTPリクエストを送信する
`curl http://localhost:5555/admin -H "Authorization: Bearer <JWT>"`

## その他
- none-attack内のjwt-goはこのハンズオンのために一部ライブラリ内のコードを変更しています
- .envファイルにはJWTの署名に用いる鍵を設定しています。weak-secretの.envを先に見てしまうとネタバレになってしまうので、ハンズオンが終わった後に開くことをお勧めします