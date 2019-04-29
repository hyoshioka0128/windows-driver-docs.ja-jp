---
title: WDM で WDF のバッファー ポインターに相当するもの
description: WDM で WDF のバッファー ポインターに相当するもの
ms.assetid: 7923A3CA-479A-4C7D-B428-F57C9701906E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abb7431bfd12eab85ea1071b587fc94c019a1b0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323429"
---
# <a name="wdm-equivalents-for-wdf-buffer-pointers"></a>WDM で WDF のバッファー ポインターに相当するもの


カーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) ドライバーは、バッファーとダイレクト I/O の I/O バッファーを取得するため、次のメソッドを使用します。 指定しない場合、メソッドは、KMDF と UMDF の両方に適用されます。

-   [**WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)
-   [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)**](https://msdn.microsoft.com/library/windows/hardware/ff550021)
-   [**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)
-   [**WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)
-   [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)**](https://msdn.microsoft.com/library/windows/hardware/ff550016)
-   [**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)

次の表に説明する取得メソッドが返す IRP の\_MJ\_読み取り、IRP\_MJ\_書き込み、および IRP\_MJ\_デバイス\_コントロール要求バッファリングダイレクト I/O。 どちらの i/o 要求では、ドライバーは、要求元のユーザー モード プロセスのコンテキストで実行中にバッファーを取得する必要がありますので、特別な処理が必要です。

## <a href="" id="read"></a>IRP のバッファー\_MJ\_読み取り要求


KMDF ドライバーでは、読み取り要求のためのバッファーを取得する呼び出しのいずれか、**WdfRequestRetrieveOutput * * * Xxx*メソッド。 バッファー、ドライバーがバッファリングまたはダイレクト I/O を実行するかどうかによって異なります、これらの各メソッドを返します。 次の表には、WDM 用語では、各メソッドによって返されるポインターがについて説明します。

| 関数                                                                             | バッファー内の I/O                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp -&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)**](https://msdn.microsoft.com/library/windows/hardware/ff550021) | メモリの記述子のリスト (MDL) のビルドを**Irp -&gt;AssociatedIrp.SystemBuffer** MDL を返します。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)             | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)を取得するには、このオブジェクトの**Irp -&gt;AssociatedIrp.SystemBuffer**します。 | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)を取得するには、このオブジェクトの[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp&gt;MdlAddress**)。 |

 

## <a href="" id="write"></a>IRP のバッファー\_MJ\_書き込み要求


KMDF ドライバーでは、書き込み要求のためのバッファーを取得する呼び出しのいずれか、**WdfRequestRetrieveInput * * * Xxx*メソッド。 バッファー、ドライバーがバッファリングまたはダイレクト I/O を実行するかどうかによって異なります、これらの各メソッドを返します。 次の表には、WDM 用語では、各メソッドによって返されるポインターがについて説明します。

| 関数                                                                           | バッファー内の I/O                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp -&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)**](https://msdn.microsoft.com/library/windows/hardware/ff550016) | ビルドの MDL **Irp -&gt;AssociatedIrp.SystemBuffer** MDL を返します。                                                                   | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)             | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)を取得するには、このオブジェクトの**Irp -&gt;AssociatedIrp.SystemBuffer**します。 | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)を取得するには、このオブジェクトの[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp&gt;MdlAddress**)。 |

 

## <a href="" id="device-control"></a>IRP のバッファー\_MJ\_デバイス\_に対する制御要求


KMDF ドライバーでは、デバイスの I/O 制御要求のためのバッファーを取得する呼び出しか**WdfRequestRetrieveInputXxx**または**WdfRequestRetrieveOutputXxx**メソッド。 バッファーのドライバーを実行するかどうかによって異なります、これらの各メソッドを返します[バッファリングまたはダイレクト I/O](https://msdn.microsoft.com/library/windows/hardware/ff540701)次の表に示すように。

| 関数                                                                             | バッファー内の I/O                                                                                                                                    | ダイレクト I/O                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)               | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp -&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveInputWdmMdl (KMDF のみ)**](https://msdn.microsoft.com/library/windows/hardware/ff550016)   | ビルドの MDL **Irp -&gt;AssociatedIrp.SystemBuffer** MDL を返します。                                                                   | ビルドの MDL **Irp -&gt;AssociatedIrp.SystemBuffer** MDL を返します。                                                                                                                             |
| [**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)               | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)を取得するには、このオブジェクトの**Irp -&gt;AssociatedIrp.SystemBuffer**します。 | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)を取得するには、このオブジェクトの[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp&gt;MdlAddress**)。 |
| [**WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)             | **Irp-&gt;AssociatedIrp.SystemBuffer**                                                                                                          | [**MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp -&gt;MdlAddress**)                                                                                                          |
| [**WdfRequestRetrieveOutputWdmMdl (KMDF のみ)**](https://msdn.microsoft.com/library/windows/hardware/ff550021) | メモリの記述子のリスト (MDL) のビルドを**Irp -&gt;AssociatedIrp.SystemBuffer** MDL を返します。                                           | **Irp-&gt;MdlAddress**                                                                                                                                                                                    |
| [**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)             | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)を取得するには、このオブジェクトの**Irp -&gt;AssociatedIrp.SystemBuffer**します。 | WDFMEMORY オブジェクトを返します。 呼び出す[ **WdfMemoryGetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548715)を取得するには、このオブジェクトの[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559) (**Irp&gt;MdlAddress**)。 |

 

 

 





