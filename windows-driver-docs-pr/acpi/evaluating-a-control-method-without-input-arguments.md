---
title: 入力引数なしの制御メソッドを評価する
description: 入力引数なしの制御メソッドを評価する
ms.assetid: dd989b4d-46db-4fe3-aa7b-8dbfe37057cb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfac0f1415df62cc09e36f29454f18a055ba2aa0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355831"
---
# <a name="evaluating-a-control-method-without-input-arguments"></a>入力引数なしの制御メソッドを評価する


デバイスのドライバーの送信を入力引数を受け取らないコントロール メソッドを同期的に評価する、 [ **IOCTL\_ACPI\_EVAL\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)要求または[ **IOCTL\_ACPI\_EVAL\_メソッド\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)デバイスに要求します。 これら両方の要求を使用するための一般的な手順については、「 [ACPI コントロールのメソッドを同期的評価](evaluating-acpi-control-methods-synchronously.md)します。 これら 2 つの要求を使用しての特定の違いは次のとおりです。

-   Control メソッドは、デバイスの直接の子オブジェクトである、ドライバー送信 IOCTL\_ACPI\_EVAL\_メソッド要求と提供を[ **ACPI\_EVAL\_入力\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)構造体を入力します。

-   IOCTL 送信 control メソッドがのデバイスを ACPI 名前空間内の子オブジェクトは、デバイスの直接の子オブジェクトではない場合は、\_ACPI\_EVAL\_メソッド\_EX 要求し、の提供[**ACPI\_EVAL\_入力\_バッファー\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)構造体。

例では、 *GetAbcData*このトピックで提供されている関数は、デバイスのドライバーが IOCTL を使用する方法を示します\_ACPI\_EVAL\_メソッド要求の制御メソッドを評価する名前 'ABCD' をデバイスをサポートします。 'ABCD' control メソッドは、ACPI 名前空間内のデバイスの直接の子は、および引数を入力したりしない出力引数を返します。

'ABCD' コントロールのメソッドが直接の子オブジェクトでない場合、必要な変更を次のコード例を次に示します。

-   送信 IOCTL\_ACPI\_EVAL\_メソッド\_IOCTL ではなく要求 EX\_ACPI\_EVAL\_メソッド要求。

-   ACPI の指定\_EVAL\_入力\_バッファー\_ACPI ではなく構造 EX\_EVAL\_入力\_バッファーの構造体。

*GetAbcData* ACPI を最初に割り当てる\_EVAL\_入力\_バッファー構造*inputBuffer*設定と、 **MethodNameAsUlong**メンバーをコントロールのメソッドおよびセットの名前、**署名**acpi メンバー\_EVAL\_入力\_バッファー\_署名します。

```cpp
    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIGNATURE;
```

*GetAbcData*も割り当てます、 [ **ACPI\_EVAL\_出力\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)構造*outputBuffer*が、メンバーは設定しません*outputBuffer*します。

*GetAbcData*という名前のドライバーによって提供される関数を呼び出して[SendDownStreamIrp](senddownstreamirp-function.md)次を実行します。

1.  呼び出し[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)要求を構築します。

2.  呼び出し[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)デバイス スタックの要求を送信します。

3.  下位レベルのドライバーが要求を完了したことをドライバーに通知する I/O マネージャーを待機します。

**SendDownStreamIrp** I/O マネージャーが下位レベルのドライバーが要求を完了したことを通知した後を返します。 前述のコード例は、次を実行します。

1.  要求の状態を確認し、下位レベルのドライバーがステータスを返さなかった場合は、追加処理することがなくを返します\_成功します。

2.  出力引数の有効性を確認します。 *OutputBuffer*有効な出力のデータを含む**署名**ACPI に設定する必要があります\_EVAL\_出力\_バッファー\_と署名**カウント**0 より大きい値に設定する必要があります。

3.  出力の処理、ドライバーを ACPI ドライバーに渡される引数。

ドライバーも呼び出す必要がありますが、サンプル コードでは、この手順が含まれていない、 [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)保留中の IOCTL を完了する出力データを処理した後\_ACPI\_EVAL\_メソッド要求または IOCTL\_ACPI\_EVAL\_メソッド要求の制御メソッドを評価するドライバーが送信されることです。

ACPI データ構造と次の例で使用される定数で定義されます*Acpiioct.h*します。

```cpp
NTSTATUS
GetAbcdData(
    IN PDEVICE_OBJECT   Pdo,
    OUT PULONG          ReturnStatus
    )
/*++

Routine Description:
    Evaluates the ABCD method on the device in the ACPI namespace referenced by Pdo

Parameters
    Pdo             - PDO for the device
    ReturnStatus    - Pointer to where the status data is placed

Return Value:
    NT Status of the operation

--*/
{
    ACPI_EVAL_INPUT_BUFFER  inputBuffer;
    ACPI_EVAL_OUTPUT_BUFFER outputBuffer;
    NTSTATUS                status;
    PACPI_METHOD_ARGUMENT   argument;

    .
    .

    ASSERT( ReturnStatus != NULL );
    *ReturnStatus = 0x0;

    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIGNATURE;

    // Send the request along
    status = SendDownStreamIrp(
       Pdo,
       IOCTL_ACPI_EVAL_METHOD,
       &inputBuffer,
       sizeof(ACPI_EVAL_INPUT_BUFFER),
       &outputBuffer,
       sizeof(ACPI_EVAL_OUTPUT_BUFFER)
       );

    if (!NT_SUCCESS(status)) {
       return status;
    }

    // Verify the data
    if (outputBuffer != NULL) {
        if ( ( (PACPI_EVAL_OUTPUT_BUFFER) outputBuffer->Signature != 
            ACPI_EVAL_OUTPUT_BUFFER_SIGNATURE ||
            ( (PACPI_EVAL_OUTPUT_BUFFER) outputBuffer->Count == 0) {
            return STATUS_ACPI_INVALID_DATA;
        } 
}

    // Retrieve the output argument
    argument = outputBuffer.Argument;
 
// Process the output argument
 .
.
.
 
    return status;
}
```

 

 




