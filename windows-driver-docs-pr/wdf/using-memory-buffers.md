---
title: メモリ バッファーの使用
description: メモリ バッファーの使用
ms.assetid: f5699837-f1ba-4088-82b3-d7e27341fb46
keywords:
- メモリバッファー WDK KMDF
- WDK KMDF のバッファー
- メモリオブジェクト WDK KMDF
- フレームワークオブジェクト WDK KMDF、memory オブジェクト
- ルックアサイドリスト WDK KMDF
- メモリ記述子に WDK KMDF が一覧表示されます。
- MDLs WDK KMDF
- ローカルバッファー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a185fb5a517529ff79059b326aedacfe602480de
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845434"
---
# <a name="using-memory-buffers"></a>メモリ バッファーの使用





通常、ドライバーは、フレームワークや他のドライバーとの間でデータをやり取りしたり、情報をローカルに格納したりするために、メモリバッファーを使用します。 このトピックでは、[フレームワークメモリオブジェクト](#using-framework-memory-objects)、[ルックアサイドリスト](#using-lookaside-lists)、 [mdls](#using-mdls)、および[ローカルバッファー](#allocating-local-buffers)について説明します。

### <a href="" id="using-framework-memory-objects"></a>フレームワークメモリオブジェクトの使用

フレームワークは、*メモリオブジェクト*を使用して、ドライバーがフレームワークに渡すメモリバッファーを記述します。 各フレームワークメモリオブジェクトは、1つのバッファーを表します。

メモリオブジェクトを作成するために、ドライバーは次のいずれかのオブジェクトメソッドを呼び出します。

-   [**Wdfmemorycreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)。メモリオブジェクトを作成し、指定したサイズのメモリバッファーを割り当てます。

-   [**Wdfmemorycreatepreallocated**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)に割り当てられた、事前に割り当てられたバッファーのメモリオブジェクトを作成します。

-   [**Wdfmemorycreatefromlookaside**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)アサイド[リスト](#using-lookaside-lists)からメモリバッファーを作成します。

受信した i/o 要求のバッファーを表すメモリオブジェクトを取得するために、ドライバーは[**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)と[**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)を呼び出します。 I/o 要求のバッファーを取得する方法の詳細については、「[フレームワークベースのドライバーでのデータバッファーへのアクセス](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)」を参照してください。

メモリオブジェクトのバッファーのアドレスとサイズを取得するために、ドライバーは[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出します。

メモリオブジェクトのバッファーにデータを移動するには、ドライバーが[**Wdfmemorycopyfrombuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)または[**Wdfmemorycopyfrombuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer)を呼び出します。 これらのオブジェクトメソッドは、ソースと宛先のサイズを確認し、バッファーオーバーランエラーを防止します。

ドライバーが[**Wdfmemorycreatepreallocated**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)割り当てを呼び出すことによってメモリオブジェクトを作成する場合、 [**Wdfmemoryassign buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer)を呼び出すことによって、メモリオブジェクトに別のバッファーを割り当てることができます。

ドライバーは、i/o 要求を i/o[ターゲット](using-i-o-targets.md)に送信するときに、通常、入力バッファーまたは出力バッファーをフレームワークの i/o[ターゲットオブジェクトメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/)に渡します。 ドライバーは、バッファーを記述するか、メモリオブジェクトハンドルを渡すことによって、 [**WDF\_メモリ\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor)構造体を渡すことによって、バッファーを指定します。 I/o 要求を同期的に送信する i/o ターゲットオブジェクトメソッドには、 **WDF\_メモリ\_記述子**構造体が必要です。また、i/o 要求を非同期に送信するメソッドには、メモリオブジェクトハンドルが必要です。

メモリバッファーが有効な場合の詳細については、「[メモリバッファー](memory-buffer-life-cycle.md)の有効期間」を参照してください。

### <a href="" id="using-lookaside-lists"></a>ルックアサイドリストの使用

ドライバーがほぼ同じサイズのバッファーを多く必要とする場合は、*ルックアサイドリスト*からそれらを割り当てる必要があります。 ドライバーは、 [**Wdfstasistcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdflookasidelistcreate)を呼び出して、ルックアサイドリストを作成します。 その後、ドライバーは、 [**Wdfmemorycreatefromlookaside アサイド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)を呼び出すことによって、ルックアサイドリストからバッファーを取得できます。

ドライバーが[**Wdfmemorycreatefromlookaside**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)を呼び出すたびに、フレームワークはメモリオブジェクトを作成し、ルックアサイドリストからバッファーを取得して、オブジェクトにバッファーを割り当てます。 これらのメモリオブジェクトのいずれかを使用してドライバーが終了したら、 [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出します。これにより、メモリオブジェクトが削除され、バッファー領域がルックアサイドリストに返されます。

オペレーティングシステムは、ルックアサイドリストに割り当てられているメモリリソースを管理します。 ドライバーが使用できないときに、ルックアサイドリストからバッファーを要求した場合 (ドライバーが[**Wdfmemorycreatefromlookaside アサイド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)を初めて呼び出すときなど)、システムはバッファーを割り当ててリストに割り当てます。 ドライバーが[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出したとき (バッファー領域がルックアサイドリストに返された場合)、ドライバーが再度必要になるまで、システムはリストに現在割り当てられていないバッファーを保持します。 システムは、必要に応じてリストのサイズを増やします。たとえば、バッファーを頻繁に要求するドライバーは、より大きなルックアサイドリストを受け取ります。 一方、システムでは、ドライバーがすべてを使用していない場合に、リスト内のバッファーの数を減らすことができます。

### <a href="" id="using-mdls"></a>MDLs の使用

一部のドライバーでは、メモリ記述子リスト (MDLs) を使用してバッファーを記述します。 たとえば、ダイレクトメモリアクセス (DMA) デバイスのドライバーは、そのメソッドを呼び出すときに、 [**Wdfdmatransactioninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)メソッドに MDL を渡す必要があります。

MDLs を使用するドライバーは、 [**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)および[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)を呼び出すことによって、受信した i/o 要求のバッファーを表す MDL を取得できます。

ほとんどのフレームワークベースのドライバーは MDLs を使用しません。

### <a href="" id="allocating-local-buffers"></a>ローカルバッファーの割り当て

ローカルの内部バッファー領域を必要とするドライバーがフレームワークに渡されない場合、バッファーを表すメモリオブジェクトを作成する必要はありません。 ドライバーは、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出して内部バッファーを割り当てることができます。 ドライバーがバッファーの使用を終了したら、 [**Exfreepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreepoolwithtag)を呼び出す必要があります。

ただし、ドライバーでは、ローカルバッファーにメモリオブジェクトを使用することもできます。 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出す代わりに、メモリバッファーを使用する利点は、各オブジェクトの親オブジェクトが削除されたときに、フレームワークによってメモリオブジェクトとバッファーが自動的に削除されることです。

### <a name="aligning-buffers"></a>バッファーの整列

ドライバーでは、 [**WDF\_align\_size\_UP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcore/nf-wdfcore-wdf_align_size_up)または[**WDF\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcore/nf-wdfcore-wdf_align_size_down) ALIGN\_size\_DOWN 関数を使用して、指定された配置オフセットに配置されているバッファーサイズを計算できます。 この計算は、各バッファーをアドレスの配置境界から開始する必要がある場合に、ドライバーが複数の連続するバッファーを割り当てる必要がある場合に便利です。

 

 





