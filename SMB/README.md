# SMBの設定

smbでTime Capsuleを実装するための設定。

## 設定

### SMB

- https://saschaeggi.medium.com/use-a-raspberry-pi-4-for-time-machine-works-with-big-sur-1e66a9650789
- https://www.reddit.com/r/linuxquestions/comments/juyue6/samba_share_as_time_machine_backup_getting/

Mediumの投稿でSMBの動作までは動いたが、Time Machineだけが動かない。SMBがGuestでも書き込めるようchmod 777も実行し、その後Redditの設定も追加したら動いた。Redditの内容も反映済みのファイルが[smb.conf](./smb.conf)なので、SMBが動いていれば/etc/samba/smb.confと置き換えればよい。

### Avahi

MacがTime Capsuleだと理解できるよう、Avahiに設定を追加する。[samba.service](./samba.service)を /etc/avahi/services/samba.service として保存する。

### HDD

- ext4 (HFS+でなくても動いた)

## 手順

```
$ sudo apt-get install samba avahi-daemon
$ ls -lha /dev/disk/by-uuid                # Time Capsule用HDDのUUIDを確認
$ sudo vi /etc/fstab                       # fstabにUUIDを記載。オプションはリポジトリ内のfstabを参考に。
$ sudo adduser timemachine                 # パスワードはわかるもの、アカウント情報は空白でよい。
$ sudo smbpasswd -a timemachine            # SMBパスワードの設定
$ sudo mkdir /mnt/timemachine
$ sudo chown -R timemachine: /mnt/timemachine
$ sudo mv smb.conf /etc/samba/smb.conf
$ sudo service smbd reload
$ sudo mv samba.service /etc/avahi/services/samba.service
$ sudo service avahi-daemon restart
```

USB HDDを引き継いだ場合、Macでバックアップ実行時にエラーが出ることがある。13の場合、コンソールでPermission Deniedだとわかるので、Time Machineのディレクトリがnobody/nogroupになっていないか確認する。なっていれば、下記コマンドでtimemachineに変更する。

```
$ sudo chown -R timemachine /mnt/timemachine/HoneyCat.sparsebundle/
$ sudo chgrp -R timemachine /mnt/timemachine/HoneyCat.sparsebundle/
```
