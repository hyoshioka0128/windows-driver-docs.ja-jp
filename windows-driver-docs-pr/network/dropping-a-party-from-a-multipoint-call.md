---
title: マルチポイント呼び出しからのパーティーの削除
description: マルチポイント呼び出しからのパーティーの削除
ms.assetid: db23e911-7c70-432e-992a-fdfdf8cb28ae
keywords:
- パーティ WDK いる CoNDIS
- multipoint 呼び出し WDK いる CoNDIS
- multipoint 呼び出しからパーティを削除しています
- multipoint 呼び出しからパーティを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91a5c3775dad289a577d688db78ee22f2de438d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372712"
---
# <a name="dropping-a-party-from-a-multipoint-call"></a>マルチポイント呼び出しからのパーティーの削除





Multipoint の呼び出しのルートでは、その呼び出しから各パーティを削除する必要があります最終的には、接続指向のクライアント[ **NdisClDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff561629)または[ **NdisClCloseCall**](https://msdn.microsoft.com/library/windows/hardware/ff561627).

クライアントは、次の状況での呼び出しからパーティを削除します。

-   Multipoint 呼び出しの下、終了処理を開始する前に**NdisClCloseCall**(を参照してください[Client-Initiated の要求の呼び出しを閉じます](client-initiated-request-to-close-a-call.md))、クライアントがへの連続呼び出しで最後のパーティがすべて削除する必要があります**NdisClDropParty**します。 クライアントの呼び出しからを削除する最後のパーティが指定**NdisClCloseCall**します。

-   Multipoint 呼び出しから削除するリモート側の要求に応答 (を参照してください[Multipoint 呼び出しからパーティを削除する受信要求](incoming-request-to-drop-a-party-from-a-multipoint-call.md))、クライアントからその[ **ProtocolClIncomingDropParty**](https://msdn.microsoft.com/library/windows/hardware/ff570231)関数では、呼び出し**NdisClDropParty**します。

クライアントの呼び出し**NdisClDropParty** NDIS を呼び出すと、 [ **ProtocolCmDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff570244)コール マネージャーまたは同じ共有 MCM ドライバーの機能は*NdisVcHandle* multipoint VC にします。

次の図は、multipoint 呼び出しからパーティを削除する要求マネージャーの呼び出しのクライアントを示します。

![multipoint 呼び出しからパーティを削除する要求のコール マネージャーのクライアントを示す図](images/cm-18.png)

次の図は、multipoint 呼び出しからパーティを削除するように要求して、MCM ドライバーのクライアントを示しています。

![multipoint 呼び出しからパーティを削除するように要求して、mcm ドライバーのクライアントを示す図](images/fig1-18.png)

*ProtocolCmDropParty*は既存の multipoint 呼び出しからパーティを削除するネットワーク デバイスの制御と通信します。 NDIS を渡すことができます*ProtocolCmDropParty*データを格納するバッファーへのポインター (への呼び出しでクライアントに渡される**NdisClDropParty**)。 *ProtocolCmDropParty*接続が削除される前に、ネットワーク経由でこのようなデータを送信する必要があります。

*ProtocolCmDropParty*で同期的にまたはより可能性があります、非同期的に完了できる[ **NdisCmDropPartyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561674)の場合は、コール マネージャーまたは[ **NdisMCmDropPartyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563543)MCM、ドライバーの場合。

呼び出し**Ndis (M) CmDropPartyComplete**を呼び出すクライアントの NDIS と[ **ProtocolClDropPartyComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570227)関数。 クライアントが作成されると、it の multipoint VC 破棄処理中の場合*ProtocolClDropPartyComplete*呼び出すことができます**NdisClDropParty**いずれかで有効な*NdisPartyHandle*multipoint vc のアクティブなクライアントの残りのパーティのいずれかにします。 クライアントが渡すことによってそのパーティを削除する必要があります 1 つのパーティは、その multipoint VC 上に残っている場合のみその*NdisPartyHandle*に**NdisClCloseCall**(を参照してください[Client-Initiated の要求をの呼び出しを閉じます](client-initiated-request-to-close-a-call.md)).

 

 





