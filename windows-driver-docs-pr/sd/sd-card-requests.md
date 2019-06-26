---
title: SD カードの要求
description: SD カードの要求
ms.assetid: 3c04573a-5fe7-4332-b899-5aff3234f1ad
keywords:
- SD WDK バスでは、要求の処理
- I/O WDK SD バス
- 要求の WDK SD バスの処理
- 同期要求の WDK SD バス
- 非同期要求の WDK SD バス
- SdBusSubmitRequest
- SdBusSubmitRequestAsync
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30305f7ac72962ffc211359cf396407c7843895f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384501"
---
# <a name="sd-card-requests"></a>SD カードの要求


セキュア デジタル (SD) カードのデバイス ドライバーが開き、SD バス ドライバーへのインターフェイスの初期化、後に、要求を送信できます。 要求を送信する 2 つの方法があります: の方法では、同期的に、 [ **SdBusSubmitRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nf-ntddsd-sdbussubmitrequest)ルーチン、および非同期的の方法で、 [ **SdBusSubmitRequestAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nf-ntddsd-sdbussubmitrequestasync)ルーチン。 SD バス ライブラリによってエクスポートされたこれらのルーチンの両方 (*sdbus.lib*)。

同期要求のルーチンは 2 つのパラメーターを受け取ります。 インターフェイスのコンテキストを、要求パケット。

<a href="" id="interface-context"></a>**インターフェイスのコンテキスト**  
デバイス ドライバーがからインターフェイスのコンテキストを取得、**コンテキスト**のメンバー、 [ **SDBUS\_インターフェイス\_標準**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537923(v=vs.85))後構造体使用して、SD インターフェイスを開く[ **SdBusOpenInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nf-ntddsd-sdbusopeninterface)します。 ドライバーは、このコンテキスト情報を渡す必要がありますでたびに、メソッドを呼び出し、インターフェイスです。

<a href="" id="request-packet"></a>**要求パケット**  
デバイス ドライバーの割り当てし、初期化する必要があります、 [ **SDBUS\_要求\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537931(v=vs.85))構造体。 この構造体には、要求の関数と、要求の他の特性を指定します。

**SdBusSubmitRequest**は同期的では返されません状態\_保留します。 IRQL でデバイス ドライバーを実行する必要があります&lt;ディスパッチ\_このルーチンを呼び出すときにレベルします。

非同期要求のルーチンは、次の 5 つのパラメーターを受け取ります。 インターフェイスのコンテキストを、要求パケット、IRP、完了ルーチン、および完了コンテキストへのポインター。

<a href="" id="interface-context"></a>**インターフェイスのコンテキスト**  
このパラメーターは、パラメーターと同じで、同じ名前を同期操作のケースで使用します。

<a href="" id="request-packet"></a>**要求パケット**  
このパラメーターは、パラメーターと同じで、同じ名前を同期操作のケースで使用します。

<a href="" id="irp"></a>**IRP**  
このパラメーターには、割り当て、デバイス ドライバーは IRP またはドライバーから受信したドライバーがドライバー スタックより上にある IRP が格納されます。 IRP は、要求のキャリアとして使用されます。

<a href="" id="completion-routine"></a>**完了ルーチン**  
このパラメーターを保持する[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP パラメーターで指定された IRP の日常的な。

<a href="" id="user-context"></a>**ユーザー コンテキスト**  
このパラメーターは、システムは、完了の日常的なパラメーターで指定した完了ルーチンに渡されるユーザー コンテキスト データへのポインターを保持します。

IRQL でデバイス ドライバーを実行する必要があります&lt;= ディスパッチ\_レベルを呼び出すときに、 **SdBusSubmitRequestAsync**ルーチン。 **SdBusSubmitRequest**は独自の IRP と呼び出しによって割り当てられるラッパー **SdBusSubmitRequestAsync**します。 ドライバーのライターの便宜上提供されます。

次のセクションでは、デバイス ドライバーが SD 要求の 2 つの主要カテゴリのそれぞれを送信する方法を示すコード例を説明します。別の要求については「 [ **SD\_要求\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/ne-ntddsd-sd_request_function)します。

## <a name="secure-digital-sd-property-requests"></a>セキュア デジタル (SD) プロパティの要求


デジタル (SD カード ドライバーの読み取りまたはカードのプロパティを設定するプロパティの要求を使用してセキュリティで保護します。 など、SD カード ドライバーが SD カード書き込み禁止スイッチがロックの位置がまたは、多機能 SDIO カード上の特定の関数用のドライバーよりバス ドライバーに割り当てます数が要求かどうかを判断するプロパティを読み取る可能性があります、関数は、管理します。

次のコード例では、関数の多機能のカードのドライバーが、バス ドライバーからその関数の数を要求可能性がある方法を示しています。

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

このコード例ではデバイス ドライバーは、SD bus 要求パケットを初期化します[ **SDBUS\_要求\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537931(v=vs.85))に渡されます[ **SdBusSubmitRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nf-ntddsd-sdbussubmitrequest)します。 完全に初期化された要求パケットには、次の特徴があります。

<a href="" id="type-of-the-request"></a>**要求の種類**  
コード例では、SDRF を指定します。\_取得\_プロパティ要求で、 **RequestFunction**カードからプロパティを取得するバス ドライバーに指示する要求パケットのメンバー。 については、SDRF\_取得\_プロパティの要求を参照してください[ **SD\_要求\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/ne-ntddsd-sd_request_function)。

<a href="" id="property-to-retrieve"></a>**プロパティを取得するには**  
コード例では、SDP を指定します\_関数\_番号のプロパティ、 **Parameters.GetSetProperty.Property**バス ドライバーの内容を取得するように指示しますが、要求パケットのメンバー、。関数の数値プロパティ。 については、SDP の\_関数\_NUMBER プロパティは、「 [ **SDBUS\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/ne-ntddsd-sdbus_property)します。

<a href="" id="property-contents-and-length"></a>**プロパティの内容と長さ**  
コード例で、デバイスの拡張機能でバッファーへのポインターを与えます、

**Parameters.GetSetProperty.Buffer**要求パケットのメンバー。 バス ドライバーは、関数の数をこの場所に保存します。 コード例では、このバッファーのサイズも格納されます、 **Parameters.GetSetProperty.Length**要求パケットのメンバー。

## <a name="secure-digital-sd-device-command-requests"></a>セキュア デジタル (SD) デバイス コマンドの要求


ドライバーでは、セキュア デジタル (SD) カード コマンド要求を使用して、SD デバイスにコマンドを送信します。 SD コマンド用のプロトコルがで定義されている、*デジタル カードのセキュリティで保護された*仕様。 ドライバーは、後にいつでもコマンド要求を送信できる、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)デバイスを起動する IRP が正常に完了します。

このセクションには、2 つのコード例が含まれています。 コマンドの要求を直接の I/O を使用して、SD カードのレジスタからバイトのデータを読み取ると拡張の I/O を使用して、SD カードに大規模なデータ量を書き込むデバイス コマンドの要求。 2 番目のセクションについては、依存を最初にそのため、リーダーが学習しなければならない最初のセクションで、2 つ目を調査する前に。

[使用してセキュリティで保護されたデジタル要求](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff538051(v=vs.85))

[I/O の拡張を使用してセキュリティで保護されたのデジタル要求](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff538055(v=vs.85))

 

 




