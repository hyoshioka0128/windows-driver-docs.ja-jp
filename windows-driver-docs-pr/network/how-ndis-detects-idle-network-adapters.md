---
title: NDIS がアイドル状態のネットワーク アダプターを検出する方法
description: NDIS がアイドル状態のネットワーク アダプターを検出する方法
ms.assetid: 1FF01B0B-9826-4467-8071-D26CA5E5EF4F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3603e7cf60020b438276247f05a12432a06e20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360823"
---
# <a name="how-ndis-detects-idle-network-adapters"></a>NDIS がアイドル状態のネットワーク アダプターを検出する方法


ミニポート ドライバーが有効にした後、選択的 NDIS を中断し、そのハンドラー関数を登録、NDIS は、次のように、ネットワーク アダプターの I/O アクティビティを監視します。

-   NDIS ミニポート ドライバーを経由して登録される I/O ハンドラー関数の呼び出しの監視、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)と[ **NDIS\_ミニポート\_PNP\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)構造体。 たとえば、ミニポート ドライバーへの呼び出しの監視 NDIS [ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)または[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)をドライバーがパケットの I/O アクティビティに含まれるかどうかを判断します。

-   NDIS の呼び出しを監視することも[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)と[ **NdisDirectOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisdirectoidrequest)プロトコル ドライバーに関連して行われます。

    **注**  NDIS はそれらのオブジェクトの NDIS によって直接処理されない識別子 (OID) 要求を基になるミニポート ドライバーのみを監視します。

     

NDIS は、ネットワーク アダプターがアイドルの場合は、アイドル状態のタイムアウト期間のアダプターのすべてのアクティビティが検出されないことを判断します。 このタイムアウト期間がの値で指定された、  **\*SSIdleTimeout** INF キーワードを標準化します。 このキーワードの詳細については、次を参照してください。 [NDIS セレクティブ サスペンドの標準化された INF キーワード](standardized-inf-keywords-for-ndis-selective-suspend.md)します。

ネットワーク アダプターがアイドル状態になると後、選択的 NDIS 開始は操作を中断します。 この操作で低電力状態に遷移することによって、ネットワーク アダプターが中断されます。

NDIS 開始この選択的ミニポート ドライバーにアイドル状態の通知を発行して、操作を中断します。 NDIS は、ドライバーの呼び出しによって[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)ハンドラー関数。 ミニポート ドライバーはこの通知を処理する方法の詳細については、次を参照してください。 [、NDIS セレクティブ サスペンド アイドル状態の通知の処理](handling-the-ndis-selective-suspend-idle-notification.md)します。

NDIS ドライバーをオーバーレイからネットワーク アダプターへの I/O 要求が発行されることを検出した場合、またはアダプターをウェイク アップ イベントを通知する場合は、NDIS はアイドル状態の通知をキャンセルします。 NDIS ミニポート ドライバーを呼び出すことによっては[ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)ハンドラー関数。

NDIS がアイドル状態の通知をキャンセルする方法の詳細については、次を参照してください。 [NDIS セレクティブ サスペンド アイドル状態通知をキャンセル](canceling-the-ndis-selective-suspend-idle-notification.md)します。

ミニポート ドライバーがアイドル状態の通知を完了する方法の詳細については、次を参照してください。 [NDIS セレクティブ サスペンド アイドル状態通知の完了](completing-the-ndis-selective-suspend-idle-notification.md)します。

 

 





