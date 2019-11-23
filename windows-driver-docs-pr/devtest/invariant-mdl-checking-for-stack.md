---
title: 不変な MDL のスタック用検査
description: インバリアントな MDL チェックスタックオプションは、ドライバーがドライバースタック全体で不変の MDL バッファーを処理する方法を監視します。
ms.assetid: AB27803A-6B3A-40FA-B962-79B0DA2F5FA9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 126ea493f4fb2f81179d5d983c511b47e4bd7963
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840261"
---
# <a name="invariant-mdl-checking-for-stack"></a>不変な MDL のスタック用検査


インバリアントな MDL チェックスタックオプションは、ドライバーがドライバースタック全体で不変の MDL バッファーを処理する方法を監視します。 不変の MDL バッファーに対する無効な改変が、ドライバーの検証ツールによって検出されます。 このオプションを使うには、少なくとも 1 つのドライバーで I/O の検証を有効にする必要があります。

**注**  このオプションは、Windows 8 以降で使用できます。

 

インバリアントな MDL チェックスタックオプションを使用すると、ドライバーは、要求がドライバースタックから出た時点でのみ、不変の MDL バッファーの規則に従っていることが保証されます。

不変の MDL を持つ IRP が[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)ルーチンで初めて検出されたときに、一意の署名がインバリアントな mdl バッファーの内容から計算され、内部データベースに格納されます。 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)ルーチンでの irp の完了時に、irp に署名を記録した不変の MDL がまだ含まれている場合、ドライバーの検証ツールはバッファーが変更されていないことを検証します。

書き込み要求の不変バッファーは、IRP の有効期間全体にわたって変更することはできません。 読み取り要求の場合、そのディスパッチパスで不変バッファーを変更することはできません。そのため、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を最後に呼び出したときにバッファー署名の比較が行われます。

インバリアントな MDL チェックスタックオプションは、スタック内の個々のドライバーを通過するときに、バッファーに何が行われるかに関係なく、ドライバースタック全体での MDL バッファーのずれを検証します。 このオプションはグローバルであり、ドライバーごとに選択的に適用することはできません。 インバリアントな MDL チェックスタックオプションでは、バッファーに違反したドライバーを特定できない限り、違反をキャッチすることはできません。 問題のあるドライバーを特定するには、[[不変の MDL のドライバーのチェック](invariant-mdl-checking-for-driver.md)] オプションを使用します。これにより、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)および[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) DDIs を呼び出すたびに、バッファーの内容の分散が検証されます。

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする


ドライバー検証マネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーについて、不変の MDL チェックスタック機能をアクティブにすることができます。 コンピューターを再起動して、インバリアントな MDL チェックスタックオプションをアクティブ化または非アクティブ化する必要があります。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

インバリアントな MDL チェックスタックオプションをアクティブにするには、 [I/o 検証](i-o-verification.md)もアクティブ化する必要があります。

-   **コマンドラインで**

    コマンドラインでは、スタックの不変な MDL チェックは**0x00002000** (ビット 13) によって表されます。 スタックに対する不変の MDL チェックをアクティブにするには、フラグ値0x00002010 を使用するか、フラグ値に0x00002010 を追加します。 この値は、i/o 検証 (0x10) とスタックの不変の MDL チェック (0x00002000) をアクティブにします。 次に、例を示します。

    ```
    verifier /flags 0x00002010 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

-   **ドライバー検証マネージャーの使用**
    1.  ドライバー検証マネージャーを起動します。 コマンドプロンプトウィンドウで「 **Verifier** 」と入力します。
    2.  [**カスタム設定の作成] (コード開発者向け)** を選択し、 **[次へ]** をクリックします。
    3.  [**完全な一覧から個々の設定を選択]** を選択します。
    4.  [I/o 検証](i-o-verification.md)を選択し、スタックの不変な MDL チェックをオンにします。
    5.  コンピューターを再起動します。

 

 





