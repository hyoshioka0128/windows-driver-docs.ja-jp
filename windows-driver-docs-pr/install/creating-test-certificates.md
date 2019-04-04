---
title: テスト証明書の作成
description: テスト証明書の作成
ms.assetid: 4e6daa96-029c-4e1c-b483-b900cb836858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb5da0a1585b825404a27ffe197fc08867b197ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580890"
---
# <a name="creating-test-certificates"></a>テスト証明書の作成


テスト署名テスト証明書が必要です。 できるテスト証明書が生成されると、複数のドライバーをテストするために使用または[ドライバー パッケージ](driver-packages.md)します。 詳細については、[テスト証明書](test-certificates.md)を参照してください。

このトピックでは、使用する方法を説明します、 [ **MakeCert** ](https://msdn.microsoft.com/library/windows/hardware/ff548309)テスト証明書を作成するためのツール。 ほとんどの開発環境では、MakeCert を使用して生成テスト証明書をインストールおよびテスト署名されたドライバーまたはドライバー パッケージの読み込みをテストするための十分な必要があります。 この種類のテスト証明書の詳細については、[テスト証明書の MakeCert](makecert-test-certificate.md)を参照してください。

次のコマンドラインの例では、MakeCert を使用して、次のタスクを完了します。

-   という名前のテスト用の自己署名証明書作成*Contoso.com(Test)* します。 この証明書は、同じサブジェクト名と証明書機関 (CA) の名前を使用します。

-   という名前の出力ファイルに証明書のコピーを配置*ContosoTest.cer*します。

-   という名前の証明書ストア、証明書のコピーを配置*PrivateCertStore*します。 テスト証明書を配置する*PrivateCertStore*可能性がある場合、システムの他の証明書から独立した状態に保ちます。

次の MakeCert コマンドを使用して作成する、 *Contoso.com(Test)* 証明書。

```cpp
makecert -r -pe -ss PrivateCertStore -n CN=Contoso.com(Test) -eku 1.3.6.1.5.5.7.3.3 ContosoTest.cer
```

各項目の意味は次のとおりです。

-   **-R**オプションは、発行者とサブジェクトの同じ名前の自己署名証明書を作成します。

-   **-Pe**オプションは、証明書に関連付けられている秘密キーをエクスポートすることを指定します。

-   **-Ss**オプションは、テスト証明書を含む証明書ストアの名前を指定します (*PrivateCertStore*)。

-   **-N CN =** オプション Contoso.com(Test)、証明書の名前を指定します。 この名前を併用、 [ **SignTool** ](../devtest/signtool.md)証明書を識別するためのツール。

-   EKU オプションは、結果のコード署名証明書の使用率を制限します。

-   *ContosoTest.cer* Contoso.com(Test) テストの証明書のコピーを含むファイルの名前です。 証明書ファイルを使用して、信頼されたルート証明機関証明書ストアと信頼された発行元の証明書ストアに証明書を追加します。

テスト証明書を含む証明書ストアは、証明書ストアが作成された開発用コンピューター上のユーザー アカウントの Windows の管理証明書ストアの一覧に追加されます。

すべての署名に 1 つだけの MakeCert テスト証明書を作成する開発者がある[ドライバー パッケージ](driver-packages.md)開発用コンピューター。

MakeCert ツールとコマンドライン引数の詳細については、[ **MakeCert**](https://msdn.microsoft.com/library/windows/hardware/ff548309)を参照してください。

Readme ファイルも参照してください*Selfsign_readme.htm*で、 *bin\\selfsign* Windows Driver Kit (WDK) のディレクトリ。

 

 





