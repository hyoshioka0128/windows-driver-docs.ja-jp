---
title: WDM で WDF のバッファー ポインターに相当するもの
description: WDM で WDF のバッファー ポインターに相当するもの
ms.assetid: 7923A3CA-479A-4C7D-B428-F57C9701906E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e87bc8cc393d9ad62d8e79d7ea6b056e5e6a6ae7
ms.sourcegitcommit: 41a1b058cdb6c10d3b5fe80e01f044e827687641
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69979401"
---
# <a name="wdm-equivalents-for-wdf-buffer-pointers"></a>WDM で WDF のバッファー ポインターに相当するもの


カーネルモードドライバーフレームワーク (KMDF) またはユーザーモードドライバーフレームワーク (UMDF) ドライバーでは、バッファーおよびダイレクト i/o の i/o バッファーを取得するために次のメソッドを使用します。 特に指定がない限り、メソッドは KMDF と UMDF の両方に適用されます。

-   [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)
-   [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)
-   [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)
-   [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)
-   [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)
-   [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)

次の表は、バッファー\_に対する irp MJ\_READ、irp\_MJ\_WRITE、および irp\_MJ\_デバイス\_制御要求に対して返される取得方法を示しています。およびダイレクト i/o。 I/o に対する要求では、要求元のユーザーモードプロセスのコンテキストで実行中にバッファーを取得する必要があるため、特別な処理は必要ありません。

## <a href="" id="read"></a>IRP\_MJ\_読み取り要求のバッファー


読み取り要求のバッファーを取得するために、KMDF ドライバーは**WdfRequestRetrieveOutput**_Xxx_メソッドの1つを呼び出します。 これらの各メソッドが返すバッファーは、ドライバーがバッファーまたは直接 i/o のどちらを実行するかによって異なります。 次の表では、WDM 用語の各メソッドによって返されるポインターについて説明します。

| 関数                                                                             | バッファーされる i/o                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp-&gt;AssociatedIrp**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)(**Irp-&gt;mdladdress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | AssociatedIrp のメモリ記述子リスト (mdl) を構築し、mdl を返します。 **&gt;**                                           | **Irp-&gt;mdladdress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して **、&gt;AssociatedIrp**を取得します。 | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;-mdladdress**) を取得します。 |

 

## <a href="" id="write"></a>IRP\_MJ\_書き込み要求のバッファー


書き込み要求のバッファーを取得するために、KMDF ドライバーは**WdfRequestRetrieveInput**_Xxx_メソッドの1つを呼び出します。 これらの各メソッドが返すバッファーは、ドライバーがバッファーまたは直接 i/o のどちらを実行するかによって異なります。 次の表では、WDM 用語の各メソッドによって返されるポインターについて説明します。

| 関数                                                                           | バッファーされる i/o                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)             | **Irp-&gt;AssociatedIrp**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)(**Irp-&gt;mdladdress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) | AssociatedIrp の mdl をビルドし、mdl を返します。 **&gt;**                                                                   | **Irp-&gt;mdladdress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)             | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して **、&gt;AssociatedIrp**を取得します。 | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;-mdladdress**) を取得します。 |

 

## <a href="" id="device-control"></a>IRP\_MJ\_デバイス制御要求のバッファー\_


デバイス i/o 制御要求のバッファーを取得するために、KMDF ドライバーは**WdfRequestRetrieveInputXxx**メソッドまたは**WdfRequestRetrieveOutputXxx**メソッドを呼び出します。 次の表に示すように、これらの各メソッドが返すバッファーは、ドライバーが[バッファーまたは直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)を実行するかどうかによって異なります。

| 関数                                                                             | バッファーされる i/o                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)               | **Irp-&gt;AssociatedIrp**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)(**Irp-&gt;mdladdress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)   | AssociatedIrp の mdl をビルドし、mdl を返します。 **&gt;**                                                                   | AssociatedIrp の mdl をビルドし、mdl を返します。 **&gt;**                                                                                                                             |
| [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)               | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して **、&gt;AssociatedIrp**を取得します。 | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;-mdladdress**) を取得します。 |
| [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp-&gt;AssociatedIrp**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)(**Irp-&gt;mdladdress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | AssociatedIrp のメモリ記述子リスト (mdl) を構築し、mdl を返します。 **&gt;**                                           | **Irp-&gt;mdladdress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して **、&gt;AssociatedIrp**を取得します。 | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;-mdladdress**) を取得します。 |

 

 

 





