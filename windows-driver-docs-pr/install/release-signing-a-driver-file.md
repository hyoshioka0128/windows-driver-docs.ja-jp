---
title: ドライバー ファイルのリリース署名
description: ドライバー ファイルのリリース署名
ms.assetid: 3da0377d-57cf-4bd4-b3ce-6ba4ebbc3ceb
keywords:
- パブリックリリースドライバー署名 WDK、ドライバーファイル
- ドライバーファイルのリリース署名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 086bae5bf2b76aca3bc3031f88a131087ab340d2
ms.sourcegitcommit: 2231d322eb4e9597ad7f537a4aa82b83422bd46a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70020635"
---
# <a name="release-signing-a-driver-file"></a>ドライバー ファイルのリリース署名


Windows Vista 以降のバージョンの windows では、次の**SignTool** 64 を使用して、SPC 署名を埋め込む必要があります。

```cpp
SignTool sign /v /ac CrossCertificateFile /s SPCCertificateStore /n SPCCertificateName /t http://timestamp.digicert.com DriverFileName.sys
```

各項目の意味は次のとおりです。

-   **Sign**コマンドは、SignTool を構成して、ファイル*driverfilename*に署名を埋め込みます。

-   **/V** verbose オプションは、実行および警告メッセージを出力するように SignTool を構成します。

-   **/Ac** *クロス certificatefile*オプションでは、 *spcisdeleted ename*によって指定された SPC に関連付けられているクロス証明書 *.cer*ファイルを指定します。

-   **/S** *spccertificatestore*オプションは、 *spcに*よって指定された SPC を保持する個人証明書ストアの名前を指定します。 「[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)」で説明されているように、証明書情報は *.pfx*ファイルに含まれている必要があります。 *.pfx*ファイル内の情報は、ローカルコンピューターの個人証明書ストアに追加する必要があります。 個人証明書ストアは、 **/s my**というオプションで指定されます。

-   **/N** *Spcは*、 *spccertificatename*証明書ストア内の証明書の名前を指定します。

-   **/T**  *http://timestamp.digicert.com オプションは、VeriSign を提供するパブリックに利用可能なタイム スタンプ サーバーの URL を提供します。

-   *Driverfilename .sys*は、ドライバーファイルの名前です。

次のコマンドは、個人の "my" 証明書ストアの "contoso.com" という名前の証明書から生成された*トースター*の署名と、対応するクロス証明書*Rsacertsvrcross*を埋め込みます。 また、署名はタイムスタンプサービス http://timestamp.digicert.com によってタイムスタンプが付けられます。 この例では、*トースター*は、コマンドが実行されるディレクトリの下の*amd64*サブディレクトリにあります。

```cpp
SignTool sign /v /ac c:\lab\rsacertsrvcross.cer /s my /n contoso.com /t http://timestamp.digicert.com amd64\toaster.sys
```

 

 





