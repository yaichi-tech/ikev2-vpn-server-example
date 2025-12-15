# VPN サーバー

[English](README.md)

DockerによるIKEv2 VPNサーバーです。OSの標準機能でVPN接続できます。

## サーバー設定

サーバーのファイアウォールで以下のポートを開放してください:

- `500/udp` - IKE (Internet Key Exchange)
- `4500/udp` - IPsec NAT-Traversal

## クライアント設定

### Windows

Windows 8, 10, 11 以降は自動でIKEv2設定をインポートできます。

1. マウントされた `ikev2-vpn-data/` ディレクトリ内の `.p12` ファイルをPCに転送する
2. [ikev2_config_import.cmd](https://github.com/hwdsl2/vpn-extras/releases/latest/download/ikev2_config_import.cmd) を右クリックして `.p12` ファイルと同じフォルダに保存
3. 保存したスクリプトを右クリック → プロパティ → 下部の「ブロックの解除」をクリック → OK
4. スクリプトを右クリック → 「管理者として実行」を選択し、プロンプトに従う

**スクリプト実行時の入力項目:**
| 項目 | 値 |
|------|-----|
| VPN client name | compose.yml の `VPN_CLIENT_NAME` |
| VPN server address | compose.yml の `VPN_DNS_NAME` |
| IKEv2 connection name | 何でもOK。そのままEnterを押すと "IKEv2 VPN {VPN_DNS_NAME}" になる |

**VPN接続方法:**
システムトレイのネットワークアイコンをクリック → 新しいVPNエントリを選択 → 「接続」をクリック

- 公式ドキュメント: https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/ikev2-howto.md#windows-7-8-10-and-11
- 動画: https://ko-fi.com/post/IKEv2-Auto-Import-Configuration-on-Windows-8-10-a-K3K1DQCHW

### Mac

ドキュメントに従って `.mobileconfig` ファイルを開くと、VPN設定が自動的に追加されます。

`.mobileconfig` ファイルはマウントされた `ikev2-vpn-data/` ディレクトリ内にあります。

- ドキュメント: https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/ikev2-howto.md#os-x-macos
- 動画: https://ko-fi.com/post/IKEv2-Auto-Import-Configuration-on-Windows-8-10-a-K3K1DQCHW

## 動作確認

VPN接続が正しく動作しているか確認するには:

1. https://www.cman.jp/network/support/go_access.cgi にアクセス
2. IPアドレスを確認
3. サーバーのIPアドレスと一致していれば、VPNは期待通りに動作しています
