---
title: 共有メモリ リソースの割り当て
description: 共有メモリ リソースの割り当て
ms.assetid: cf030a0f-1202-4d10-b9a1-58d031345678
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45b2121785fba430e9c5c0321c7e54c4484e3e65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561062"
---
# <a name="shared-memory-resource-allocation"></a>共有メモリ リソースの割り当て





ミニポート ドライバーを呼び出して VM キューの共有メモリ リソースを割り当てる、 [ **NdisAllocateSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561616)関数。 受信したときに、ミニポート ドライバーが共有メモリを割り当てますなど、 [OID\_受信\_フィルター\_キュー\_割り当て\_完了](https://msdn.microsoft.com/library/windows/hardware/ff569793)OID。 また、ミニポート ドライバーは、ネットワーク アダプターの初期化中に、既定のキューの共有メモリを割り当てることができます。 キューの割り当てに関する詳細については、次を参照してください。 [VM キューを割り当てる](allocating-a-vm-queue.md)します。

ミニポート ドライバーは、キューが解放されるまで、キューの多くのメモリを割り当てることができます。 キューを解放する方法の詳細については、次を参照してください。 [VM キューの解放](freeing-a-vm-queue.md)します。

[ **NDIS\_SHARED\_メモリ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567303)構造体は、共有メモリの割り当て要求の共有メモリ パラメーターを指定します。 ミニポート ドライバーは、この構造体を渡す、 [ **NdisAllocateSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561616)関数。 NDIS は、この構造体を渡します、 [ **NetAllocateSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff568327)関数 (つまり、割り当て\_共有\_メモリ\_ハンドラー エントリ ポイント)。

ミニポート ドライバーでは、共有メモリを割り当て、ときに、次を指定します。

-   キューの識別子です。

-   共有メモリ長。

-   共有メモリの使用方法。 たとえば、ミニポート ドライバーを指定します**NdisSharedMemoryUsageReceive**共有メモリの受信バッファーに使用する場合。

場合は、NDIS\_SHARED\_メモリ最適化\_パラメーター\_サイズのフラグが設定されていない、**フラグ**メンバー、共有メモリに含まれているスキャッター/ギャザー リストで指定できます連続しないメモリ。

[ **NDIS\_SHARED\_メモリ\_使用状況**](https://msdn.microsoft.com/library/windows/hardware/ff567309)列挙体で指定する方法の共有メモリが使用します。 NDIS\_SHARED\_メモリ\_で使用状況の列挙が使用される、 [ **NDIS\_SHARED\_メモリ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567303)と[ **NDIS\_散布図\_収集\_一覧\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567292)構造体。 共有メモリについては、VMQ のパラメーターは受信データ バッファーを参照してください[受信バッファー内の共有メモリ](shared-memory-in-receive-buffers.md)します。

[ **NdisAllocateSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561616)関数が呼び出し元に、次を提供します。

-   割り当てられたメモリの仮想アドレス。

-   スキャッター/ギャザーの一覧です。

-   共有メモリ ハンドルのインジケーターが表示されます。

-   割り当てハンドルの後で、メモリを識別するために使用します。

ミニポート ドライバーの呼び出し、 [ **NdisFreeSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562601)キュー用の共有メモリを解放します。 コンテキストで共有メモリを解放する場合は、ミニポート ドライバーでは、既定以外のキューの共有メモリを割り当て、 [OID\_受信\_フィルター\_FREE\_キュー](https://msdn.microsoft.com/library/windows/hardware/ff569789)間に OIDキューを解放します。 無料のミニポート ドライバーのコンテキストで、既定のキューに割り当てられるメモリの共有、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)関数。

 

 





