---
title: CoNDIS クライアントでアドレス ファミリを閉じる
description: CoNDIS クライアントでアドレス ファミリを閉じる
ms.assetid: 06e8128a-f3da-48f2-a045-6c4be5f85889
keywords:
- クライアントが終了した AFs WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a490fdb618858ba06a32cccce63e2a3d7bc4da6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838197"
---
# <a name="closing-an-address-family-in-a-condis-client"></a>CoNDIS クライアントでアドレス ファミリを閉じる





AFs を閉じるには、CoNDIS クライアントが[**Protocolclnotifycloseaf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_notify_close_af)関数を提供する必要があります。 NDIS は、 [**NdisCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmnotifycloseaddressfamily)関数または[**NdisMCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmnotifycloseaddressfamily)関数をそれぞれ呼び出して、スタンドアロンの呼び出しマネージャーまたは mcm が呼び出すときに、 *protocolclnotifycloseaf*を呼び出します。

*Protocolclnotifycloseaf*内から、クライアントは指定された AF を終了します。または、NDIS\_STATUS\_PENDING を返し、 [**NdisClNotifyCloseAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclnotifycloseaddressfamilycomplete)関数を呼び出して操作を完了します。 クライアントが**NdisClNotifyCloseAddressFamilyComplete**を呼び出すと、NDIS は[**Protocolcmnotifycloseafcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_notify_close_af_complete)関数を呼び出して、クライアントが AF を閉じたことを呼び出しマネージャーに通知します。

AF を閉じるには、クライアントは次のことを行う必要があります。

1.  クライアントにアクティブな multipoint 接続がある場合は、各 multipoint 仮想接続 (VC) で1つのパーティだけがアクティブなままになるまで、必要な回数だけ[**NdisClDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty)関数を呼び出します。

2.  [**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)関数は、開いたままで、アドレスファミリに関連付けられているすべての呼び出しを閉じるために必要な回数だけ呼び出します。

3.  クライアントが呼び出しマネージャーに登録したすべてのサービスアクセスポイント (Sap) の登録を解除するには、必要な回数だけ[**NdisClDeregisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclderegistersap)関数を呼び出します。

4.  [**NdisClCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily)関数を呼び出して、AF を閉じます。

 

 





