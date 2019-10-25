---
title: SD カードの要求
description: SD カードの要求
ms.assetid: 3c04573a-5fe7-4332-b899-5aff3234f1ad
keywords:
- SD WDK バス、要求の処理
- I/o WDK SD bus
- WDK SD bus の要求の処理
- 同期要求 WDK SD バス
- 非同期要求の WDK SD バス
- SdBusSubmitRequest
- SdBusSubmitRequestAsync
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc4a7e4276bb124113f5b1ae34b78ee9cd156948
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842459"
---
# <a name="sd-card-requests"></a>SD カードの要求


セキュアデジタル (SD) カードデバイスドライバが、SD bus ドライバのインターフェイスを開いて初期化した後、要求を送信できます。 要求を送信するには、 [**Sdbussubmitrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequest)ルーチンによって同期的に要求を送信する方法と、 [**Sdbussubmitrequestasync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequestasync)ルーチンを介して非同期的に送信する方法の2つの方法があります。 これらのルーチンはどちらも、SD bus ライブラリ (*sdbus .lib*) によってエクスポートされます。

同期要求ルーチンは、インターフェイスコンテキストと要求パケットの2つのパラメーターを受け取ります。

<a href="" id="interface-context"></a>**インターフェイスコンテキスト**  
デバイスドライバーは、 [**Sdbusopeninterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbusopeninterface)で SD インターフェイスを開いた後、 [**sdbus\_インターフェイス\_** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537923(v=vs.85))の**コンテキスト**メンバーからインターフェイスコンテキストを取得します。 ドライバーは、インターフェイスのメソッドを呼び出すたびに、このコンテキスト情報をに渡す必要があります。

<a href="" id="request-packet"></a>**パケットの要求**  
デバイスドライバーは、 [**Sdbus\_要求\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537931(v=vs.85))構造を割り当てて初期化する必要があります。 この構造体は、要求の関数とその他の要求の特性を指定します。

**Sdbussubmitrequest**は同期的であるため、状態\_PENDING を返しません。 このルーチンを呼び出すときに、デバイスドライバーが IRQL &lt; ディスパッチ\_レベルで実行されている必要があります。

非同期要求ルーチンは、インターフェイスコンテキスト、要求パケット、IRP、完了ルーチンへのポインター、および完了コンテキストの5つのパラメーターを受け取ります。

<a href="" id="interface-context"></a>**インターフェイスコンテキスト**  
このパラメーターは、同期ケースで使用される同じ名前のパラメーターと同じです。

<a href="" id="request-packet"></a>**パケットの要求**  
このパラメーターは、同期ケースで使用される同じ名前のパラメーターと同じです。

<a href="" id="irp"></a>**IRP**  
このパラメーターには、デバイスドライバーによって割り当てられた IRP、またはドライバーがドライバースタック内のその上にあるドライバーから受け取った IRP が保持されます。 IRP は、要求の通信事業者として使用されます。

