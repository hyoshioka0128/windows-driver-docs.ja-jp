---
title: 操作後コールバック ルーチン内でユーザー バッファーへアクセスする
description: 操作後コールバック ルーチン内でユーザー バッファーへアクセスする
ms.assetid: a980f302-6fde-461e-8b11-313530aff350
keywords:
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 000401f32303a44a5ce129fdb526fadcc34adba3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841505"
---
# <a name="accessing-user-buffers-in-a-postoperation-callback-routine"></a>操作後コールバック ルーチン内でユーザー バッファーへアクセスする


## <span id="ddk_accessing_user_buffers_in_a_postoperation_callback_routine_if"></span><span id="DDK_ACCESSING_USER_BUFFERS_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


ミニフィルタードライバー [**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)は、次のように、IRP ベースの i/o 操作でバッファーを処理する必要があります。

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

-   バッファーに対して MDL が存在する場合は、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出してバッファーのシステムアドレスを取得し、このアドレスを使用してバッファーにアクセスします。 (**MmGetSystemAddressForMdlSafe**は IRQL &lt;= DISPATCH\_LEVEL で呼び出すことができます)。

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

-   バッファー用の MDL がない場合は、 [**FLT\_is\_システム\_buffer**](https://docs.microsoft.com/previous-versions/ff544663(v=vs.85))マクロを使用して、システムバッファーフラグが操作に対して設定されているかどうかを確認します。

    -   FLT\_が\_システム\_バッファーマクロによって**TRUE**が返された場合、操作はバッファー i/o を使用し、IRQL = ディスパッチ\_レベルでバッファーに安全にアクセスできます。

    -   FLT\_が\_システム\_バッファーマクロによって**FALSE**が返された場合、IRQL = ディスパッチ\_レベルでバッファーに安全にアクセスすることはできません。 Postoperation コールバックルーチンをディスパッチ\_レベルで呼び出すことができる場合、この呼び出しは、IRQL &lt;= APC\_レベルで処理できるようになるまで、操作を保留するために[**Fltdo補完 Processingwhensafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)を呼び出す必要があります。 **FltdoFltLockUserBuffer Processingwhensafe**の*safepostcallback*パラメーターが指すコールバックルーチンは、最初にバッファーをロックしてから[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出すために、まず** should first call [**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)を呼び出します。バッファーのシステムアドレスを取得します。

Postoperation コールバックルーチンは、次のように、高速の i/o 操作でバッファーを処理する必要があります。

-   バッファーアドレスを使用してバッファーにアクセスします (高速 i/o 操作には MDL を設定できないため)。

-   ユーザー領域のバッファーアドレスが有効であることを確認するには、ミニフィルタードライバーで[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)や[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)などのルーチンを使用し**て、try**/**以外**のブロックですべてのバッファー参照を囲む必要があります。

-   高速 i/o 操作の postoperation コールバックルーチンは、正しいスレッドコンテキストで呼び出されることが保証されています。

-   高速 i/o 操作の postoperation コールバックルーチンは、IRQL &lt;= APC\_レベルで呼び出されることが保証されているので、 [**FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)などのルーチンを安全に呼び出すことができます。

次のコード例では、ディレクトリ制御操作のシステムバッファーまたは高速 i/o フラグをチェックし、必要に応じて完了処理を延期します。

```CSS
if (*DirectoryControlMdl == NULL)
{
    if (FLT_IS_SYSTEM_BUFFER(CallbackData) || FLT_IS_FASTIO_OPERATION(CallbackData))
    {
        dirBuffer = CallbackData->Iopb->Parameters.DirectoryControl.QueryDirectory.DirectoryBuffer;
    }
    else
    {
        // Defer processing until safe.
        if (!FltDoCompletionProcessingWhenSafe(CallbackData, FltObjects, CompletionContext, Flags, ProcessPostDirCtrlWhenSafe, &retValue))
        {
            CallbackData->IoStatus.Status = STATUS_UNSUCCESSFUL;
            CallbackData->IoStatus.Information = 0;
        }
    }
}
```

高速 i/o または IRP ベースのいずれかの操作を実行するには、すべてのバッファー参照を**try**/**以外**のブロックで囲む必要があります。 バッファリングされた i/o を使用する IRP ベースの操作では、これらの参照を囲む必要はありませんが、 **try**/**except**ブロックは安全な予防措置です。

 

 




