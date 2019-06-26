---
title: テスト証明書のインストール
description: テスト証明書のインストール
ms.assetid: 4c306390-32cc-4c7a-9f61-48e8af385a6d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da6dc5c4a44e219afc30ac748f9b4823bea04980
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385623"
---
# <a name="installing-test-certificates"></a>テスト証明書のインストール


テスト署名を正常にインストールする[ドライバー パッケージ](driver-packages.md)テスト コンピューターには、コンピューターで、署名を確認できる必要があります。 そのためには、テスト コンピューターが、コンピューターの信頼されたルート証明機関の証明書ストアにインストールされているパッケージのテスト証明書を発行した証明機関 (CA) の証明書をいる必要があります。

CA 証明書は、信頼されたルート証明機関の証明書ストアに 1 回だけ追加する必要があります。 追加されるとのすべてのドライバーまたはドライバー パッケージは、ドライバー パッケージがコンピューターにインストールする前に、証明書で署名されたデジタル署名を確認し、使用できます。

テスト証明書を信頼されたルート証明機関の証明書ストアに追加する最も簡単な方法は、使用、 [ **CertMgr** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)ツール。 このトピックでは、Contoso.com(test) テスト証明書をインストールする手順について説明します。 内でこの証明書が格納されている、 *ContosoTest.cer*ファイル。 この証明書の作成方法の詳細については、次を参照してください。[テスト証明書を作成する](creating-test-certificates.md)します。

次のコマンドラインは、インストール、またはテスト コンピューターの信頼されたルート証明機関の証明書ストアに Contoso.com(test) 証明書を追加します。 Certmgr.exe を使用します。

```cpp
certmgr.exe /add ContosoTest.cer /s /r localMachine root
```

各項目の意味は次のとおりです。

-   ]、[追加オプションを指定する、証明書で、 *ContosoTest.cer*ファイルが指定された証明書ストアに追加するのには。

-   **/S**オプションは、証明書がシステム ストアに追加することを指定します。

-   /R オプションをいずれかであるシステム ストアの場所を指定します*currentUser*または*localMachine*します。

-   *ルート*か、ローカル コンピューターの保存先ストアの名前を指定します***ルート***信頼されたルート証明機関の証明書ストアを指定するか、 ***trustedpublisher***信頼された発行元の証明書ストアを指定します。

証明書を信頼されたルート証明機関の証明書ストアにコピー後できますで表示する、Microsoft 管理コンソール (MMC) の証明書スナップイン」の説明に従って[テスト証明書の表示](viewing-test-certificates.md)します。

次のスクリーン ショットでは、信頼されたルート証明機関の証明書ストアに Contoso.com(Test) 証明書を示しています。

![信頼されたルート証明機関の証明書のスクリーン ショットは、mmc 証明書スナップインで保存します。](images/certstore2.png)

CertMgr とコマンドライン引数の詳細については、次を参照してください。 [ **CertMgr**](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)します。

テスト証明書をインストールする方法の詳細については、次を参照してください。[テスト コンピューターにテスト証明書をインストールする](installing-a-test-certificate-on-a-test-computer.md)します。

 

 





