---
title: IOCTL_ACPI_ENUM_CHILDREN 要求を送信する
description: IOCTL_ACPI_ENUM_CHILDREN 要求を送信する
ms.assetid: cbad53dd-4320-4920-9d16-231d0aaae839
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 620b75352436551925c185984b6c5ed24fcf1ef0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330272"
---
# <a name="sending-an-ioctlacpienumchildren-request"></a>送信 IOCTL\_ACPI\_ENUM\_子要求


ドライバーは通常 2 つのシーケンスを使用して[ **IOCTL\_ACPI\_ENUM\_子**](https://msdn.microsoft.com/library/windows/hardware/ff536147)にデバイスの名前空間内の目的のオブジェクトを列挙する要求要求が送信されます。 ドライバーは、オブジェクトの名前とパスを格納するために必要なドライバーに割り当てられた出力バッファーのサイズを取得する最初の要求を送信します。 ドライバーはドライバーによって割り当てられる出力バッファー内のオブジェクトの名前とパスを返すには、2 番目の要求を送信します。

次のコード例は、2 つの同期 IOCTL のシーケンスを送信する方法を示しています。\_ACPI\_ENUM\_子要求を再帰的には、要求が送られる親デバイスのすべての子デバイスを列挙します。 コードでは、次の一連の最初の要求を処理するために操作を実行します。

1.  最初の要求の入力バッファーを設定します。 入力バッファーが、 [ **ACPI\_ENUM\_子\_入力\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff536110)構造体**署名**設定列挙体を\_子\_入力\_バッファー\_署名と**フラグ**列挙型に設定\_子\_マルチレベルします。

2.  最初の要求の出力バッファーを設定します。 出力バッファーに設定されて、 [ **ACPI\_ENUM\_子\_出力\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff536112)構造体。 この出力バッファーでは、1 つだけ含まれている[ **ACPI\_ENUM\_子**](https://msdn.microsoft.com/library/windows/hardware/ff536109)をデバイスの名前を返すのに十分な大きさではない構造体。

3.  呼び出し元が指定した呼び出し[SendDownStreamIrp 関数](senddownstreamirp-function.md)親デバイスに同期的に、最初の要求を送信します。

4.  ACPI のドライバーが状態に戻り値の状態を設定するかどうかをチェック\_バッファー\_オーバーフローが発生します。 別の状態が返された場合は、エラーが発生し、コードが終了したこれを示します。

5.  ACPI ドライバーことを確認します、**署名**acpi メンバー\_ENUM\_子\_出力\_バッファー\_署名とセット**コード**より大きいか等しい値に、 **sizeof**(ACPI\_ENUM\_子\_出力\_バッファー)。 True の値が両方とも場合**コード**要求された子オブジェクトの名前を格納するために必要な出力バッファーのバイト単位のサイズします。

コード例では、出力バッファーに必要なサイズを取得した後は、次の一連の要求された子オブジェクトの名前とパスを返しますの 2 番目の要求を処理するために操作を実行します。

1.  必要なサイズ (バイト) の出力バッファーを割り当てます。

2.  ドライバーによって提供される呼び出し**SendDownStreamIrp**親デバイスに同期的に 2 番目の要求を送信します。

3.  ACPI ドライバーことを確認します、**署名**acpi メンバー\_ENUM\_子\_出力\_バッファー\_署名設定**コード** 1 つ以上の (少なくとも 1 つのオブジェクトの名前とパスが返されたことを示す) に設定し、**情報**のメンバー、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)出力バッファーの割り当てのサイズにします。

4.  出力バッファー内の子オブジェクト名の配列を処理します。

```cpp
#define MY_TAG 'gTyM'   // Pool tag for memory allocation

 ACPI_ENUM_CHILDREN_INPUT_BUFFER  inputBuffer;
    ACPI_ENUM_CHILDREN_OUTPUT_BUFFER outputSizeBuffer = { 0 };
    ACPI_ENUM_CHILDREN_OUTPUT_BUFFER outputBuffer = { 0 };
    ULONG                            bufferSize;
 PACPI_ENUM_CHILD                 childObject = NULL;
 ULONG                            index;

    NTSTATUS                         status;

    ASSERT( ReturnStatus != NULL );
    *ReturnStatus = 0x0;

    // Fill in the input data
    inputBuffer.Signature = ACPI_ENUM_CHILDREN_INPUT_BUFFER_SIGNATURE;
    inputBuffer.Flags = ENUM_CHILDREN_MULTILEVEL;

    // Send the request along
    status = SendDownStreamIrp(
       Pdo,
 IOCTL_ACPI_ENUM_CHILDREN,
       &inputBuffer,
       sizeof(inputBuffer),
       &outputSizeBuffer,
       sizeof(outputSizeBuffer)
       );

 if (Status != STATUS_BUFFER_OVERFLOW) {
        // There should be at least one child device (that is the device itself)
        // Return error return status
    }

    // Verify the data
    // NOTE: The NumberOfChildren returned by ACPI actually contains the required size
 // when the status returned is STATUS_BUFFER_OVERFLOW 

    if ((outputSizeBuffer.Signature != ACPI_ENUM_CHILDREN_OUTPUT_BUFFER_SIGNATURE) ||
       (outputSizeBuffer.NumberOfChildren < sizeof(ACPI_ENUM_CHILDREN_OUTPUT_BUFFER)))
    {
        return STATUS_ACPI_INVALID_DATA;
    }

    //
    // Allocate a buffer to hold all the child devices
    //
    bufferSize = outputSizeBuffer.NumberOfChildren;
    outputBuffer = (PACPI_ENUM_CHILDREN_OUTPUT_BUFFER)
 ExAllocatePoolWithTag(PagedPool, bufferSize, MY_TAG);

    if (outputBuffer == NULL){
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    RtlZeroMemory(outputBuffer, bufferSize);

    // Allocate a new IRP with the new output buffer
    // Send another request together with the new output buffer
    status = SendDownStreamIrp(
       Pdo,
 IOCTL_ACPI_ENUM_CHILDREN,
       &inputBuffer,
       sizeof(inputBuffer),
       &outputBuffer,
       bufferSize
       );

    // Verify the data
    if ((outputBuffer->Signature != ACPI_ENUM_CHILDREN_OUTPUT_BUFFER_SIGNATURE) ||
        (outputBuffer->NumberOfChildren == 0) ||
        (IoStatusBlock.Information != bufferSize)) {
        return STATUS_ACPI_INVALID_DATA;
    }

    // Skip the first child device because ACPI returns the device itself 
 // as the first child device
    childObject = &(outputBuffer->Children[0]);

    for (index = 1; index < outputBuffer->NumberOfChildren; ++index) {

        // Proceed to the next ACPI child device. 
        childObject = ACPI_ENUM_CHILD_NEXT(childObject);

        //  Process each child device.
 
 
 
    }
```

 

 




