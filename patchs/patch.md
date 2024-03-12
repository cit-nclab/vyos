# Create patch file

## ソースファイルの差分からpatchファイルを作成

```
diff -up wireguard-linux-compat_a/src/messages.h wireguard-linux-compat_b/src/messages.h > 1001-wireguard-dscp-change.patch
```

## 作成したpatchファイルを移動

```
mv 1001-wireguard-dscp-change.patch packages/linux-kernel/patches/wireguard-linux-compat/
```
