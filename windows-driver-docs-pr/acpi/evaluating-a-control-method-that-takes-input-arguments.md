---
title: 入力引数を受け取る制御メソッドを評価する
description: 入力引数を受け取る制御メソッドを評価する
ms.assetid: 3a4be8a8-0906-4d38-bf6d-f245e6ae236a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cad6bc7b279af08b276a0e90c1fd8e2fecf0248
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328834"
---
# <a name="evaluating-a-control-method-that-takes-input-arguments"></a>入力引数を受け取る制御メソッドを評価する


入力引数を受け取るコントロール メソッドを同期的に評価するデバイスのドライバーの送信、 [ **IOCTL\_ACPI\_EVAL\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff536148)要求または、 [**IOCTL\_ACPI\_EVAL\_メソッド\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff536149)デバイスに要求します。 これら両方の要求を使用するための一般的な手順については、「 [ACPI コントロールのメソッドを同期的評価](evaluating-acpi-control-methods-synchronously.md)します。 これら 2 つの要求を使用しての特定の違いは次のとおりです。

-   コントロール メソッドは、デバイスの直接の子オブジェクトは、ドライバーは送信 IOCTL\_ACPI\_EVAL\_メソッド要求と次の入力構造体の 1 つを提供します。[**ACPI\_EVAL\_入力\_バッファー\_単純\_整数**](https://msdn.microsoft.com/library/windows/hardware/ff536119)、 [ **ACPI\_EVAL\_の入力\_バッファー\_単純\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff536121)、または[ **ACPI\_EVAL\_入力\_バッファー\_複合**](https://msdn.microsoft.com/library/windows/hardware/ff536116).

-   IOCTL 送信 control メソッドがのデバイスを ACPI 名前空間内の子オブジェクトは、デバイスの直接の子オブジェクトではない場合は、\_ACPI\_EVAL\_メソッド\_EX 要求との 1 つを提供します次の入力構造体。[**ACPI\_EVAL\_入力\_バッファー\_単純\_整数\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536120)、 [ **ACPI\_EVAL\_入力\_バッファー\_単純\_文字列\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536122)、または[ **ACPI\_EVAL\_入力\_バッファー\_複雑な\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536117)します。

例では、 *EvaluateABCDWithInputArgument*このトピックで提供されている関数は、ドライバーが IOCTL を使用する方法を示します\_ACPI\_EVAL\_という名前の制御メソッドを評価するメソッドの要求 'ABCD' を 1 つの整数の入力引数を受け取る。

入力引数が文字列または整数ではなく、カスタム データの配列である場合のコード例に必要な変更が、文字列入力構造体または整数入力構造体ではなく、複雑な入力構造を指定します。

さらに、'ABCD' コントロールのメソッドが直接の子オブジェクトでない場合、必要な変更のコード例を次に示します。

-   送信 IOCTL\_ACPI\_EVAL\_メソッド\_IOCTL ではなく要求 EX\_ACPI\_EVAL\_メソッド要求。

-   入力引数の型 (整数の単純な単純な文字列、または複雑な) に対応する拡張入力構造体の型を指定します。

*EvaluateABCDWithInputArgument* ACPI を最初に割り当てる\_EVAL\_入力\_バッファー\_単純\_整数構造*inputBuffer*し設定、 **MethodNameAsUlong**コントロール メソッドの名前にメンバーを設定、 **IntegerArgument**入力の整数値、およびセットへのメンバー、**署名**acpi メンバー\_EVAL\_入力\_バッファー\_単純\_整数\_署名します。

```cpp
    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.IntegerArgument  =  Argument1;
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_SIGNATURE;
```

*EvaluateABCDWithInputArgument*も割り当てます、 [ **ACPI\_EVAL\_出力\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff536123)構造*outputBuffer*のメンバーは設定しませんが、 *outputBuffer*します。

*EvaluateABCDWithInputArgument*という名前のドライバーによって提供される関数を呼び出して[SendDownStreamIrp](senddownstreamirp-function.md)次を実行します。

1.  呼び出し[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)要求を構築します。

2.  呼び出し[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)デバイス スタックの要求を送信します。

3.  下位レベルのドライバーが要求を完了したことをドライバーに通知する I/O マネージャーを待機します。

**SendDownStreamIrp** I/O マネージャーが下位レベルのドライバーが要求を完了したことを通知した後を返します。

含まれません*EvaluateABCDWithInputArgument*、ドライバーは、後に、次の追加操作を実行する必要がありますも**SendDownStreamIrp**を返します。

1.  状態を確認する**SendDownStreamIrp**を返します。 場合**SendDownStreamIrp**状態を返さない\_成功すると、ドライバーは、追加の処理を行わなくても返す必要があります。

2.  出力パラメーターの有効性を確認します。 *OutputBuffer*有効な出力のデータを含む**署名**ACPI に設定する必要があります\_EVAL\_出力\_バッファー\_と署名**カウント**0 より大きい値に設定する必要があります。

3.  ドライバーに渡された出力パラメーターを処理します。

4.  呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) IOCTL を完了する\_ACPI\_EVAL\_メソッド要求。

ACPI データ構造と次の例で使用される定数で定義されます*Acpiioct.h*します。

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

 

 




