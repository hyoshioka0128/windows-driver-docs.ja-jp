---
title: テスト証明書のインストール
description: テスト証明書のインストール
ms.assetid: 4c306390-32cc-4c7a-9f61-48e8af385a6d
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: c433aad292c490f831f81b0bc8250e894df13567
ms.sourcegitcommit: 6914901515545eda08b2c35bef816e6e2711a5b6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86944620"
---
# <a name="installing-test-certificates"></a>テスト証明書のインストール


テスト署名された[ドライバーパッケージ](driver-packages.md)をテストコンピューターに正常にインストールするには、コンピューターが署名を検証できる必要があります。 これを行うには、コンピューターの信頼されたルート証明機関の証明書ストアにインストールされたパッケージのテスト証明書を発行した証明機関 (CA) の証明書がテストコンピューターに必要です。

CA 証明書は、信頼されたルート証明機関の証明書ストアに1回だけ追加する必要があります。 追加されると、ドライバーパッケージがコンピューターにインストールされる前に、証明書によってデジタル署名されたすべてのドライバーまたはドライバーパッケージの署名を検証するために使用できます。

信頼されたルート証明機関の証明書ストアにテスト証明書を追加する最も簡単な方法は、 [**certmgr.exe**](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)ツールを使用することです。 このトピックでは、テスト証明書 (Contoso .com) をインストールする手順について説明します。 この証明書は、 *ContosoTest*ファイル内に格納されます。 この証明書の作成方法の詳細については、「[テスト証明書の作成](creating-test-certificates.md)」を参照してください。

次のコマンドラインでは、Certmgr.exe を使用して、テストコンピューターの信頼されたルート証明機関の証明書ストアに、Contoso .com (テスト) 証明書をインストールまたは追加します。

```cpp
certmgr /add ContosoTest.cer /s /r localMachine root
```

各値の説明:

-   /Add オプションは、 *ContosoTest*ファイル内の証明書を指定された証明書ストアに追加することを指定します。

-   **/S**オプションは、証明書をシステムストアに追加することを指定します。

-   /R オプションは、システムストアの場所を指定します。これは*currentUser*または*localMachine*のいずれかです。

-   *ルート*ローカルコンピューターの保存先ストアの名前を指定します。これは、信頼された発行元の証明書ストアを指定するために、ルート証明機関の証明書ストアまたは***trustedpublisher***を指定する***ルート***のいずれかです。

正常に実行されると、次の出力が生成されます。

```cmd
certmgr /add ContosoTest.cer /s /r localMachine root
CertMgr Succeeded
```

証明書を信頼されたルート証明機関の証明書ストア (ユーザーストアでは*なく*ローカルコンピューターのルートストア) にコピーした後、「[テスト証明書の表示](viewing-test-certificates.md)」で説明されているように、MICROSOFT 管理コンソール (MMC) の証明書スナップインを使用して証明書を表示できます。

次のスクリーンショットは、信頼されたルート証明機関の証明書ストアにある Contoso .com (Test) 証明書を示しています。

![mmc 証明書スナップイン内の信頼されたルート証明機関の証明書ストアのスクリーンショット](images/certstore2.png)

コマンドプロンプトで証明書を表示することもできます。

```cmd
certutil -store root | findstr Contoso
certutil -store root <SHA-1 id of certificate>
```

または、PowerShell から:

```cmd
Get-ChildItem -path cert: \LocalMachine\My | findstr Contoso
```

Certmgr.exe ツールは Windows SDK の一部であり、通常はにインストールされ `C:\Program Files (x86)\Windows Kits\10\bin\<build>\x86\certmgr.exe` ます。

Certmgr.exe とそのコマンドライン引数の詳細については、 [**certmgr.exe**](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)を参照してください。

テスト証明書のインストール方法の詳細については、「テスト[コンピューターへのテスト証明書のインストール](installing-a-test-certificate-on-a-test-computer.md)」を参照してください。

 

 





