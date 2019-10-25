---
title: ダイレクト i/o のエラー
description: ダイレクト i/o のエラー
ms.assetid: 9efc2875-3402-4e2e-871b-3cc1d8f45360
keywords:
- 信頼性 WDK カーネル、ダイレクト i/o
- ダイレクト i/o WDK カーネル
- I/o WDK カーネル、ダイレクト i/o
- 長さ0のバッファー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 038f851bec4bebd301cda6aee62b93ce61749679
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838708"
---
# <a name="errors-in-direct-io"></a>ダイレクト i/o のエラー





最も一般的なダイレクト i/o の問題は、長さ0のバッファーを正しく処理できないことを示しています。 I/o マネージャーは長さ0の転送に MDLs を作成しないため、長さ0のバッファーでは、 **Irp-&gt;MdlAddress**に**NULL**値が返されます。

アドレス空間をマップするには、ドライバーで[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を使用する必要があります。これは、ドライバーが null の **mdladdress**を渡す場合と同様に、マッピングが失敗した場合に**null**を返します。 ドライバーは、返されたアドレスを使用しようとする前に、必ず**NULL**の戻り値を確認する必要があります。

ダイレクト i/o では、2つの異なる仮想アドレスの物理アドレスが同じになるように、ユーザーのアドレス空間をシステムアドレスバッファーに二重にマップします。 ダブルマッピングには次のような影響があります。これにより、ドライバーで問題が発生する可能性があります。

-   ユーザーのアドレスの仮想ページへのオフセットは、システムページへのオフセットになります。

    これらのシステムバッファーの末尾を越えたアクセスは、マッピングのページ粒度によっては、長期間にわたって気付かれない場合があります。 呼び出し元のバッファーがページの末尾付近に割り当てられていない限り、バッファーの末尾を越えて書き込まれたデータはバッファーに表示されますが、呼び出し元はエラーが発生したことを認識しません。 バッファーの末尾がページの末尾と一致する場合、末尾を越えるシステム仮想アドレスは、何かを指しているか、無効である可能性があります。 このような問題は、検索が非常に困難な場合があります。

-   呼び出しプロセスに、ユーザーのメモリマッピングを変更する別のスレッドがある場合、ユーザーのメモリマッピングが変更されると、システムバッファーの内容が変更されます。

    このような状況では、システムバッファーを使用してスクラッチデータを格納すると、問題が発生する可能性があります。 同じメモリ位置から2つのフェッチを行うと、異なる値が生成される可能性があります。

    次のコードスニペットは、ダイレクト i/o 要求で文字列を受け取り、その文字列を大文字に変換しようとします。

    ```cpp
    PWCHAR  PortName = NULL;

    PortName = (PWCHAR)MmGetSystemAddressForMdlSafe(irp->MdlAddress, NormalPagePriority);

    //
    // Null-terminate the PortName so that RtlInitUnicodeString will not
    // be invalid.
    //
    PortName[Size / sizeof(WCHAR) - 1] = UNICODE_NULL;

    RtlInitUnicodeString(&AdapterName, PortName);
    ```

    バッファーが正しく書式設定されていない可能性があるため、コードは、最後のバッファー文字として Unicode **NULL**を強制的に適用しようとします。 ただし、基になる物理メモリがユーザーとカーネルモードの両方のアドレスに二重にマップされている場合、この書き込み操作が完了するとすぐに、プロセス内の別のスレッドがバッファーを上書きできます。

    逆に、 **NULL**が存在しない場合、 **RtlInitUnicodeString**の呼び出しはバッファーの範囲を超える可能性があり、システムマッピングの外部にある場合はバグチェックが発生する可能性があります。

ドライバーが独自の MDL を作成してマップする場合は、プローブされたメソッドを使用してのみ、MDL にアクセスできるようにする必要があります。 つまり、ドライバーが[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)を呼び出すと、アクセスメソッド (**IoReadAccess**、 **iowriteaccess**、または**iowriteaccess**) が指定されます。 ドライバーで**IoReadAccess**が指定されている場合、後で[**MmGetSystemAddressForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetsystemaddressformdl)または[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)で使用可能なシステムバッファーへの書き込みを試みることはできません。

 

 




