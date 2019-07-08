---
title: ドライバー ファイルのリリース署名
description: ドライバー ファイルのリリース署名
ms.assetid: 3da0377d-57cf-4bd4-b3ce-6ba4ebbc3ceb
keywords:
- パブリック リリース ドライバーの WDK、ドライバー ファイルの署名
- WDK の署名ドライバー ファイルのリリース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21cfc1d62b2b9e0bf5a3d210bd5ca164c089a13c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375714"
---
# <a name="release-signing-a-driver-file"></a>ドライバー ファイルのリリース署名


次を使用して、 **SignTool**は 64 ビット バージョンの Windows Vista と以降のバージョンの Windows embedded の SPC 署名機能がある必要です。

```cpp
SignTool sign /v /ac CrossCertificateFile /s SPCCertificateStore /n SPCCertificateName /t http://timestamp.verisign.com/scripts/timstamp.dll DriverFileName.sys
```

各項目の意味は次のとおりです。

-   **サインオン**コマンド構成ファイルに署名を埋め込む SignTool *DriverFileName.sys*します。

-   **/V** /verbose オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/Ac** *CrossCertificateFile*オプションは、クロス証明書を指定します *.cer*ファイルで指定された SPC に関連付けられている*SPCCertificateName*します。

-   **/S** *SPCCertificateStore*オプションで指定されている、SPC を保持する個人証明書ストアの名前を指定する*SPCCertificateName*します。 」の説明に従って[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)、証明書の情報を含める必要があります、 *.pfx*ファイル、および内の情報、 *.pfx*ファイルである必要がありますローカル コンピューターの個人証明書ストアに追加されます。 個人証明書ストアが、オプションで指定された **/s 自分**します。

-   **/N** *SPCCertificateName*オプションで証明書の名前を指定、 *SPCCertificateStore*証明書ストア。

-   **/T**  *http://timestamp.verisign.com/scripts/timstamp.dll* オプションは、VeriSign を提供するパブリックに利用可能なタイム スタンプ サーバーの URL を提供します。

-   *DriverFileName.sys*ドライバー ファイルの名前を指定します。

次のコマンドは、内のシグネチャを埋め込みます*Toaster.sys*は"my"証明書ストアと対応するクロス証明書は、"contoso.com"をという名前で、個人証明書から生成された*Rsacertsvrcross.cer*します。 さらに、署名は、タイム スタンプ サービスによってタイムスタンプ http://timestamp.verisign.com/scripts/timstamp.dll します。 この例で*Toaster.sys*では、 *amd64*コマンドが実行されるディレクトリのサブディレクトリ。

```cpp
SignTool sign /v /ac c:\lab\rsacertsrvcross.cer /s my /n contoso.com /t http://timestamp.verisign.com/scripts/timstamp.dll amd64\toaster.sys
```

 

 





