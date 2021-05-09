# Raspberry Pi 4の設定集

## OS

- Ubuntu Server 20.04.2 LTS 64bit

Raspberry Pi ImagerからMicroSDカードに書き込む。USBブート等は一旦行わない。

## Hostname

```
$ sudo hostnamectl set-hostname RPi4
```

hostnamectlで設定すると、.localのmDNS名も変わる。

## Timezone

標準がUTCなので、時計表示で困る。

```
$ sudo timedatectl set-timezone Asia/Tokyo
```