<a href="" id="completion-routine"></a>**完了ルーチン**  
このパラメーターは、IRP パラメーターに指定された IRP の[**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを保持します。

<a href="" id="user-context"></a>**ユーザーコンテキスト**  
このパラメーターは、システムが完了ルーチンパラメーターで指定された完了ルーチンに渡すユーザーコンテキストデータへのポインターを保持します。

デバイスドライバーは、 **Sdbussubmitrequestasync**ルーチンを呼び出すときに、IRQL &lt;= ディスパッチ\_レベルで実行されている必要があります。 **Sdbussubmitrequest**は、独自の IRP を割り当て、 **Sdbussubmitrequestasync**を呼び出すラッパーです。 これは、ドライバーライターを使いやすくするために用意されています。

次のセクションでは、デバイスドライバーが SD 要求の2つのプリンシパルカテゴリをそれぞれ送信する方法を示すコード例を示します。さまざまな要求の説明については、「 [**sd\_REQUEST\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sd_request_function)」を参照してください。

## <a name="secure-digital-sd-property-requests"></a>セキュアデジタル (SD) プロパティ要求


セキュアデジタル (SD) カードドライバーは、プロパティ要求を使用してカードのプロパティの読み取りまたは設定を行います。 たとえば、sd カードドライバーは、SD カードの書き込み保護スイッチがロックされた位置にあるかどうかを判断するためにプロパティを読み取ります。また、多機能 SDIO カードの特定の機能のドライバーが、バスドライバーが割り当てたit が管理する関数。

次のコード例は、多機能カード上の関数のドライバーが、バスドライバーからの関数番号を要求する方法を示しています。

```cpp
 sdrp = ExAllocatePool(NonPagedPool, 
 sizeof(SDBUS_REQUEST_PACKET));
 if (!sdrp) {
 return STATUS_INSUFFICIENT_RESOURCES;
 }
 RtlZeroMemory(sdrp, sizeof(SDBUS_REQUEST_PACKET));
 sdrp->RequestFunction = SDRF_GET_PROPERTY;
 sdrp->Parameters.GetSetProperty.Property = 
 SDP_FUNCTION_NUMBER;
 sdrp->Parameters.GetSetProperty.Buffer = 
 &pDevExt->FunctionNumber;
 sdrp->Parameters.GetSetProperty.Length = 
 sizeof(pDevExt->FunctionNumber);
 status = SdBusSubmitRequest (pDevExt->BusInterface.Context,sdrp);
 ExFreePool(sdrp);
 if (!NT_SUCCESS(status)) {
 return status;
 }
```

このコード例では、デバイスドライバーは SD bus 要求パケット、 [**sdbus\_要求\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537931(v=vs.85))を初期化し、それを[**Sdbussubmitrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequest)に渡します。 完全に初期化された要求パケットには、次の特性があります。

<a href="" id="type-of-the-request"></a>**要求の種類**  
このコード例では、要求パケットの**Requestfunction**メンバーで SDRF\_GET\_property 要求を指定しています。これにより、カードからプロパティを取得するようにバスドライバーに指示します。 SDRF\_GET\_PROPERTY 要求の詳細については、「 [**SD\_request\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sd_request_function)」を参照してください。

<a href="" id="property-to-retrieve"></a>**取得するプロパティ**  
このコード例では、SDP\_関数\_NUMBER プロパティを指定しています。これは、要求パケットの**GetSetProperty**プロパティメンバーです。これは、関数番号プロパティの内容を取得するようにバスドライバーに指示します。 SDP\_関数\_NUMBER プロパティの説明については、「 [**Sdbus\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sdbus_property)」を参照してください。

<a href="" id="property-contents-and-length"></a>**プロパティの内容と長さ**  
このコード例では、デバイス拡張機能のバッファーへのポインターを

**Parameters. GetSetProperty。** 要求パケットのバッファーのメンバー。 バスドライバーは、この場所に関数番号を格納します。 このコード例では、このバッファーのサイズも要求パケットの**パラメーター. GetSetProperty. Length**メンバーに格納されています。

## <a name="secure-digital-sd-device-command-requests"></a>セキュアデジタル (SD) デバイスコマンド要求


ドライバーは SD デバイスにコマンドを送信するために、セキュアデジタル (SD) カードコマンド要求を使用します。 SD コマンドのプロトコルは、セキュリティで保護された*デジタルカード*仕様で定義されています。 ドライバーは、 [**irp\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)が完了した後にいつでもコマンド要求を送信できます。\_デバイスの IRP が開始されると、デバイスが正常に起動します。

このセクションには、2つのコード例が含まれています。 direct i/o を使用して SD カードのレジスタからデータバイトを読み取るコマンド要求と、拡張 i/o を使用して SD カードに大量のデータを書き込むデバイスコマンド要求です。 2番目のセクションの説明は最初の部分に依存しているため、読者は2番目のセクションを学習する前に最初のセクションを調べる必要があります。

[使用するデジタル要求をセキュリティで保護する](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff538051(v=vs.85))

[拡張 i/o を使用するデジタル要求をセキュリティで保護する](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff538055(v=vs.85))

 

 




