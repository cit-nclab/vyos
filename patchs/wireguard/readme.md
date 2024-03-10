# Wireguardのpatch

## HandshakeパケットのDSCP値を変更

### patchファイル

```
./wireguard-linux-compat/1001-wireguard-dscp-change.patch
```

### 詳細

NTTのNGN網内ではDSCP値が0x88のIPv6パケットはひかり電話用に割り当てられており、通常のインターネット通信で利用できない。(破棄される)
WireguardのHandshakeパケットはDSCP値が0x88である。

そこで、WireguardのHandshakeパケットのDSCP値を0x00に変更する必要がある。

HandshakeパケットのDSCP値を0x88から0x00に変更する方法として以下を検討した。
- Wireguardのソースコードを書き換える  
    メンテナンスコストが高い
- VyOSでDSCP値を書き換える  
    設定項目が見当たらない
- さらに上位のルーターでDSCP値を書き換える  
    上位ルータが設定の書き換えに対応しているとは限らない  
    特定のプロジェクトでnk-vyosを使用する場合、メンテナンス責任範囲が拡大する  

検討の結果、Wireguardのソースコードを変更することとした。  
メンテナンコストは以下で改善する。
- Jenkensの使用
- patchファイルの使用

### 検証結果

以下は通信開始時のパケットをダンプしたものである。

```
test-result/before-patch.txt
test-result/after-patch.txt
```

beforeの方では、一部のIPv6パケット(Handshakeと思われる)のDSCP値が0x88になっている。  
afterの方では、全てのIPv6パケットのDSCP値が0x00になっていることがわかる。

### 関連するIssue

https://github.com/cit-nclab/nekko-cloud/issues/1
