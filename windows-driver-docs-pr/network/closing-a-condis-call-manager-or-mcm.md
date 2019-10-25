---
title: CoNDIS コール マネージャーまたは MCM を閉じる
description: CoNDIS コール マネージャーまたは MCM を閉じる
ms.assetid: 6ef64e4c-eec4-4477-a06c-f80e21d5b1c7
keywords:
- 呼び出しマネージャー WDK ネットワーク、CoNDIS
- MCMs WDK ネットワーク、終了
- ミニポート呼び出しマネージャー WDK ネットワーク、終了
- 呼び出しマネージャーを閉じる
- ミニポートコールマネージャーを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ffbf6b59ce15212aa70272270f2107d0fe004ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838199"
---
# <a name="closing-a-condis-call-manager-or-mcm"></a>CoNDIS コール マネージャーまたは MCM を閉じる





スタンドアロンコールマネージャーが、基になるミニポートアダプターからバインド解除されている場合、呼び出しマネージャーは、関連付けられている AF を閉じる必要がある、影響を受けるすべての CoNDIS クライアントに通知する必要があります。 各クライアントに通知するために、NDIS スタンドアロンコールマネージャーは[**NdisCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmnotifycloseaddressfamily)関数を呼び出します。

MCM が管理する CoNDIS ミニポートアダプターが停止している場合、MCM は、関連付けられている AF を閉じる必要があることを、影響を受けるすべてのクライアントに通知する必要があります。 各クライアントに通知するために、MCMs は[**NdisMCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmnotifycloseaddressfamily)関数を呼び出します。

スタンドアロンの呼び出しマネージャーまたは MCM が**NdisCmNotifyCloseAddressFamily**または**NdisMCmNotifyCloseAddressFamily**を呼び出す場合、NDIS は、[**この関数に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_notify_close_af)関連付けられている**NdisCmNotifyCloseAddressFamily**または**NdisMCmNotifyCloseAddressFamily**の*NdisAfHandle*パラメーターのハンドル。 この呼び出しは、AF を閉じるようにクライアントに通知します。 **NdisCmNotifyCloseAddressFamily**または**NdisMCmNotifyCloseAddressFamily**が NDIS\_STATUS\_PENDING を返した場合、ndis は close が呼び出されると、呼び出しマネージャーの[**Protocolcmnotifycloseafcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_notify_close_af_complete)関数を呼び出します。通知操作が完了しました。

Condis クライアントでアドレスファミリを終了する方法の詳細については、「 [condis アドレスファミリを切断する](closing-an-address-family-in-a-condis-client.md)」を参照してください。

 

 





