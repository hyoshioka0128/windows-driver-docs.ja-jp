---
title: テスト署名ドライバー パッケージ
description: このセクションの説明テスト ドライバー パッケージを署名する方法。
ms.assetid: 3BC92099-A464-4C62-9EB7-DD6AA0D1FB03
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9ac12f24d66237581ba90831b04a7da3237192ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539598"
---
# <a name="test-sign-a-driver-package"></a>テスト署名ドライバー パッケージ


このセクションの説明テスト ドライバー パッケージを署名する方法。

## <a name="test-sign-a-driver-package"></a>テスト署名ドライバー パッケージ


次の手順をテスト署名テスト証明書を使用してドライバー パッケージを使用します。

1.  新しい証明書ファイルを作成します。

    ```console
    makecert -r -pe -ss TestCertStoreName -n "CN=WSD FabrikamV4 Driver Testing Cert" CertFileName.cer -sv CertFile.pvk
    ```

    パスワードを入力するように促されます。

2.  Pfx ファイルを作成するのにには、pvk ファイルを使用します。

    ```console
    pvk2pfx.exe /pvk CertFile.pvk /spc CertFileName.cer /pfx CertPfx.pfx
    ```

    パスワードを入力するように促されます。

3.  コンピューターのルートおよび trustedpublisher の証明書ストアに証明書を追加で、ドライバーがインストールされます。

    これにより、プラグ アンド プレイ インストール中に署名の検証に合格するドライバーができます。 このステップのドライバーがこのチェックに合格しないは自動的に失敗がない場合に、プリンターをインストールします。

    ```console
    CertMgr /add CertFileName.cer /s /r localMachine root
    CertMgr /add CertFileName.cer /s /r localMachine trustedpublisher
    ```

4.  手順 2. で作成した pfx ファイル「FabrikamPrintDriverV4 パッケージ」に署名します。 他のプロジェクトは、としては、この手順で署名されたドライバーはどのようなパッケージを作成する必要はありません。

詳細については、次を参照してください。[テスト署名ドライバー パッケージ方法](https://docs.microsoft.com/windows-hardware/drivers/install/how-to-test-sign-a-driver-package)します。


