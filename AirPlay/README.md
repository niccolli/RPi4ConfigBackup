# AirPlayサーバーの設定

iPhone・Macから音声データを受信して、Raspberry Piのイヤホン端子から出力させる。I2SやUSBオーディオI/Fは一旦考慮しない。

## 設定

### shairport-sync

- https://qiita.com/peishnm2/items/280216428a654670ba85

上記投稿ではshairport-syncを自前でビルドしているが、aptでインストールできる(OSのリポジトリにある)もので問題ない。

[shairport-sync.conf](./shairport-sync.conf)を/etc/shairport-sync.confにコピーする。イヤホン端子から出すならば general / name の箇所(iPhone等で表示される名前)のみ適宜変更すればよい。

## 手順

```
$ sudo apt-get install shairport-sync
$ sudo mv shairport-sync.conf /etc/shairport-sync.conf
$ sudo systemctl enable shairport-sync
$ sudo systemctl start shairport-sync
```

Macで表示名が反映されていない場合は、Raspberry Piを再起動する。サービス再起動でもよいかもしれない(未確認)。
