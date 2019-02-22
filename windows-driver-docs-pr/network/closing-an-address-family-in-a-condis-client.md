---
title: 閉じている CoNDIS クライアントで、アドレス ファミリ
description: 閉じている CoNDIS クライアントで、アドレス ファミリ
ms.assetid: 06e8128a-f3da-48f2-a045-6c4be5f85889
keywords:
- クライアントは、AFs WDK いる CoNDIS を閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1ca0437d033078b39fcdec57387f4774fe7f549
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539128"
---
# <a name="closing-an-address-family-in-a-condis-client"></a>閉じている CoNDIS クライアントで、アドレス ファミリ





AFs を閉じるには、いる CoNDIS クライアントが提供する必要があります、 [ **ProtocolClNotifyCloseAf** ](https://msdn.microsoft.com/library/windows/hardware/ff570234)関数。 NDIS 呼び出し*ProtocolClNotifyCloseAf*スタンドアロン コール マネージャーまたは MCM を呼び出すと、 [ **NdisCmNotifyCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff561680)関数または[ **NdisMCmNotifyCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff563546)関数は、それぞれします。

内から*ProtocolClNotifyCloseAf*クライアントでは、指定の AF の終了が完了すると、または、NDIS 返します\_状態\_PENDING と呼び出し、 [ **NdisClNotifyCloseAddressFamilyComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561638)操作を完了する関数。 クライアントの呼び出し後**NdisClNotifyCloseAddressFamilyComplete**、NDIS 呼び出し、 [ **ProtocolCmNotifyCloseAfComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570248)コール マネージャーに通知する関数をクライアントでは、AF が閉じられます。

AF を閉じるには、クライアントが必要です。

1.  クライアントに multipoint のアクティブな接続がある場合は、呼び出し、 [ **NdisClDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff561629)単一のパーティのみが各 multipoint 接続 (VC) でアクティブなままになるまでに必要な回数として機能します。

2.  呼び出す、 [ **NdisClCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561627)閉じますすべての呼び出しに必要な回数がまだ開いているとおりに機能し、は、アドレス ファミリに関連付けられます。

3.  呼び出す、 [ **NdisClDeregisterSap** ](https://msdn.microsoft.com/library/windows/hardware/ff561628)すべてのサービスへのアクセス ポイント (Sap)、クライアントが、コール マネージャーに登録されている登録の解除に必要な回数として機能します。

4.  呼び出す、 [ **NdisClCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff561626) AF を閉じます。

 

 





