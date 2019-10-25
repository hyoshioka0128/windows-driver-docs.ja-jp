---
title: VC の削除
description: VC の削除
ms.assetid: 6e49fb69-0b22-4f52-9b6d-661e818c1758
keywords:
- 仮想接続 WDK の削除、削除
- 仮想接続を削除しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63ec0604c350817f6eafaa735a7a07682d11c70e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838179"
---
# <a name="deleting-a-vc"></a>VC の削除





仮想回線 (VC) の作成を開始した接続指向クライアント、コールマネージャー、または MCM ドライバーのみが、その VC の削除を開始できます。 そのため、クライアントは、発信呼び出し用に以前に作成した VC を削除します。呼び出しマネージャーまたは MCM ドライバーは、ネットワーク経由の着信呼び出し用に以前に作成した vc を削除します。ネットワーク経由のメッセージ。 (MCM ドライバーは、通知メッセージを交換するために作成された VC を削除するために NDIS を呼び出しません。 MCM ドライバーは、NDIS に対して非透過的な内部操作で VC を削除します)。

接続指向クライアントまたは呼び出しマネージャーによって、 [**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)を使用した VC の削除が開始されます。

次の図は、VC の削除を開始する呼び出しマネージャーのクライアントを示しています。

![vc の削除を開始するコールマネージャーのクライアントを示す図](images/cm-09.png)

次の図は、VC の削除を開始する MCM ドライバーのクライアントを示しています。

![vc の削除を開始する mcm ドライバーのクライアントを示す図](images/fig1-09.png)

次の図は、VC の削除を開始する呼び出しマネージャーを示しています。

![vc の削除を開始するコールマネージャーを示す図](images/cm-10.png)

クライアントまたは呼び出しマネージャーが**NdisCoDeleteVc**を呼び出したとき、または mcm ドライバーが**NdisMCmDeleteVc**を呼び出したときに、指定された vc に未処理の呼び出しがないことと、vc が既に[非アクティブ](deactivating-a-vc.md)化されている必要があります。 これらの要件を満たすために、次の条件が満たされていることを意味します。

-   クライアントは、指定された*NdisVcHandle*で既に[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)を呼び出しましたが、その[クローズ呼び出し要求](client-initiated-request-to-close-a-call.md)が正常に完了しました。

-   呼び出しマネージャーが既に[**NdisCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc)を呼び出しているか、mcm ドライバーが既に指定された*NdisVcHandle*を使用して[**NdisMCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc)を呼び出していて、非アクティブ化要求が正常に完了しました ([への受信要求を参照)。呼び出しを終了](incoming-request-to-close-a-call.md)します)。

クライアントまたはコールマネージャーの**NdisCoDeleteVc**への呼び出しにより、NDIS は、基になるミニポートドライバーの[**MiniportCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_delete_vc)関数と、呼び出し元が使用するクライアントまたは呼び出しマネージャーの[**ProtocolCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_delete_vc)関数の両方を呼び出します。*NdisVcHandle*を共有します (前の3つの図を参照)。

*MiniportCoDeleteVc*は、vc に割り当てられたすべてのリソースと、vc のミニポートドライバーのコンテキストを解放します。 *ProtocolCoDeleteVc*は、クライアントまたは呼び出しマネージャーが VC の操作を実行したり、状態を追跡したりするために使用したすべてのリソースを解放します。 *MiniportCoDeleteVc*と*ProtocolCoDeleteVc*はどちらも、NDIS\_\_STATUS を返すことができない同期関数です。

MCM ドライバーは、 [**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc)を使用した VC の削除を開始します (次の図を参照してください)。

![vc の削除を開始する mcm ドライバーを示す図 ](images/fig1-10.png)

MCM ドライバーの**NdisMCmDeleteVc**への呼び出しにより、NDIS は mcm ドライバーが*NdisVcHandle*を共有するクライアントの[**ProtocolCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_delete_vc)関数を呼び出します。

**NdisCoDeleteVc**または**NdisMCmDeleteVc**が制御を返すと、 *NdisVcHandle*は無効になります。

 

 





