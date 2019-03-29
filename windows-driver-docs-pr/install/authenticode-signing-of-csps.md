---
title: サード パーティ製の CSP の Authenticode での署名
description: サード パーティ製 Authenticode のカスタム暗号化サービス プロバイダー (Csp) の署名は、以降、Windows Vista で利用可能されており、Windows XP SP3 および、2013 年 5 月の時点での Windows Server 2003 SP2 にこのダウンロードを使用して戻る移植されました。
ms.assetid: DBAA575A-F0B5-4725-A7B1-D6EA84977212
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6dc171573b04401fd293800dd12012ec496b535
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574207"
---
# <a name="authenticode-signing-of-third-party-csps"></a>サード パーティ製の CSP の Authenticode での署名


使用して Windows XP SP3 および、2013 年 5 月の時点での Windows Server 2003 SP2 に移植カスタム暗号化サービス プロバイダー (Csp) されて以降、Windows Vista で利用可能とバックアップされていますが、サード パーティ製の Authenticode 署名[このダウンロード](http://support.microsoft.com/kb/2836198).

その結果、Microsoft は、Csp に署名できなくおよび署名サービス手動 CSP は廃止されました。 送信される電子メールや Cspcspsign@microsoft.comまたはcecspsig@microsoft.comに署名できなくによって処理される Microsoft。

代わりに、すべてのサード パーティ製 Csp 今すぐ自己署名できる次の手順で。

1.  コード署名証明書、証明書機関 (CA) から Microsoft も発行するクロス証明書を購入します。 [カーネル モード コード署名用クロス証明書](cross-certificates-for-kernel-mode-code-signing.md)トピックでは、Microsoft も提供するクロス証明書と対応するクロス証明書の Ca の一覧を示します。 これらは、のみクロス証明書を"Microsoft コード検証 Root"により、サード パーティ製の Csp を実行する Windows、Microsoft によって発行されるまでチェーンであることに注意してください。
2.  使用することができます、CA と一致するクロス証明書から証明書を作成したら、 [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778) CSP のすべてのバイナリに署名します。
3.  SignTool は、最新バージョンの Visual Studio に含まれます。 WDK バージョン 7.0 と新しいバージョンにも含まれます。 以前のバージョンの WDK に付属する SignTool はクロス証明書と互換性がないと、バイナリの署名に使用されることはできませんに注意してください。

**注**  Windows 8 以降、できなくなった要件の Csp を署名する必要があります。

 

、コマンドラインからのバイナリに署名したり、Visual Studio 2012 以降の、統合ビルド ステップとしてサインインできます。

コマンドを[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)は。

```cpp
signtool.exe sign /ac <cross-certificate_from_ms> /sha1 <sha1_hash> /t <timestamp_server> /d <”optional_description_in_double_quotes”> <binary_file.ext>
```

-   &lt;クロス certificate_from_ca&gt;は Microsoft からダウンロードしたクロス証明書ファイル
-   &lt;sha1_hash&gt;はコード署名証明書に対応する SHA1 拇印です
-   &lt;timestamp_server&gt;タイムスタンプ署名操作に使用されるサーバー
-   &lt;"optional_description_in_double_quotes"&gt;省略可能な説明のわかりやすい名前
-   &lt;binary_file.ext&gt;署名するファイルは、

以下に例を示します。

```cpp
signtool.exe sign /ac certificate.cer /sha1 553e39af9e0ea8c9edcd802abbf103166f81fa50 /t "http://timestamp.verisign.com/scripts/timstamp.dll" /d "My Cryptographic Service Provider" csp.dll
```

**注**  リソース ID を含める必要はありません\#666 CSP DLL、またはが以前の CSP の署名に必要なため、レジストリで署名します。

 

## <a name="additional-help-and-support"></a>追加のヘルプとサポート


参照してください、[トラブルシューティングとサポート](https://msdn.microsoft.com/hh361695)追加のヘルプとサポートのページ。

確認することも、[アプリケーション セキュリティ for Windows Desktop](http://social.msdn.microsoft.com/Forums/home?forum=windowssecurity)アシスタンスのフォーラムです。

 

 





