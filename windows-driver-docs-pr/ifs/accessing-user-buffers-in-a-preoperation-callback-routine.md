---
title: Preoperation コールバック ルーチンでユーザー バッファーへのアクセス
description: Preoperation コールバック ルーチンでユーザー バッファーへのアクセス
ms.assetid: 16e6a9e0-3a92-471f-98e6-9a4e8eb7d4a6
keywords:
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7c35fcc95ff83f74a42d07ff95c6b8860d57d8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531846"
---
# <a name="accessing-user-buffers-in-a-preoperation-callback-routine"></a>Preoperation コールバック ルーチンでユーザー バッファーへのアクセス


## <span id="ddk_accessing_user_buffers_in_a_preoperation_callback_routine_if"></span><span id="DDK_ACCESSING_USER_BUFFERS_IN_A_PREOPERATION_CALLBACK_ROUTINE_IF"></span>


ミニフィルター ドライバーの[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)扱う必要があります、バッファー、IRP ベースの I/O 操作で次のようにします。

-   バッファーの MDL が存在するかどうかを確認します。 見つかる MDL ポインター、 *MdlAddress*または*OutputMdlAddress*パラメーター、 [ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673)の操作。 ミニフィルター ドライバーが呼び出せる[ **FltDecodeParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff541956) MDL ポインターを照会します。

    有効な MDL を取得するための 1 つのメソッドが IRP 検索\_MN\_MDL フラグ、 **MinorFunction** I/O パラメーター ブロックのメンバー [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)コールバックのデータ。 次の例は、IRP をチェックする方法を示しています。\_MN\_MDL フラグ。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    if (FlagOn(CallbackData->Iopb->MinorFunction, IRP_MN_MDL))
    {
        ReadMdl = &CallbackData->Iopb->Parameters.Read.MdlAddress;
    }
    ```

    ただし、IRP\_MN\_MDL フラグ操作と書き込み操作の読み取りのみ設定できます。 使用することをお勧め[ **FltDecodeParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff541956)ルーチンは、すべての操作に対して有効な MDL のチェックがあるため、MDL を取得します。 次の例では、有効な場合、MDL パラメーターのみが返されます。

    ```ManagedCPlusPlus
    NTSTATUS status;
    PMDL *ReadMdl = NULL;
    PVOID ReadAddress = NULL;

    status = FltDecodeParameters(CallbackData, &ReadMdl, NULL, NULL, NULL);
    ```

-   バッファーの MDL が存在する場合に呼び出す[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)バッファーのシステム アドレスを取得し、このアドレスを使用して、バッファーへのアクセスにします。

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

-   バッファーの MDL がない場合は、バッファーのアドレスを使用して、バッファーへのアクセスします。 ユーザー領域バッファーのアドレスが有効では、ミニフィルター ドライバーなどでルーチンを使用する必要があります[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)または[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)、内のすべてのバッファー参照を囲む**お試しください**/**を除く**ブロックします。

Preoperation コールバック ルーチンを高速な I/O 操作では、バッファーを次のように扱う必要があります。

-   (高速な I/O 操作を MDL ことがあるできない) ため、バッファーにアクセスするのにには、バッファーのアドレスを使用します。

-   ユーザー領域バッファーのアドレスが有効では、ミニフィルター ドライバーなどでルーチンを使用する必要があります**ProbeForRead**または**ProbeForWrite**、内のすべてのバッファー参照を囲む**をお試しください**/**を除く**ブロックします。

できる高速な I/O 操作の IRP に基づくすべてのバッファー参照で囲むか、または**お試しください**/**を除く**ブロックします。 バッファー内の I/O を使用する IRP ベース操作でこれらの参照を囲む必要はありませんが、**お試しください**/**を除く**ブロックは、安全な予防措置です。

 

 




