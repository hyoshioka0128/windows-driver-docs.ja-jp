---
title: TESTSIGNING ブート構成オプション
description: TESTSIGNING ブート構成オプション
ms.assetid: 4898595e-20c9-4607-aad7-792f7d1074e4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 009082b702987ab3abacfadca89f3b6e90c32ac0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574165"
---
# <a name="the-testsigning-boot-configuration-option"></a>TESTSIGNING ブート構成オプション


TESTSIGNING ブートの構成オプションは、Windows Vista および Windows の以降のバージョンがあらゆる種類のテスト署名されたカーネル モード コードを読み込むかどうかを決定します。 既定で、既定で 64 ビット バージョンの Windows Vista と Windows の以降のバージョンはテスト署名されたカーネル モード ドライバーを読み込むことでは、このオプションは設定されていません。

**注**  カーネル モードのすべてのコードにデジタル署名があることの 64 ビット バージョンの Windows Vista と以降のバージョンの Windows では、カーネル モード コード署名ポリシーに必要です。 ただし、ほとんどの場合、未署名のドライバをインストールして、Windows Vista の 32 ビット バージョンおよび以降のバージョンの Windows にロードすることができますが。 詳細については、次を参照してください。[カーネル モード コード署名ポリシー (Windows Vista 以降)](kernel-mode-code-signing-policy--windows-vista-and-later-.md)します。

 

TESTSIGNING ブートの構成オプションが有効になっているまたは BCDEdit コマンドで無効になっています。 テスト署名を有効にするには、次の BCDEdit コマンドを使用します。

```cpp
Bcdedit.exe -set TESTSIGNING ON
```

テスト署名を無効にするには、次の BCDEdit コマンドを使用します。

```cpp
Bcdedit.exe -set TESTSIGNING OFF
```

**注**  TESTSIGNING ブートの構成オプションを変更した後は、変更を反映するには、コンピューターを再起動します。

 

**注意**  BCDEdit を使用して BCD を変更する管理者特権が必要です。 使用してオプションのいくつかのブート エントリを変更、 **BCDEdit/set**コマンドしなくなる可能性コンピューター。 代わりに、システム構成ユーティリティ (MSConfig.exe) を使用して、ブート設定を変更します。

**注**  BCDEdit のオプションを無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要がありますを設定する前にします。

 

 

BCDEdit を使用しては、システムの Administrators グループのメンバーであるし、管理者特権のコマンド プロンプトからコマンドを実行する必要があります。 管理者特権のコマンド プロンプト ウィンドウを開くには、デスクトップ ショートカットを作成*Cmd.exe*を右クリックし、 *Cmd.exe*ショートカット、および選択**管理者として実行**します。

次のスクリーン ショットでは、BCDEdit のコマンド ライン ツールを使用して、テスト署名を有効にする結果を示します。

![testsigning ブートの構成オプションを使用した結果のスクリーン ショット](images/driver-signing-enable-vista-test-signing.png)

テスト署名の BCDEdit のオプションを有効にすると、Windows は、次を行います。

-   「テスト モード」で 4 つすべての角のデスクトップのシステムがテスト署名を有効になっているユーザーに通知するテキストの透かしが表示されます。
    **注**  Windows 7 以降、Windows この透かしでのみ表示されます、デスクトップの左下隅。

     

-   オペレーティング システム ローダー、カーネルは、任意の証明書によって署名されているドライバーをロードします。 証明書の検証は、信頼されたルート証明機関までのチェーンする必要はありません。 ただし、各ドライバーのイメージ ファイルには、デジタル署名が必要です。

 

 





