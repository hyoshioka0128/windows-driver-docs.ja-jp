---
title: サード パーティ製の CSP の Authenticode での署名
description: カスタム暗号化サービスプロバイダー (Csp) のサードパーティの Authenticode 署名は、Windows Vista 以降で使用可能になりました。このダウンロードでは、2013年5月以降、Windows XP SP3 および Windows Server 2003 SP2 に移植されています。
ms.assetid: DBAA575A-F0B5-4725-A7B1-D6EA84977212
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa86373ca04df46c39909f9f8dc999d34cd77227
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025344"
---
# <a name="authenticode-signing-of-third-party-csps"></a>サード パーティ製の CSP の Authenticode での署名


カスタム暗号化サービスプロバイダー (Csp) のサードパーティの Authenticode 署名は、Windows Vista 以降で使用可能になりました。[このダウンロード](https://support.microsoft.com/help/2836198)では、2013年5月以降、WINDOWS XP SP3 および windows SERVER 2003 SP2 に移植されています。

その結果、Microsoft は Csp に署名しなくなり、CSP 署名サービスは手動で廃止されました。 署名にcspsign@microsoft.com cecspsig@microsoft.com送信された電子メールと csp は、Microsoft によって処理されなくなります。

代わりに、次の手順に従って、すべてのサードパーティの Csp を自己署名できるようになりました。

1.  Microsoft がクロス証明書を発行する証明機関 (CA) からコード署名証明書を購入します。 「[カーネルモードのクロス証明書のコード署名](cross-certificates-for-kernel-mode-code-signing.md)」トピックでは、Microsoft がクロス証明書と対応するクロス証明書を提供する ca の一覧を示します。 これらは、Microsoft によって発行された "Microsoft コード検証ルート" にチェーンされる唯一のクロス証明書であり、Windows でサードパーティの Csp を実行することができます。
2.  CA から証明書を取得し、一致するクロス証明書を取得した後、 [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)を使用してすべての CSP バイナリに署名することができます。
3.  SignTool は、最新バージョンの Visual Studio に含まれています。 また、WDK バージョン7.0 以降のバージョンにも含まれています。 以前のバージョンの WDK に付属する SignTool は、クロス証明書と互換性がないため、バイナリの署名には使用できないことに注意してください。

**注 Windows 8**以降では、csp に署名が必要であるという要件はなくなりました。  

 

コマンドラインからバイナリに署名することも、Visual Studio 2012 以降の統合ビルドステップとして署名することもできます。

[**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)するコマンドは次のとおりです。

```cpp
signtool.exe sign /ac <cross-certificate_from_ms> /sha1 <sha1_hash> /t <timestamp_server> /d <”optional_description_in_double_quotes”> <binary_file.ext>
```

-   &lt;クロス certificate_from_ca&gt;は、Microsoft からダウンロードしたクロス証明書ファイルです。
-   &lt;sha1_hash&gt;は、コード署名証明書に対応する SHA1 拇印です。
-   &lt;timestamp_server&gt;は、署名操作のタイムスタンプに使用されるサーバーです。
-   &lt;"optional_description_in_double_quotes"&gt;は省略可能なフレンドリ名の説明です。
-   &lt;binary_file&gt;は、署名するファイルです。

以下に例を示します。

```cpp
signtool.exe sign /ac certificate.cer /sha1 553e39af9e0ea8c9edcd802abbf103166f81fa50 /t "http://timestamp.digicert.com" /d "My Cryptographic Service Provider" csp.dll
```

**ただし、古い**csp 署名に必要で\#あったように、csp DLL またはレジストリの署名にリソース ID 666 を含める必要はありません。  

 

## <a name="additional-help-and-support"></a>その他のヘルプとサポート


追加のヘルプとサポートについては、[トラブルシューティングとサポート](https://msdn.microsoft.com/hh361695)に関するページを参照してください。

詳細については、 [Windows デスクトップのアプリケーションセキュリティに](https://social.msdn.microsoft.com/Forums/home?forum=windowssecurity)関するフォーラムを確認することもできます。

 

 





