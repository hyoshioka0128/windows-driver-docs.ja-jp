---
title: メモリ バッファーを使用します。
description: メモリ バッファーを使用します。
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
ms.openlocfilehash: 92b784d2603ffd40fece586072797aeadcc2c6e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560420"
---
# <a name="using-memory-buffers"></a>メモリ バッファーを使用します。





ドライバーは、通常には、framework およびその他のドライバーとの間のデータを渡す、またはローカル情報を格納するメモリ バッファーの機能を使用します。 このトピックで説明[framework メモリ オブジェクト](#using-framework-memory-objects)、[ルック アサイド リスト](#using-lookaside-lists)、 [MDLs](#using-mdls)、および[ローカル バッファー](#allocating-local-buffers)します。

### <a href="" id="using-framework-memory-objects"></a> Framework メモリ オブジェクトを使用します。

フレームワークを使用して*メモリ オブジェクト*ドライバーから受信し、フレームワークに通過するメモリ バッファーを記述します。 各フレームワークのメモリ オブジェクトでは、1 つのバッファーを表します。

メモリ オブジェクトを作成するには、ドライバーは次のオブジェクトのメソッドのいずれかを呼び出します。

-   [**WdfMemoryCreate**](https://msdn.microsoft.com/library/windows/hardware/ff548706)、メモリ オブジェクトを作成して、指定したサイズのメモリ バッファーを割り当てます。

-   [**WdfMemoryCreatePreallocated**](https://msdn.microsoft.com/library/windows/hardware/ff548712)、事前に割り当てられるバッファーのメモリ オブジェクトを作成します。

-   [**WdfMemoryCreateFromLookaside**](https://msdn.microsoft.com/library/windows/hardware/ff548709)からのメモリ バッファーを作成し、[ルック アサイド リスト](#using-lookaside-lists)します。

受信の I/O 要求を表すメモリ オブジェクトを取得するバッファー、ドライバーの呼び出し[ **WdfRequestRetrieveInputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff550015)と[ **WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)します。 詳細については、I/O 要求のバッファーを取得する方法については、次を参照してください。 [Framework ベースのドライバーでのデータ バッファーへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff540701)します。

メモリ オブジェクトのバッファーのサイズとアドレスを取得するには、ドライバーが呼び出す[ **WdfMemoryGetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548715)します。

メモリ オブジェクトのバッファーの内外にデータを移動するには、ドライバーを呼び出すか[ **WdfMemoryCopyFromBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548701)または[ **WdfMemoryCopyToBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548703). これらのオブジェクトのメソッドは、ソースと変換先のサイズを確認し、バッファー オーバーラン エラーを回避します。

ドライバーは、呼び出すことによってメモリ オブジェクトを作成する場合[ **WdfMemoryCreatePreallocated**](https://msdn.microsoft.com/library/windows/hardware/ff548712)、呼び出すことによって、メモリ オブジェクトを別のバッファーを割り当てる、ことができます、その後[ **WdfMemoryAssignBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548697)します。

ドライバーが I/O 要求を送信すると、 [I/O ターゲット](using-i-o-targets.md)、通常への入力または出力バッファーを渡す、 [framework I/O ターゲット オブジェクトのメソッド](https://msdn.microsoft.com/library/windows/hardware/dn265644)します。 ドライバーは、いずれかを渡すことによって、バッファーを指定します、 [ **WDF\_メモリ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff552392)バッファーを記述またはメモリ オブジェクトを渡すことによって処理される構造体。 (同期的に I/O 要求の送信 I/O ターゲット オブジェクトのメソッドが必要です、 **WDF\_メモリ\_記述子**構造、およびメソッドを非同期的に必要なメモリ オブジェクトのハンドルを I/O 要求を送信します)。

メモリ バッファーが有効な場合については、次を参照してください。[メモリ バッファーのライフ サイクル](memory-buffer-life-cycle.md)します。

### <a href="" id="using-lookaside-lists"></a> ルック アサイド リストの使用

割り当てる必要があります、ドライバーには、ほぼ同じサイズのバッファーが多は必要がある場合、*ルック アサイド リスト*します。 ドライバーは、呼び出してルック アサイド リストを作成します。 [ **WdfLookasideListCreate**](https://msdn.microsoft.com/library/windows/hardware/ff548694)します。 その後、ドライバーできますバッファー ルック アサイド リストから呼び出すことによって取得[ **WdfMemoryCreateFromLookaside**](https://msdn.microsoft.com/library/windows/hardware/ff548709)します。

ドライバーの呼び出しごとに[ **WdfMemoryCreateFromLookaside**](https://msdn.microsoft.com/library/windows/hardware/ff548709)フレームワークは、メモリ オブジェクトを作成し、ルック アサイド リストからバッファーを取得します。 オブジェクトにバッファーを割り当てます。 ドライバーがいつ終了した呼び出し、これらのメモリ オブジェクトのいずれかを使用して[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)、メモリ オブジェクトを削除してルック アサイド リストにバッファー領域を返します。

オペレーティング システムでは、ルック アサイド リストに割り当てられているメモリ リソースを管理します。 ドライバーは、いずれも、ドライバーを呼び出す最初の時間など、使用できない場合にルック アサイド リストからバッファーを要求した場合[ **WdfMemoryCreateFromLookaside**](https://msdn.microsoft.com/library/windows/hardware/ff548709)システムのバッファーを割り当て、割り当てますリストします。 ドライバーを呼び出すと[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734) (とルック アサイド リストにバッファー領域が返されます)、ドライバーは、これをもう一度必要になるまで、システムが一覧に現在割り当てられていないバッファーを保持します。 システムには、必要に応じ、リストのサイズが大きくなります。たとえば、ドライバーの詳細は頻繁にバッファーを要求するには、ルック アサイド リストが大きいが表示されます。 その一方で、ドライバーがすべてを使用しない場合は、システムは、リスト内のバッファーの数を減らす可能性があります。

### <a href="" id="using-mdls"></a> MDLs を使用します。

一部のドライバーでは、記述子の一覧 (MDLs) バッファーを記述するメモリを使用します。 たとえば、ダイレクト メモリ アクセス (DMA) デバイス用のドライバーの MDL を渡す必要があります、 [ **WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099)メソッドでは、このメソッドを呼び出しています。

MDLs を使用するドライバーを呼び出すことによって、受信した I/O 要求のバッファーを表す MDL を取得できます[ **WdfRequestRetrieveInputWdmMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff550016)と[ **WdfRequestRetrieveOutputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550021)します。

ほとんどのフレームワーク ベースのドライバーでは、MDLs は使用しないでください。

### <a href="" id="allocating-local-buffers"></a> ローカル バッファーの割り当てください。

フレームワークに合格しないローカルの内部バッファー領域が必要なドライバーをメモリ バッファーを表すオブジェクトを作成する必要はありません。 ドライバーが呼び出せる[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)内部バッファーを割り当てる。 呼び出す必要がありますが、ドライバーは、バッファーの使用が完了したら、 [ **ExFreePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544593)します。

ただし、ドライバーはローカル バッファーのメモリ オブジェクトを使用することができますも。 呼び出す代わりに、メモリ バッファーを使用する利点[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)、いるフレームワークと自動的に削除メモリ オブジェクトとそのバッファーの各オブジェクトの親オブジェクトが、削除されます。

### <a name="aligning-buffers"></a>バッファーの整列

ドライバーを使用できます、 [ **WDF\_ALIGN\_サイズ\_を**](https://msdn.microsoft.com/library/windows/hardware/ff551217)または[ **WDF\_ALIGN\_サイズ\_ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff551214)指定された配置のオフセットに配置されるバッファー サイズを計算する関数。 この計算は、各バッファーは、アドレスのアラインメント境界で開始する必要がある場合は、ドライバーは、複数の連続したバッファーを割り当てる必要がある場合に便利です。

 

 





