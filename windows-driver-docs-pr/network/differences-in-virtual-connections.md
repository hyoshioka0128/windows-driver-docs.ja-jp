---
title: 仮想接続の違い
description: 仮想接続の違い
ms.assetid: 6e705f31-eec7-4b9c-a46f-ff7641d224c2
keywords:
- 仮想接続 WDK いる CoNDIS、マネージャーを呼び出すと MCM のドライバー
- シグナリングの VCs WDK いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bda82d768f2e8c008e5dd677e67d705cbd4e57ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579163"
---
# <a name="differences-in-virtual-connections"></a>仮想接続の違い





コール マネージャーを使用して*VCs のシグナリング*とスイッチなどのネットワーク エンティティの間のシグナリング メッセージを送受信します。 コール マネージャーのシグナリング VCs は、NDIS に表示されます。 コール マネージャーは、作成、アクティブ化、非アクティブ化、および NDIS への呼び出しですべての VCs を削除する必要があります。 ただし、MCM ドライバーのシグナリングの VCs は、NDIS を不透明なは。 MCM ドライバーはいない作成、アクティブ化、非アクティブ化、および削除 NDIS への呼び出しの VCs をシグナル通知。 代わりに、MCM、ドライバーはこのような操作を内部的に実行します。 MCM、ドライバーは、クライアントのデータ送信または受信に使用される VCs で操作を実行する NDIS を呼び出す必要があります。 NDIS する必要がありますの追跡クライアント VCs ためにです。

MCM のドライバーがコール マネージャーとミニポート ドライバーの両方であるため、特定の接続指向の機能は冗長です。 具体的には、 [ **MiniportCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559354)と[ **MiniportCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559358)が冗長になると、MCM ドライバーで提供されないためです。 VC 操作は、によって処理されます。

-   MCM ドライバーの[ **ProtocolCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff570252)と[ **ProtocolCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff570253)関数の作成または削除のクライアントが要求したときに、VC します。

-   [**NdisMCmCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562812)と[ **NdisMCmDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562819) MCM ドライバーが作成または VC を削除します。

-   [**NdisMCmActivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562792)と[ **NdisCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561657) MCM ドライバーがアクティブにまたは VC を非アクティブ化します。

MCM にドライバーを指定する必要があります、 [ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)クライアントでの照会や設定は、ミニポート ドライバー情報を使用するための関数と[ **MiniportCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff559365)クライアントから送信操作を処理する関数。

 

 





