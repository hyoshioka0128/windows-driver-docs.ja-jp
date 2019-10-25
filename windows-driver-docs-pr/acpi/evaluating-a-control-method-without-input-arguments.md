---
title: 入力引数なしの制御メソッドを評価する
description: 入力引数なしの制御メソッドを評価する
ms.assetid: dd989b4d-46db-4fe3-aa7b-8dbfe37057cb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02a796fc7cd2713b0fcd4ae8ad3af0ce948b3de8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826301"
---
# <a name="evaluating-a-control-method-without-input-arguments"></a>入力引数なしの制御メソッドを評価する


入力引数を受け取らない制御メソッドを同期的に評価するために、デバイスのドライバーは、 [**acpi\_acpi\_eval\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)要求または[**ioctl\_acpi\_eval\_メソッド\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)に ioctl を送信します。デバイスに要求します。 これらの要求の両方を使用するための一般的な手順については、「 [ACPI 制御メソッドを同期的に評価](evaluating-acpi-control-methods-synchronously.md)する」を参照してください。 この2つの要求を使用する場合の具体的な違いは次のとおりです。

-   コントロールメソッドがデバイスの直接の子オブジェクトである場合、ドライバーは IOCTL\_ACPI\_EVAL\_METHOD 要求を送信し、 [**acpi\_eval\_入力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)入力構造を提供します。

-   コントロールメソッドがデバイスの ACPI 名前空間の子オブジェクトであるのに、デバイスの直接の子オブジェクトではない場合、ドライバーは\_ACPI\_EVAL\_メソッド\_EX 要求を送信し、 [**acpi\_eval を提供します。\_入力\_BUFFER\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)構造体を入力します。

このトピックで提供する*Getabcdata*関数の例では、デバイスのドライバーが IOCTL\_ACPI\_EVAL\_method 要求を使用して、デバイスがサポートする ' ABCD ' という名前のコントロールメソッドを評価する方法を示しています。 ' ABCD ' コントロールメソッドは、ACPI 名前空間のデバイスの直下の子であり、入力引数を取らず、出力引数を返しません。

' ABCD ' コントロールメソッドが直接の子オブジェクトではない場合、このコード例に必要な変更は次のとおりです。

-   Ioctl\_ACPI\_EVAL\_METHOD 要求ではなく、\_ACPI\_EVAL\_メソッド\_EX 要求を送信します。

-   Acpi\_EVAL\_入力\_バッファー構造の代わりに、ACPI\_EVAL\_入力\_バッファー\_EX 構造体を指定します。

*Getabcdata*はまず、ACPI\_EVAL\_入力\_バッファー構造*inputBuffer*に割り当て、 **methodnameasulong**メンバーをコントロールメソッドの名前に設定し、**署名**メンバーを acpi に設定し @no__t\_入力\_バッファー\_署名を評価する (_s)。

```cpp
    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIGNATURE;
```

また、 *Getabcdata*によって、 [**ACPI\_EVAL\_出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)構造の*outputbuffer*も割り当てられますが、 *outputbuffer*のメンバーは設定されません。

次に、 *Getabcdata*は、次の処理を実行する[Senddownstreamirp](senddownstreamirp-function.md)という名前のドライバーで提供される関数を呼び出します。

1.  [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を呼び出して要求をビルドします。

2.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、デバイススタックで要求を送信します。

3.  I/o マネージャーが、下位レベルのドライバーが要求を完了したことを示すドライバーを通知するまで待機します。

**Senddownstreamirp**は、下位レベルのドライバーが要求を完了したことを i/o マネージャーが通知した後に戻ります。 前に説明したコード例では、次の処理を実行します。

1.  下位レベルのドライバーがステータス\_成功を返さなかった場合に、要求の状態を確認し、追加の処理を行わずに返します。

2.  出力引数が有効かどうかを確認します。 *Outputbuffer*に有効な出力データが含まれるようにするには、**署名**が ACPI\_EVAL に設定されている必要があります。\_出力\_バッファー\_署名、**カウント**は0より大きい値に設定する必要があります。

3.  ACPI ドライバーによってドライバーに戻された出力引数を処理します。

この手順はサンプルコードに含まれていませんが、ドライバーは、出力データを処理した後に[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、保留中の IOCTL\_ACPI\_EVAL\_メソッド要求または IOCTL\_ACPI を完了する必要があり\_コントロールメソッドを評価するためにドライバーによって送信された、EVAL\_メソッドの要求。

次の例で使用される ACPI データ構造および定数は、 *Acpiioct*で定義されています。

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

 

 




