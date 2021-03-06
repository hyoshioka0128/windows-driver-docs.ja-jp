---
title: 操作後コールバック ルーチン内でユーザー バッファーへアクセスする
description: 操作後コールバック ルーチン内でユーザー バッファーへアクセスする
ms.assetid: a980f302-6fde-461e-8b11-313530aff350
keywords:
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73faf5545cbd8db2a4240324e972a0d00eff3213
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381738"
---
# <a name="accessing-user-buffers-in-a-postoperation-callback-routine"></a>操作後コールバック ルーチン内でユーザー バッファーへアクセスする


## <span id="ddk_accessing_user_buffers_in_a_postoperation_callback_routine_if"></span><span id="DDK_ACCESSING_USER_BUFFERS_IN_A_POSTOPERATION_CALLBACK_ROUTINE_IF"></span>


ミニフィルター ドライバー [ **postoperation コールバック ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)扱う必要があります、バッファー、IRP ベースの I/O 操作で次のようにします。

-   バッファーの MDL が存在するかどうかを確認します。 見つかる MDL ポインター、 *MdlAddress*または*OutputMdlAddress*パラメーター、 [ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)の操作。 ミニフィルター ドライバーが呼び出せる[ **FltDecodeParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdecodeparameters) MDL ポインターを照会します。

    有効な MDL を取得するための 1 つのメソッドが IRP 検索\_MN\_MDL フラグ、 **MinorFunction** I/O パラメーター ブロックのメンバー [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)コールバックのデータ。 次の例は、IRP をチェックする方法を示しています。\_MN\_MDL フラグ。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    if (FlagOn(CallbackData->Iopb->MinorFunction, IRP_MN_MDL))
    {
        ReadMdl = &CallbackData->Iopb->Parameters.Read.MdlAddress;
    }
    ```

    ただし、IRP\_MN\_MDL フラグ操作と書き込み操作の読み取りのみ設定できます。 使用することをお勧め[ **FltDecodeParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdecodeparameters)ルーチンは、すべての操作に対して有効な MDL のチェックがあるため、MDL を取得します。 次の例では、有効な場合、MDL パラメーターのみが返されます。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    status = FltDecodeParameters(CallbackData, &ReadMdl, NULL, NULL, NULL);
    ```

-   バッファーの MDL が存在する場合に呼び出す[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)バッファーのシステム アドレスを取得し、このアドレスを使用して、バッファーへのアクセスにします。 (**MmGetSystemAddressForMdlSafe** IRQL で呼び出すことができます&lt;= ディスパッチ\_レベルです)。

    前の例から続行すると、次のコードは、システムのアドレスを取得します。

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

-   バッファーの MDL がない場合は、操作を使用してシステム バッファー フラグが設定するかどうかを確認、 [ **FLT\_IS\_システム\_バッファー** ](https://docs.microsoft.com/previous-versions/ff544663(v=vs.85))マクロ。

    -   場合、FLT\_IS\_システム\_バッファー マクロを返します**TRUE**操作がバッファー内の I/O を使用し、バッファーは、IRQL で安全にアクセスできる、ディスパッチ =\_レベル。

    -   場合、FLT\_IS\_システム\_バッファー マクロを返します**FALSE**、バッファーは、IRQL で安全にアクセスできない = ディスパッチ\_レベル。 ディスパッチで postoperation コールバック ルーチンを呼び出すことができるかどうか\_呼び出す必要がありますレベル、 [ **FltDoCompletionProcessingWhenSafe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe) IRQLで処理することができるまで、操作を保留する&lt;APC を =\_レベル。 コールバック ルーチンを指していますが、 *SafePostCallback*パラメーターの**FltDoCompletionProcessingWhenSafe**呼び出す必要がありますまず[ **FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)バッファーをロックし、呼び出す[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)バッファーのシステム アドレスを取得します。

Postoperation コールバック ルーチンを高速な I/O 操作では、バッファーを次のように扱う必要があります。

-   (高速な I/O 操作を MDL ことがあるできない) ため、バッファーにアクセスするのにには、バッファーのアドレスを使用します。

-   ユーザー領域バッファーのアドレスが有効では、ミニフィルター ドライバーなどでルーチンを使用する必要があります[ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)または[ **ProbeForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)、内のすべてのバッファー参照を囲む**お試しください**/**を除く**ブロックします。

-   高速な I/O 操作の postoperation コールバック ルーチンを適切なスレッド コンテキストで呼び出されることが保証されます。

-   高速な I/O 操作の postoperation コールバック ルーチンは IRQL で呼び出される保証&lt;APC を =\_レベルなどのルーチンを呼び出すことが安全に[ **FltLockUserBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)します。

システムのバッファーの次の例のコード フラグメントをチェックまたは高速な I/O フラグのディレクトリの管理操作と完了に必要な場合の処理を延期します。

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

できる、高速な I/O 操作の IRP に基づくすべてのバッファー参照で囲むか、または**お試しください**/**を除く**ブロックします。 バッファー内の I/O を使用する IRP ベース操作でこれらの参照を囲む必要はありませんが、**お試しください**/**を除く**ブロックは、安全な予防措置です。

 

 




