---
title: マルチポイント呼び出しからのパーティーの削除
description: マルチポイント呼び出しからのパーティーの削除
ms.assetid: db23e911-7c70-432e-992a-fdfdf8cb28ae
keywords:
- パーティ WDK
- マルチポイント呼び出し WDK CoNDIS
- multipoint 呼び出しからのパーティの削除
- multipoint 呼び出しからのパーティの削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6364fd1a2e55d0df092ccd1dfe66503c47197e7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834821"
---
# <a name="dropping-a-party-from-a-multipoint-call"></a>マルチポイント呼び出しからのパーティーの削除





Multipoint 呼び出しのルートとして機能する接続指向クライアントは、最終的に[**NdisClDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty)または[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)を使用して、その呼び出しから各パーティを削除する必要があります。

クライアントは、次の状況で呼び出しからパーティを削除します。

-   **NdisClCloseCall**を使用して multipoint 呼び出しの破棄を開始する前に (クライアントによって開始された[呼び出しを閉じる要求](client-initiated-request-to-close-a-call.md)を参照)、クライアントは、 **NdisClDropParty**を連続して呼び出して、最後のパーティ以外のすべてを削除する必要があります。 クライアントは、 **NdisClCloseCall**を使用して呼び出しから削除する最後のパーティを指定します。

-   リモートパーティの要求が multipoint 呼び出しから削除される (「受信要求」を参照して、 [Multipoint 呼び出しからパーティを削除](incoming-request-to-drop-a-party-from-a-multipoint-call.md)する) と、 [**ProtocolClIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_incoming_drop_party)関数からのクライアントが**NdisClDropParty**を呼び出します。

クライアントが**NdisClDropParty**を呼び出すと、NDIS は、同じ*NDISVCHANDLE*を multipoint VC と共有する call manager または Mcm ドライバーの[**protocolcmdropparty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_drop_party)関数を呼び出します。

次の図は、multipoint 呼び出しからのパーティの削除を要求する呼び出しマネージャーのクライアントを示しています。

![multipoint 呼び出しからのパーティの削除を要求する呼び出しマネージャーのクライアントを示す図](images/cm-18.png)

次の図は、multipoint 呼び出しからのパーティの削除を要求している MCM ドライバーのクライアントを示しています。

![multipoint 呼び出しからのパーティの削除を要求している mcm ドライバーのクライアントを示す図](images/fig1-18.png)

*Protocolcmdropparty*は、ネットワークコントロールデバイスと通信して、既存の multipoint 呼び出しからパーティを削除します。 NDIS は、( **NdisClDropParty**の呼び出しでクライアントに提供される) データを含むバッファーへのポインターを*Protocolcmdropparty*に渡すことができます。 *Protocolcmdropparty*は、接続が切断される前に、そのようなデータをネットワーク経由で送信する必要があります。

*Protocolcmdropparty*は、mcm ドライバーの場合は、呼び出しマネージャーまたは[**NdisMCmDropPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdroppartycomplete)の場合、 [**NdisCmDropPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdroppartycomplete)を使用して同期的に (または可能性がある) 非同期的に完了できます。

**Ndis (M) CmDropPartyComplete**の呼び出しにより、ndis はクライアントの[**protocolcldroppartycomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_drop_party_complete)関数を呼び出します。 クライアントが作成した multipoint VC を破棄する処理を実行している場合、 *Protocolcldroppartycomplete*は、クライアントのアクティブな multipoint vc の残りのパーティのいずれかに対して有効な*Ndispartyhandle*で**NdisClDropParty**を呼び出すことができます. Multipoint VC に存在するパーティが1つだけの場合、クライアントはその*Ndispartyhandle*を**NdisClCloseCall**に渡すことによって、そのパーティを削除する必要があります (「クライアントが開始した[呼び出しを閉じる要求](client-initiated-request-to-close-a-call.md)」を参照してください)。

 

 





