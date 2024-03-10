# NekkoVyOS

## 概要

日本のけしからんインターネット接続事情に対応するよう変更を加えたVyOS

## 変更点

### WireguardのHandshakeパケットのDSCP値を0x00にする。

NGN網はDSCP値が0x88のパケットを破棄するため。
