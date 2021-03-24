# SMBの設定

smbでTime Capsuleを実装するための設定。

## 設定

### SMB

- https://saschaeggi.medium.com/use-a-raspberry-pi-4-for-time-machine-works-with-big-sur-1e66a9650789
- https://www.reddit.com/r/linuxquestions/comments/juyue6/samba_share_as_time_machine_backup_getting/

Mediumの投稿でSMBの動作までは動いたが、Time Machineだけが動かない。SMBがGuestでも書き込めるようchmod 777も実行し、その後Redditの設定も追加したら動いた。Redditの内容も反映済みのファイルが[smb.conf](./smb.conf)なので、SMBが動いていれば/etc/samba/smb.confと置き換えればよい。

### HDD

- ext4 (HFS+でなくても動いた)
