---
title: メモリ バッファーの使用
description: メモリ バッファーの使用
ms.assetid: f5699837-f1ba-4088-82b3-d7e27341fb46
keywords:
- メモリ バッファーの WDK KMDF
- バッファー WDK KMDF
- メモリ オブジェクト WDK KMDF
- フレームワークは、WDK KMDF、メモリ オブジェクトをオブジェクトします。
- ルック アサイド リストの WDK KMDF
- メモリの記述子には、WDK KMDF が一覧表示されます。
- MDLs WDK KMDF
- WDK KMDF のローカル バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c74e631612ba02c1187d3e5f10d9d0ddc31ec5d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372224"
---
# <a name="using-memory-buffers"></a>メモリ バッファーの使用





ドライバーは、通常には、framework およびその他のドライバーとの間のデータを渡す、またはローカル情報を格納するメモリ バッファーの機能を使用します。 このトピックで説明[framework メモリ オブジェクト](#using-framework-memory-objects)、[ルック アサイド リスト](#using-lookaside-lists)、 [MDLs](#using-mdls)、および[ローカル バッファー](#allocating-local-buffers)します。

### <a href="" id="using-framework-memory-objects"></a> Framework メモリ オブジェクトを使用します。

フレームワークを使用して*メモリ オブジェクト*ドライバーから受信し、フレームワークに通過するメモリ バッファーを記述します。 各フレームワークのメモリ オブジェクトでは、1 つのバッファーを表します。

メモリ オブジェクトを作成するには、ドライバーは次のオブジェクトのメソッドのいずれかを呼び出します。

-   [**WdfMemoryCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreate)、メモリ オブジェクトを作成して、指定したサイズのメモリ バッファーを割り当てます。

-   [**WdfMemoryCreatePreallocated**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)、事前に割り当てられるバッファーのメモリ オブジェクトを作成します。

-   [**WdfMemoryCreateFromLookaside**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)からのメモリ バッファーを作成し、[ルック アサイド リスト](#using-lookaside-lists)します。

受信の I/O 要求を表すメモリ オブジェクトを取得するバッファー、ドライバーの呼び出し[ **WdfRequestRetrieveInputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)と[ **WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)します。 詳細については、I/O 要求のバッファーを取得する方法については、次を参照してください。 [Framework ベースのドライバーでのデータ バッファーへのアクセス](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)します。

メモリ オブジェクトのバッファーのサイズとアドレスを取得するには、ドライバーが呼び出す[ **WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)します。

メモリ オブジェクトのバッファーの内外にデータを移動するには、ドライバーを呼び出すか[ **WdfMemoryCopyFromBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)または[ **WdfMemoryCopyToBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer). これらのオブジェクトのメソッドは、ソースと変換先のサイズを確認し、バッファー オーバーラン エラーを回避します。

ドライバーは、呼び出すことによってメモリ オブジェクトを作成する場合[ **WdfMemoryCreatePreallocated**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)、呼び出すことによって、メモリ オブジェクトを別のバッファーを割り当てる、ことができます、その後[ **WdfMemoryAssignBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer)します。

ドライバーが I/O 要求を送信すると、 [I/O ターゲット](using-i-o-targets.md)、通常への入力または出力バッファーを渡す、 [framework I/O ターゲット オブジェクトのメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/)します。 ドライバーは、いずれかを渡すことによって、バッファーを指定します、 [ **WDF\_メモリ\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor)バッファーを記述またはメモリ オブジェクトを渡すことによって処理される構造体。 (同期的に I/O 要求の送信 I/O ターゲット オブジェクトのメソッドが必要です、 **WDF\_メモリ\_記述子**構造、およびメソッドを非同期的に必要なメモリ オブジェクトのハンドルを I/O 要求を送信します)。

メモリ バッファーが有効な場合については、次を参照してください。[メモリ バッファーのライフ サイクル](memory-buffer-life-cycle.md)します。

### <a href="" id="using-lookaside-lists"></a> ルック アサイド リストの使用

割り当てる必要があります、ドライバーには、ほぼ同じサイズのバッファーが多は必要がある場合、*ルック アサイド リスト*します。 ドライバーは、呼び出してルック アサイド リストを作成します。 [ **WdfLookasideListCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdflookasidelistcreate)します。 その後、ドライバーできますバッファー ルック アサイド リストから呼び出すことによって取得[ **WdfMemoryCreateFromLookaside**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)します。

ドライバーの呼び出しごとに[ **WdfMemoryCreateFromLookaside**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)フレームワークは、メモリ オブジェクトを作成し、ルック アサイド リストからバッファーを取得します。 オブジェクトにバッファーを割り当てます。 ドライバーがいつ終了した呼び出し、これらのメモリ オブジェクトのいずれかを使用して[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)、メモリ オブジェクトを削除してルック アサイド リストにバッファー領域を返します。

オペレーティング システムでは、ルック アサイド リストに割り当てられているメモリ リソースを管理します。 ドライバーは、いずれも、ドライバーを呼び出す最初の時間など、使用できない場合にルック アサイド リストからバッファーを要求した場合[ **WdfMemoryCreateFromLookaside**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatefromlookaside)システムのバッファーを割り当て、割り当てますリストします。 ドライバーを呼び出すと[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete) (とルック アサイド リストにバッファー領域が返されます)、ドライバーは、これをもう一度必要になるまで、システムが一覧に現在割り当てられていないバッファーを保持します。 システムには、必要に応じ、リストのサイズが大きくなります。たとえば、ドライバーの詳細は頻繁にバッファーを要求するには、ルック アサイド リストが大きいが表示されます。 その一方で、ドライバーがすべてを使用しない場合は、システムは、リスト内のバッファーの数を減らす可能性があります。

### <a href="" id="using-mdls"></a> MDLs を使用します。

一部のドライバーでは、記述子の一覧 (MDLs) バッファーを記述するメモリを使用します。 たとえば、ダイレクト メモリ アクセス (DMA) デバイス用のドライバーの MDL を渡す必要があります、 [ **WdfDmaTransactionInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)メソッドでは、このメソッドを呼び出しています。

MDLs を使用するドライバーを呼び出すことによって、受信した I/O 要求のバッファーを表す MDL を取得できます[ **WdfRequestRetrieveInputWdmMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)と[ **WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)します。

ほとんどのフレームワーク ベースのドライバーでは、MDLs は使用しないでください。

### <a href="" id="allocating-local-buffers"></a> ローカル バッファーの割り当てください。

フレームワークに合格しないローカルの内部バッファー領域が必要なドライバーをメモリ バッファーを表すオブジェクトを作成する必要はありません。 ドライバーが呼び出せる[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)内部バッファーを割り当てる。 呼び出す必要がありますが、ドライバーは、バッファーの使用が完了したら、 [ **ExFreePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreepoolwithtag)します。

ただし、ドライバーはローカル バッファーのメモリ オブジェクトを使用することができますも。 呼び出す代わりに、メモリ バッファーを使用する利点[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)、いるフレームワークと自動的に削除メモリ オブジェクトとそのバッファーの各オブジェクトの親オブジェクトが、削除されます。

### <a name="aligning-buffers"></a>バッファーの整列

ドライバーを使用できます、 [ **WDF\_ALIGN\_サイズ\_を**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcore/nf-wdfcore-wdf_align_size_up)または[ **WDF\_ALIGN\_サイズ\_ダウン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcore/nf-wdfcore-wdf_align_size_down)指定された配置のオフセットに配置されるバッファー サイズを計算する関数。 この計算は、各バッファーは、アドレスのアラインメント境界で開始する必要がある場合は、ドライバーは、複数の連続したバッファーを割り当てる必要がある場合に便利です。

 

 





