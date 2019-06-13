---
title: 署名されたコードのテストの読み込み
description: 有効にする方法を説明しますテストの読み込み TESTSIGNING オプションを使用して、BCDEdit ツールを使用したドライバーの署名。
ms.assetid: 4898595e-20c9-4607-aad7-792f7d1074e4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcab1f049a0ec4bf7e85b679aac723a593245338
ms.sourcegitcommit: ba351c01be491b8ab5c74d778ab02c8766a5667a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "67041372"
---
# <a name="enable-loading-of-test-signed-drivers"></a>テスト署名されたドライバーの読み込みの有効化

既定では、Windows では、テスト署名されたカーネル モード ドライバーは読み込まれません。 この動作を変更し、読み込むテスト署名されたドライバーを有効にするには、ブート構成データ エディター、BCDEdit.exe を使用して、有効または TESTSIGNING、ブート構成のオプションを無効にします。 このオプションを有効にするには、管理者権限が必要です。

> [!Note]
> 64 ビット バージョンの Windows Vista と Windows の以降のバージョンでは、カーネル モード コード署名ポリシーでは、すべてのカーネル モード コードにデジタル署名があることが必要です。 ただし、ほとんどの場合、未署名のドライバをインストールして、Windows Vista の 32 ビット バージョンおよび以降のバージョンの Windows にロードすることができますが。 詳細については、次を参照してください。[ドライバー署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)します。


## <a name="administrator-rights-required"></a>必要な管理者権限

BCDEdit を使用しては、システムの Administrators グループのメンバーであるし、管理者特権のコマンド プロンプトからコマンドを実行する必要があります。 管理者特権のコマンド プロンプト ウィンドウを開き、「 **cmd** Windows タスク バーの [検索] ボックスに、右クリック**コマンド プロンプト**クリックして、検索結果で**管理者として実行**.

> [!Warning]
> BCDEdit を使用して、ブート構成データを変更するには、管理者権限が必要です。 使用してブート エントリのいくつかのオプションを変更する**BCDEdit/set**しなくなる可能性コンピューター。 代わりに、システム構成ユーティリティ (MSConfig.exe) を使用して、ブート設定を変更します。


## <a name="enable-or-disable-use-of-test-signed-code"></a>有効にするか、テスト署名されたコードの使用を無効にします。

有効またはテスト署名されたコードの読み込みを無効にする BCDEdit のコマンド行を実行します。 変更を有効にするか、オプションを無効にするかどうか有効にするには、構成の変更後にコンピューターを再起動する必要があります。

> [!Note]
> BCDEdit のオプションを設定する前に、無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要があります。

テスト署名されたコードを有効にするには、次の BCDEdit コマンド ラインを使用します。

```cpp
Bcdedit.exe -set TESTSIGNING ON
```

テスト署名されたコードの使用を無効にするには、次の BCDEdit コマンド ラインを使用します。

```cpp
Bcdedit.exe -set TESTSIGNING OFF
```

次の図は、BCDEdit のコマンド ラインを使用して、テスト署名を有効にする結果を示します。

![Testsigning、ブート構成のオプションを使用した結果のスクリーン ショット](images/driver-signing-enable-vista-test-signing.png)


## <a name="behavior-of-windows-when-loading-test-signed-code-is-enabled"></a>テスト署名されたコードの読み込み時に Windows の動作が有効になっています。

テスト署名されたコードの読み込みを有効にすると、Windows は、次を行います。

-   「テスト モード」で 4 つすべての角のデスクトップのシステムがテスト署名を有効になっているユーザーに通知するテキストの透かしが表示されます。
    **注**  Windows 7 以降、Windows この透かしでのみ表示されます、デスクトップの右下隅。

-   ユーザーに通知する、システムのテスト署名を有効になっているデスクトップの左上隅にある「テスト モード」のテキストの透かしが表示されます。

-   オペレーティング システム ローダー、カーネルは、任意の証明書によって署名されているドライバーをロードします。 証明書の検証は、信頼されたルート証明機関までのチェーンする必要はありません。 ただし、各ドライバーのイメージ ファイルには、デジタル署名が必要です。
