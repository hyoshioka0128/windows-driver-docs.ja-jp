---
title: 入力引数を受け取る制御メソッドを評価する
description: 入力引数を受け取る制御メソッドを評価する
ms.assetid: 3a4be8a8-0906-4d38-bf6d-f245e6ae236a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 365c9511abe7eea29de2857cc6c86cbb2812d011
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826182"
---
# <a name="evaluating-a-control-method-that-takes-input-arguments"></a>入力引数を受け取る制御メソッドを評価する


入力引数を受け取るコントロールメソッドを同期的に評価するために、デバイスのドライバーは、 [**acpi\_eval\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)の要求、または[**ioctl\_acpi\_eval\_method\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)要求に ioctl\_を送信します。デバイスに対して。 これらの要求の両方を使用するための一般的な手順については、「 [ACPI 制御メソッドを同期的に評価](evaluating-acpi-control-methods-synchronously.md)する」を参照してください。 この2つの要求を使用する場合の具体的な違いは次のとおりです。

-   コントロールメソッドがデバイスの直下の子オブジェクトである場合、ドライバーは IOCTL\_ACPI\_EVAL\_METHOD 要求を送信し、次のいずれかの入力構造を提供します: [**acpi\_EVAL\_入力\_バッファー\_SIMPLE\_INTEGER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)、 [**ACPI\_EVAL\_INPUT\_buffer\_単純な\_STRING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)、または[**ACPI\_EVAL\_INPUT\_buffer\_COMPLEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)です。

-   コントロールメソッドがデバイスの ACPI 名前空間の子オブジェクトであり、デバイスの直接の子オブジェクトではない場合、ドライバーは IOCTL\_ACPI\_EVAL\_メソッド\_EX 要求を送信し、次の入力のいずれかを提供します。構造体: [**acpi\_eval\_入力\_バッファー\_単純\_整数\_ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1_ex)、 [**ACPI\_EVAL\_入力\_バッファー\_単純\_文字列\_ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)、または[**ACPI\_EVAL\_入力\_BUFFER\_複雑な\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)です。

このトピックで提供する*EvaluateABCDWithInputArgument*関数の例では、ドライバーが IOCTL\_ACPI\_EVAL\_method 要求を使用して、単一の整数入力を受け取る ' ABCD ' という名前のコントロールメソッドを評価する方法を示しています。引数.

入力引数が整数ではなく、文字列またはカスタムデータの配列の場合、例のコードに必要な変更は、整数入力構造ではなく、文字列入力構造または複雑な入力構造を指定することです。

また、' ABCD ' コントロールメソッドが直接の子オブジェクトではない場合は、次のような変更が必要になります。

-   Ioctl\_ACPI\_EVAL\_METHOD 要求ではなく、\_ACPI\_EVAL\_メソッド\_EX 要求を送信します。

-   入力引数の型 (単純な整数、単純な文字列、または複合) に対応する拡張入力構造の種類を指定します。

*EvaluateABCDWithInputArgument*は、最初に ACPI\_EVAL\_入力\_バッファー\_単純\_整数構造体*inputBuffer*に割り当て、次に**methodnameasulong**メンバーをの名前に設定します。制御メソッドは、整数**引数**のメンバーを入力整数値に設定し、**署名**メンバーを ACPI\_EVAL\_入力\_バッファー\_単純\_整数\_署名に設定します。

```cpp
    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.IntegerArgument  =  Argument1;
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_SIGNATURE;
```

また、 *EvaluateABCDWithInputArgument*では、 [**ACPI\_EVAL\_出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)構造の*outputbuffer*も割り当てられますが、 *outputbuffer*のメンバーは設定されません。

*EvaluateABCDWithInputArgument*は、次の処理を実行する[Senddownstreamirp](senddownstreamirp-function.md)という名前のドライバー提供関数を呼び出します。

1.  [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を呼び出して要求をビルドします。

2.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、デバイススタックで要求を送信します。

3.  I/o マネージャーが、下位レベルのドライバーが要求を完了したことをドライバーに通知するまで待機します。

**Senddownstreamirp**は、下位レベルのドライバーが要求を完了したことを i/o マネージャーが通知した後に戻ります。

*EvaluateABCDWithInputArgument*には含まれていませんが、ドライバーは、 **Senddownstreamirp**からの戻り後に、次の追加操作も実行する必要があります。

1.  **Senddownstreamirp**が返す状態を確認します。 **Senddownstreamirp**が正常\_状態を返さない場合、ドライバーは追加の処理を行わずにを返します。

2.  出力パラメーターが有効かどうかを確認します。 *Outputbuffer*に有効な出力データが含まれるようにするには、**署名**が ACPI\_EVAL に設定されている必要があります。\_出力\_バッファー\_署名、**カウント**は0より大きい値に設定する必要があります。

3.  ドライバーに戻された出力パラメーターを処理します。

4.  [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、IOCTL\_ACPI\_EVAL\_METHOD 要求を完了します。

次の例で使用される ACPI データ構造および定数は、 *Acpiioct*で定義されています。

```cpp
NTSTATUS
EvaluateABCDWithInputArgument(
    IN PDEVICE_OBJECT   Pdo,
    IN ULONG            Argument1,
    OUT PULONG          ReturnStatus
    )
/*
Routine Description:
    Called to evaluate the example 'ABCD' method with a single integer input argument

Parameters:
    Pdo             - For the device.
    Argument1       - Input argument.
    ReturnStatus    - Pointer to where the status data is placed.

Return Value:
    NT Status of the operation
*/
{
 ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER  inputBuffer;
    ACPI_EVAL_OUTPUT_BUFFER                outputBuffer; 
    NTSTATUS                               status;
    PACPI_METHOD_ARGUMENT                  argument;

    .
    .
    // Omitted: bounds checking on Argument1 value.


    ASSERT( ReturnStatus != NULL );
    *ReturnStatus = 0x0;

    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.IntegerArgument  =  Argument1;
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_SIGNATURE;

    // Send the request along
    status = SendDownStreamIrp(
       Pdo,
       IOCTL_ACPI_EVAL_METHOD,
       &inputBuffer,
       sizeof(ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER),
       &outputBuffer,
       sizeof(ACPI_EVAL_OUTPUT_BUFFER)
       );

    return status;
}
```

 

 




