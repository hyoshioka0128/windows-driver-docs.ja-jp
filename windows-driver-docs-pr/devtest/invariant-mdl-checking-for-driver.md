---
title: 不変な MDL のドライバー用検査
description: 不変な Mdl ドライバー用検査オプションは、ドライバーがドライバーごとの単位で不変の MDL バッファーを処理する方法を監視します。
ms.assetid: 2FA69B7C-3EF4-4660-84D4-5108C97E395F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 216fd8e5dce96044a20df927a8498323015eaec9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373712"
---
# <a name="invariant-mdl-checking-for-driver"></a>不変な MDL のドライバー用検査


不変な Mdl ドライバー用検査オプションは、ドライバーがドライバーごとの単位で不変の MDL バッファーを処理する方法を監視します。 不変の MDL バッファーに対する無効な改変が、このオプションによって検出されます。 このオプションを使うには、少なくとも 1 つのドライバーで I/O の検証を有効にする必要があります。

**注**  このオプションは Windows 8 以降で使用できます。

 

不変な mdl よりもより多くのフォームを実行する不変な Mdl のドライバー オプション、[不変な Mdl のスタック](invariant-mdl-checking-for-stack.md)オプション。 すべての呼び出しの間でバッファーの不変性が検証される不変な Mdl のドライバーがアクティブの場合、 [**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)と[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)ルーチン。

IRP で新しい不変の MDL バッファーを表示するたびに Driver Verifier は、バッファーの内容の署名を計算し、その内部データベースに格納します。 Driver Verifier は、先ほど説明したが不変の MDL バッファーを検出すると、そのバッファーの内容が変更されていないこと、現在不変の MDL バッファーの内容について計算されたシグネチャを持つ、データベース内の署名を比較することでは検証します。

このオプションはグローバルであり、選択的には適用できません一部のドライバーです。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。


ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用してに不変な Mdl のドライバーの機能の 1 つまたは複数のドライバーをアクティブにできます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。 不変な Mdl のドライバーのオプションがアクティブまたは非アクティブにコンピューターを再起動する必要があります。

アクティブ化する、[不変な Mdl のスタック](invariant-mdl-checking-for-stack.md)オプション、する必要がありますもアクティブ化する[I/O の検証](i-o-verification.md)です。

-   **コマンドラインで**

    、コマンドラインで不変な Mdl のドライバーによって表される**verifier/flags 0x00004000** (ビット 14)。 不変な Mdl のドライバーを有効にするには、0x00004010 のフラグの値を使用して、または 0x00004010 をフラグ値に追加します。 この値には、I/O の検証 (0x10) と不変な Mdl のドライバー (0x00004000) がアクティブにします。 以下に例を示します。

    ```
    verifier /flags 0x00004010 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

-   **ドライバー検証マネージャーを使用します。**
    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する** をクリックし、 **次へ。**
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック)[I/O の検証](i-o-verification.md)不変な Mdl のドライバーとします。
    5.  コンピューターを再起動します。

 

 





