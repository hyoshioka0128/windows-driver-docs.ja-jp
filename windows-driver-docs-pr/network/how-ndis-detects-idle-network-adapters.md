---
title: NDIS がアイドル状態のネットワーク アダプターを検出する方法
description: NDIS がアイドル状態のネットワーク アダプターを検出する方法
ms.assetid: 1FF01B0B-9826-4467-8071-D26CA5E5EF4F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d67604b557349bb0446fc32b4293064b0db9403
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842543"
---
# <a name="how-ndis-detects-idle-network-adapters"></a>NDIS がアイドル状態のネットワーク アダプターを検出する方法


ミニポートドライバーによって NDIS のセレクティブサスペンドが有効になり、そのハンドラー機能が登録されると、NDIS は次のようにネットワークアダプターの i/o アクティビティを監視します。

-   NDIS は、ミニポートドライバーが[**ndis\_ミニポート\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics) [ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)\_ドライバーによって登録する i/o ハンドラー関数への呼び出しを監視します。構成. たとえば、NDIS はミニポートドライバーの[*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)または[*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)の呼び出しを監視して、ドライバーがパケット i/o アクティビティに関係しているかどうかを判断します。

-   また、プロトコルドライバーによって行われた[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)と[**NdisDirectOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdirectoidrequest)の呼び出しも監視します。

    **注**  ndis は、ndis によって直接処理されない、基になるミニポートドライバーに対するオブジェクト識別子 (OID) 要求のみを監視します。

     

NDIS は、アイドルタイムアウト期間のアダプターのアクティビティが検出されない場合に、ネットワークアダプターがアイドル状態であると判断します。 このタイムアウト期間の期間は、 **\*SSIdleTimeout**標準化された INF キーワードの値によって指定されます。 このキーワードの詳細については、「 [NDIS 選択的中断の標準化](standardized-inf-keywords-for-ndis-selective-suspend.md)された INF キーワード」を参照してください。

ネットワークアダプターがアイドル状態になると、NDIS はセレクティブサスペンド操作を開始します。 この操作を実行すると、ネットワークアダプターが低電力状態に移行することによって中断されます。

NDIS は、ミニポートドライバーにアイドル通知を発行することによって、このセレクティブサスペンド操作を開始します。 NDIS は、ドライバーの[*MiniportIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)ハンドラー関数を呼び出すことによってこれを行います。 ミニポートドライバーがこの通知を処理する方法の詳細については、「 [NDIS セレクティブサスペンドアイドル通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)」を参照してください。

NDIS がネットワークアダプターへの i/o 要求が、オーバーレイドライバーから発行されていることを検出した場合、またはアダプターがウェイクアップイベントを通知した場合、NDIS はアイドル状態の通知をキャンセルします。 NDIS は、ミニポートドライバーの[*MiniportCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification)ハンドラー関数を呼び出すことによってこれを行います。

NDIS がアイドル状態の通知をキャンセルする方法の詳細については、「 [ndis の選択的中断のアイドル通知を取り消す](canceling-the-ndis-selective-suspend-idle-notification.md)」を参照してください。

ミニポートドライバーがアイドル状態の通知を完了する方法の詳細については、「 [NDIS の選択的中断のアイドル通知を完了](completing-the-ndis-selective-suspend-idle-notification.md)する」を参照してください。

 

 





