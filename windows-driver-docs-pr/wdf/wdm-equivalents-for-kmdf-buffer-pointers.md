---
title: WDM で WDF のバッファー ポインターに相当するもの
description: WDM で WDF のバッファー ポインターに相当するもの
ms.assetid: 7923A3CA-479A-4C7D-B428-F57C9701906E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c2b9a9a11234afa22da5492671e22d01614d5d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354429"
---
# <a name="wdm-equivalents-for-wdf-buffer-pointers"></a>WDM で WDF のバッファー ポインターに相当するもの


カーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) ドライバーは、バッファーとダイレクト I/O の I/O バッファーを取得するため、次のメソッドを使用します。 指定しない場合、メソッドは、KMDF と UMDF の両方に適用されます。

-   [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)
-   [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)
-   [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)
-   [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)
-   [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)
-   [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)

次の表に説明する取得メソッドが返す IRP の\_MJ\_読み取り、IRP\_MJ\_書き込み、および IRP\_MJ\_デバイス\_コントロール要求バッファリングダイレクト I/O。 どちらの i/o 要求では、ドライバーは、要求元のユーザー モード プロセスのコンテキストで実行中にバッファーを取得する必要がありますので、特別な処理が必要です。

## <a href="" id="read"></a>IRP のバッファー\_MJ\_読み取り要求


KMDF ドライバーでは、読み取り要求のためのバッファーを取得する呼び出しのいずれか、**WdfRequestRetrieveOutput * * * Xxx*メソッド。 バッファー、ドライバーがバッファリングまたはダイレクト I/O を実行するかどうかによって異なります、これらの各メソッドを返します。 次の表には、WDM 用語では、各メソッドによって返されるポインターがについて説明します。

| 関数                                                                             | バッファー内の I/O                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp -&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | メモリの記述子のリスト (MDL) のビルドを**Irp -&gt;AssociatedIrp.SystemBuffer** MDL を返します。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を取得するには、このオブジェクトの**Irp -&gt;AssociatedIrp.SystemBuffer**します。 | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を取得するには、このオブジェクトの[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;MdlAddress**)。 |

 

## <a href="" id="write"></a>IRP のバッファー\_MJ\_書き込み要求


KMDF ドライバーでは、書き込み要求のためのバッファーを取得する呼び出しのいずれか、**WdfRequestRetrieveInput * * * Xxx*メソッド。 バッファー、ドライバーがバッファリングまたはダイレクト I/O を実行するかどうかによって異なります、これらの各メソッドを返します。 次の表には、WDM 用語では、各メソッドによって返されるポインターがについて説明します。

| 関数                                                                           | バッファー内の I/O                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp -&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) | ビルドの MDL **Irp -&gt;AssociatedIrp.SystemBuffer** MDL を返します。                                                                   | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)             | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を取得するには、このオブジェクトの**Irp -&gt;AssociatedIrp.SystemBuffer**します。 | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を取得するには、このオブジェクトの[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;MdlAddress**)。 |

 

## <a href="" id="device-control"></a>IRP のバッファー\_MJ\_デバイス\_に対する制御要求


KMDF ドライバーでは、デバイスの I/O 制御要求のためのバッファーを取得する呼び出しか**WdfRequestRetrieveInputXxx**または**WdfRequestRetrieveOutputXxx**メソッド。 バッファーのドライバーを実行するかどうかによって異なります、これらの各メソッドを返します[バッファリングまたはダイレクト I/O](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)次の表に示すように。

| 関数                                                                             | バッファー内の I/O                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)               | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp -&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)   | ビルドの MDL **Irp -&gt;AssociatedIrp.SystemBuffer** MDL を返します。                                                                   | ビルドの MDL **Irp -&gt;AssociatedIrp.SystemBuffer** MDL を返します。                                                                                                                             |
| [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)               | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を取得するには、このオブジェクトの**Irp -&gt;AssociatedIrp.SystemBuffer**します。 | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を取得するには、このオブジェクトの[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;MdlAddress**)。 |
| [**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp -&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) | メモリの記述子のリスト (MDL) のビルドを**Irp -&gt;AssociatedIrp.SystemBuffer** MDL を返します。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)             | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を取得するには、このオブジェクトの**Irp -&gt;AssociatedIrp.SystemBuffer**します。 | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を取得するには、このオブジェクトの[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) (**Irp&gt;MdlAddress**)。 |

 

 

 





