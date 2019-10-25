---
title: 操作前コールバック ルーチン内でユーザー バッファーへアクセスする
description: 操作前コールバック ルーチン内でユーザー バッファーへアクセスする
ms.assetid: 16e6a9e0-3a92-471f-98e6-9a4e8eb7d4a6
keywords:
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター、バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fc8ab417505dac51cdf72f2df33ce7cabc0d384
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841502"
---
# <a name="accessing-user-buffers-in-a-preoperation-callback-routine"></a>操作前コールバック ルーチン内でユーザー バッファーへアクセスする


## <span id="ddk_accessing_user_buffers_in_a_preoperation_callback_routine_if"></span><span id="DDK_ACCESSING_USER_BUFFERS_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


ミニフィルタードライバーの[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)は、次のように、IRP ベースの i/o 操作でバッファーを処理する必要があります。

-   バッファーに対して MDL が存在するかどうかを確認します。 MDL ポインターは、操作の[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)の*mdladdress*パラメーターまたは*outputmdladdress*パラメーターにあります。 ミニフィルタードライバーは、 [**FltDecodeParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters)を呼び出して、MDL ポインターを照会できます。

    有効な MDL を取得するための1つの方法として、コールバックデータ内の i/o パラメーターブロック[**FLT\_IO\_parameter\_block**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)の**minorfunction**メンバーで、IRP\_\_MDL フラグを探します。 次の例では、IRP\_\_MDL フラグをチェックする方法を示します。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    if (FlagOn(CallbackData->Iopb->MinorFunction, IRP_MN_MDL))
    {
        ReadMdl = &CallbackData->Iopb->Parameters.Read.MdlAddress;
    }
    ```

    ただし、IRP\_\_MDL フラグは、読み取りおよび書き込み操作に対してのみ設定できます。 [**FltDecodeParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdecodeparameters)を使用して mdl を取得することをお勧めします。これは、ルーチンが任意の操作に対して有効な mdl をチェックするためです。 次の例では、有効な場合にのみ、MDL パラメーターが返されます。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    status = FltDecodeParameters(CallbackData, &ReadMdl, NULL, NULL, NULL);
    ```

-   バッファーに対して MDL が存在する場合は、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出してバッファーのシステムアドレスを取得し、このアドレスを使用してバッファーにアクセスします。

    前の例から続けると、次のコードはシステムアドレスを取得します。

    ```ManagedCPlusPlus
    if (*ReadMdl != NULL)
    {
        ReadAddress = MmGetSystemAddressForMdlSafe(*ReadMdl, NormalPagePriority);
        if (ReadAddress == NULL)
        {
            CallbackData->IoStatus.Status = STATUS_INSUFFICIENT_RESOURCES;
            CallbackData->IoStatus.Information = 0;
        }
    }
    ```

-   バッファーに対して MDL が存在しない場合は、バッファーアドレスを使用してバッファーにアクセスします。 ユーザー領域のバッファーアドレスが有効であることを確認するには、ミニフィルタードライバーで[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)や[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)などのルーチンを使用し**て、try**/**以外**のブロックですべてのバッファー参照を囲む必要があります。

Preoperation コールバックルーチンは、次のように、高速の i/o 操作でバッファーを処理する必要があります。

-   バッファーアドレスを使用してバッファーにアクセスします (高速 i/o 操作には MDL を設定できないため)。

-   ユーザー領域のバッファーアドレスが有効であることを確認するには、ミニフィルタードライバーで**ProbeForRead**や**ProbeForWrite**などのルーチンを使用し**て、try**/**以外**のブロックですべてのバッファー参照を囲む必要があります。

高速 i/o または IRP ベースの可能性がある操作では、すべてのバッファー参照を**try**/**以外**のブロックで囲む必要があります。 バッファリングされた i/o を使用する IRP ベースの操作では、これらの参照を囲む必要はありませんが、 **try**/**except**ブロックは安全な予防措置です。

 

 




