---
title: 不変な MDL のドライバー用検査
description: インバリアントな MDL チェックドライバーオプションは、ドライバーがドライバー単位で不変の MDL バッファーを処理する方法を監視します。
ms.assetid: 2FA69B7C-3EF4-4660-84D4-5108C97E395F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00921ea58e2d117703df64255519ef0f525016db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839553"
---
# <a name="invariant-mdl-checking-for-driver"></a>不変な MDL のドライバー用検査


インバリアントな MDL チェックドライバーオプションは、ドライバーがドライバー単位で不変の MDL バッファーを処理する方法を監視します。 不変の MDL バッファーに対する無効な改変が、このオプションによって検出されます。 このオプションを使うには、少なくとも 1 つのドライバーで I/O の検証を有効にする必要があります。

**注**  このオプションは、Windows 8 以降で使用できます。

 

インバリアントな MDL チェックドライバーオプションでは、インバリアントな mdl チェック[スタック](invariant-mdl-checking-for-stack.md)オプションよりもより多くの不変の mdl チェックが実行されます。 ドライバーの不変の MDL チェックがアクティブになっている場合は、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)ルーチンと[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)ルーチンを呼び出すたびに、buffer 不変性が検証されます。

新しい不変の MDL バッファーが IRP で認識されるたびに、ドライバー検証ツールはバッファーの内容の署名を計算し、内部データベースに格納します。 Driver Verifier は、前に見た不変の MDL バッファーを検出すると、データベース内の署名を現在のインバリアントな MDL バッファーの内容に対して計算された署名と比較することによって、バッファーの内容が変更されていないことを検証します。

このオプションはグローバルであり、一部のドライバーを選択的に適用することはできません。

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする


ドライバー検証ツールマネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーのドライバー機能に対する不変の MDL チェックをアクティブ化できます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。 コンピューターを再起動して、インバリアントな MDL チェックドライバーオプションをアクティブ化または非アクティブ化する必要があります。

[インバリアントな MDL チェックスタック](invariant-mdl-checking-for-stack.md)オプションをアクティブにするには、 [i/o 検証](i-o-verification.md)もアクティブ化する必要があります。

-   **コマンドラインで**

    コマンドラインでは、ドライバーの不変な MDL チェックは、 **verifier/flags 0x00004000** (ビット 14) によって表されます。 ドライバーの不変の MDL チェックをアクティブにするには、フラグ値0x00004010 を使用するか、フラグ値に0x00004010 を追加します。 この値は、i/o 検証 (0x10) とドライバーの不変の MDL チェック (0x00004000) をアクティブにします。 次に、例を示します。

    ```
    verifier /flags 0x00004010 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

-   **ドライバー検証マネージャーの使用**
    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  ドライバーの[I/o 検証](i-o-verification.md)と不変の MDL チェックを選択 (チェック) します。
    5.  コンピューターを再起動します。

 

 





