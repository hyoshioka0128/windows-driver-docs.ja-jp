---
title: WDM で WDF のバッファー ポインターに相当するもの
description: WDM で WDF のバッファー ポインターに相当するもの
ms.assetid: 7923A3CA-479A-4C7D-B428-F57C9701906E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d74318e20729b8155e818d5fd585f722f7337ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842793"
---
# <a name="wdm-equivalents-for-wdf-buffer-pointers"></a>WDM で WDF のバッファー ポインターに相当するもの


カーネルモードドライバーフレームワーク (KMDF) またはユーザーモードドライバーフレームワーク (UMDF) ドライバーでは、バッファーおよびダイレクト i/o の i/o バッファーを取得するために次のメソッドを使用します。 特に指定がない限り、メソッドは KMDF と UMDF の両方に適用されます。

-   [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)
-   [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)
-   [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)
-   [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)
-   [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)
-   [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)

次の表では、IRP\_MJ\_READ、IRP\_MJ\_WRITE、および IRP\_MJ\_デバイス\_バッファーおよびダイレクト i/o の要求を制御する方法について説明します。 I/o に対する要求では、要求元のユーザーモードプロセスのコンテキストで実行中にバッファーを取得する必要があるため、特別な処理は必要ありません。

## <a href="" id="read"></a>IRP\_MJ\_読み取り要求のバッファー


読み取り要求のバッファーを取得するために、KMDF ドライバーは**WdfRequestRetrieveOutput**_Xxx_メソッドの1つを呼び出します。 これらの各メソッドが返すバッファーは、ドライバーがバッファーまたは直接 i/o のどちらを実行するかによって異なります。 次の表では、WDM 用語の各メソッドによって返されるポインターについて説明します。

| 関数                                                                             | バッファーされる i/o                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp-&gt;AssociatedIrp**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;mdladdress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | **Irp&gt;AssociatedIrp**のメモリ記述子リスト (mdl) をビルドし、mdl を返します。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して **、Irp&gt;AssociatedIrp**を取得します。 | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;mdladdress**) を取得します。 |

 

## <a href="" id="write"></a>IRP\_MJ\_書き込み要求のバッファー


書き込み要求のバッファーを取得するために、KMDF ドライバーは**WdfRequestRetrieveInput**_Xxx_メソッドの1つを呼び出します。 これらの各メソッドが返すバッファーは、ドライバーがバッファーまたは直接 i/o のどちらを実行するかによって異なります。 次の表では、WDM 用語の各メソッドによって返されるポインターについて説明します。

| 関数                                                                           | バッファーされる i/o                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)             | **Irp-&gt;AssociatedIrp**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;mdladdress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) | **Irp&gt;AssociatedIrp**の mdl をビルドし、mdl を返します。                                                                   | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)             | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して **、Irp&gt;AssociatedIrp**を取得します。 | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;mdladdress**) を取得します。 |

 

## <a href="" id="device-control"></a>IRP\_MJ\_デバイス\_制御要求のバッファー


デバイス i/o 制御要求のバッファーを取得するために、KMDF ドライバーは**WdfRequestRetrieveInputXxx**メソッドまたは**WdfRequestRetrieveOutputXxx**メソッドを呼び出します。 次の表に示すように、これらの各メソッドが返すバッファーは、ドライバーが[バッファーまたは直接 i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)を実行するかどうかによって異なります。

| 関数                                                                             | バッファーされる i/o                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)               | **Irp-&gt;AssociatedIrp**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;mdladdress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)   | **Irp&gt;AssociatedIrp**の mdl をビルドし、mdl を返します。                                                                   | **Irp&gt;AssociatedIrp**の mdl をビルドし、mdl を返します。                                                                                                                             |
| [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)               | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して **、Irp&gt;AssociatedIrp**を取得します。 | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;mdladdress**) を取得します。 |
| [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp-&gt;AssociatedIrp**                                                                                                          | [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;mdladdress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | **Irp&gt;AssociatedIrp**のメモリ記述子リスト (mdl) をビルドし、mdl を返します。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して **、Irp&gt;AssociatedIrp**を取得します。 | WDFMEMORY オブジェクトを返します。 このオブジェクトの[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出して、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp-&gt;mdladdress**) を取得します。 |

 

 

 





