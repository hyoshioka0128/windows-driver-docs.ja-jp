---
title: 証明書ストアに、SPC をインポートします。
description: 証明書ストアに、SPC をインポートします。
ms.assetid: 4640b48c-e56f-4c6b-8943-f8b6fc3e37d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f60a60c92312a6fb79e66c12e04d80dcc1b81bf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552068"
---
# <a name="importing-an-spc-into-a-certificate-store"></a>証明書ストアに、SPC をインポートします。


1 回、Personal Information Exchange (.*pfx*) を格納するファイルを作成、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)と、プライベートおよびパブリック キー、 *.pfx*ファイルは、個人証明書ストアにインポートする必要があります、コンピューターを署名します。 詳細については *.pfx*ファイルを参照してください[Personal Information Exchange (.pfx) ファイル](personal-information-exchange---pfx--files.md)します。

インポートする、 *.pfx*をローカルの個人証明書ストアにファイルを次の操作します。

1.  Windows エクスプ ローラーを起動し、ダブルクリック、 *.pfx*証明書のインポート ウィザードを開くファイル。

2.  コード署名証明書を個人証明書ストアにインポートする証明書のインポート ウィザードの手順に従います。

証明書と秘密キーでは、SignTool を使用するのに使用できるようになりました。

Windows Vista では、インポートする別の方法で始まる、 *.pfx*ファイルをローカルの個人証明書ストアには、 [CertUtil](https://go.microsoft.com/fwlink/p/?linkid=168888)コマンド ライン ユーティリティです。 次のコマンドライン例をインポートする CertUtil を使用して、 *abc.pfx*個人証明書ストアにファイル。

```cpp
certutil -user -p pfxpassword -importPFX abc.pfx
```

各項目の意味は次のとおりです。

-   **-ユーザー**オプションは、個人用ストアの「現在のユーザー」を指定します。

-   **-P**のパスワードを指定するオプション、 *.pfx*ファイル (*pfxpassword*)。

-   **-Importpfx**オプションの名前を指定します、 *.pfx*ファイル (*abc.pfx*)。

1 回、 *.pfx*署名のコンピューター上の個人証明書ストアにファイルをインポート、使用することができます[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)リリースへの署名を[ドライバーパッケージ](driver-packages.md)します。

 

 





