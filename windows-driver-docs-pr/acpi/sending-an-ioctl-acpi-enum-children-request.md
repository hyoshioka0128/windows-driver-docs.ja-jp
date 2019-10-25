---
title: IOCTL_ACPI_ENUM_CHILDREN 要求を送信する
description: IOCTL_ACPI_ENUM_CHILDREN 要求を送信する
ms.assetid: cbad53dd-4320-4920-9d16-231d0aaae839
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4997f58455d32941c95ef6e6ea4003f3e5e32ef7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831465"
---
# <a name="sending-an-ioctl_acpi_enum_children-request"></a>子\_の子要求\_IOCTL\_の送信


通常、ドライバーは、2つの[**IOCTL\_\_列挙型\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)要求を使用して、要求が送信されるデバイスの名前空間で対象となるオブジェクトを列挙します。 ドライバーは、オブジェクトのパスと名前を格納するために必要なドライバー割り当て出力バッファーのサイズを取得するために、最初の要求を送信します。 ドライバーは、ドライバーによって割り当てられた出力バッファー内のオブジェクトのパスと名前を返す2番目の要求を送信します。

次のコード例では、2つの同期 IOCTL\_ACPI\_ENUM\_CHILDREN 要求を送信して、要求が送信される親デバイスのすべての子デバイスを再帰的に列挙する方法を示します。 このコードは、最初の要求を処理するために、次の一連の操作を実行します。

1.  最初の要求の入力バッファーを設定します。 入力バッファーは、 [ **\_子\_入力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_input_buffer)構造に\_設定されている、子の\_列挙型の列挙型に設定されています **。また、** 署名が列挙型に設定**されて**います。\_の子\_複数レベルです。

2.  最初の要求の出力バッファーを設定します。 出力バッファーは、 [**ACPI\_列挙型\_子\_出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer)構造に設定されます。 この出力バッファーには、デバイスの名前を返すには十分な大きさではない、1つの[**ACPI\_列挙型\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child)構造体だけが含まれています。

3.  呼び出し元が提供した[Senddownstreamirp 関数](senddownstreamirp-function.md)を呼び出して、最初の要求を親デバイスに同期的に送信します。

4.  ACPI ドライバーがステータス\_バッファー\_オーバーフローに設定したかどうかを確認します。 別の状態が返された場合は、エラーが発生したことを示し、コードは終了します。

5.  ACPI ドライバーによって**署名**メンバーが acpi\_列挙型に設定されていることを確認します。\_\_子には、出力\_バッファー\_署名を設定し、 **numberofchildren**の値を**sizeof**(acpi @no__t_ の値以上に設定します。8_ ENUM\_子\_出力\_BUFFER) です。 両方が true の場合、 **Numberofchildren**の値は、要求された子オブジェクト名を格納するために必要な出力バッファーのサイズ (バイト単位) になります。

コード例では、出力バッファーに必要なサイズを取得した後、次の一連の操作を実行して2番目の要求を処理します。これにより、要求された子オブジェクトのパスと名前が返されます。

1.  必要なサイズの出力バッファーをバイト単位で割り当てます。

2.  ドライバーが提供する**Senddownstreamirp**関数を呼び出して、2番目の要求を親デバイスに同期的に送信します。

3.  ACPI ドライバーが**署名**メンバーを ACPI\_ENUM に設定していることを確認します。\_子は\_出力\_バッファー\_署名により、 **numberofchildren**を1つ以上のオブジェクトのパスと名前を示します。が返されました)。 [**IO\_STATUS\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)の**情報**メンバーを、出力バッファーに割り当てられたサイズに設定します。

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

 

 




