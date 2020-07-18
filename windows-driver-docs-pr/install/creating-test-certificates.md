---
title: テスト証明書の作成
description: テスト証明書の作成
ms.assetid: 4e6daa96-029c-4e1c-b483-b900cb836858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30b8d68e952c4efaa6eba5c7d3cb510f385e80f0
ms.sourcegitcommit: 701e4a41860877cc1134e139bc0bd4a9f7270443
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86453984"
---
# <a name="creating-test-certificates"></a>テスト証明書の作成


テスト署名にはテスト証明書が必要です。 テスト証明書を生成した後は、複数のドライバーまたは[ドライバーパッケージ](driver-packages.md)のテスト署名に使用できます。 詳細については、「[テスト証明書](test-certificates.md)」を参照してください。

このトピックでは、 [**MakeCert**](https://docs.microsoft.com/windows-hardware/drivers/devtest/makecert)ツールを使用してテスト証明書を作成する方法について説明します。 ほとんどの開発環境では、テスト署名されたドライバーまたはドライバーパッケージのインストールと読み込みをテストするには、MakeCert によって生成されるテスト証明書が十分である必要があります。 この種類のテスト証明書の詳細については、「 [MakeCert Test certificate](makecert-test-certificate.md)」を参照してください。

次のコマンドラインの例では、MakeCert を使用して、次のタスクを実行します。

-   *Contoso .com (test)* という名前の自己署名テスト証明書を作成します。 この証明書では、サブジェクト名と証明機関 (CA) に同じ名前が使用されます。

-   *ContosoTest*という名前の出力ファイルに証明書のコピーを配置します。

-   *PrivateCertStore*という名前の証明書ストアに証明書のコピーを配置します。 テスト証明書を*PrivateCertStore*に配置すると、システム上にある他の証明書とは分離されます。

次の MakeCert コマンドを使用して、 *Contoso .com (テスト)* 証明書を作成します。

```cmd
makecert -r -pe -ss PrivateCertStore -n CN=Contoso.com(Test) -eku 1.3.6.1.5.5.7.3.3 ContosoTest.cer
```

各値の説明:

-   **-R**オプションを指定すると、同じ発行者とサブジェクト名を持つ自己署名証明書が作成されます。

-   **-Pe**オプションは、証明書に関連付けられている秘密キーをエクスポートできることを指定します。

-   **-Ss**オプションは、テスト証明書 (*PrivateCertStore*) を含む証明書ストアの名前を指定します。

-   **-N CN =** オプションは、証明書の名前 (Contoso .com) を指定します。 この名前は、証明書を識別するために[**SignTool**](../devtest/signtool.md)ツールと共に使用されます。

-   EKU オプションは、1つまたは複数のコンマ区切りの[*拡張キー使用法*](https://docs.microsoft.com/windows/desktop/SecGloss/e-gly)オブジェクト識別子 (oid) の一覧を証明書に挿入します。 たとえば、では、 `-eku 1.3.6.1.5.5.7.3.2` クライアント認証 OID が挿入されます。 許容される Oid の定義については、CryptoAPI 2.0 の Wincrypt ファイルを参照してください。

-   *ContosoTest*は、テスト証明書 (Contoso .com) のコピーを含むファイル名です。 証明書ファイルは、信頼されたルート証明機関の証明書ストアおよび信頼された発行元の証明書ストアに証明書を追加するために使用されます。

テスト証明書を含む証明書ストアは、証明書ストアが作成された開発用コンピューター上のユーザーアカウントに対して Windows が管理する証明書ストアの一覧に追加されます。

開発者は、開発用コンピューター上のすべての[ドライバーパッケージ](driver-packages.md)に署名するために、MakeCert テスト証明書を1つだけ作成する必要があります。

MakeCert ツールとそのコマンドライン引数の詳細については、 [**MakeCert**](https://docs.microsoft.com/windows-hardware/drivers/devtest/makecert)を参照してください。

また、Windows Driver Kit (WDK) の*bin \\ selfsign*ディレクトリにある readme ファイル*Selfsign_readme.htm*も参照してください。

 

 





