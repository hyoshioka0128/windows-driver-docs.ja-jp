---
title: 関連付け後の操作の停止
description: 関連付け後の操作の停止
ms.assetid: 28400cad-1e77-4bcd-9b9a-103df5f06d10
keywords:
- 後の関連付け操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- 後の関連付け操作を停止しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7094c852c31a918cca6bf6c1152b2a4a51022bad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383583"
---
# <a name="stopping-a-post-association-operation"></a>関連付け後の操作の停止




 

オペレーティング システムが呼び出すことによって、後の関連付け操作を終了、 [ *Dot11ExtIhvStopPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)次のいずれかが発生するたびに、IHV ハンドラー関数。

-   ワイヤレス LAN (WLAN) アダプターは、AP との関連付け解除操作を完了します。 このような状況で、アダプターを管理するには、ネイティブの 802.11 ステーションは、メディア固有[NDIS\_状態\_DOT11\_戻せません](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-disassociation)を示す値。 関連付け解除操作の詳細については、次を参照してください。[関連付け解除操作](disassociation-operations.md)します。

-   WLAN アダプターが無効にしたり、削除します。 このような状況でオペレーティング システムの呼び出し、 [ *Dot11ExtIhvStopPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)関数を呼び出す前に、 [ *Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)関数。

オペレーティング システムの呼び出し、 [ *Dot11ExtIhvStopPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate) AP との関連付けの作成、データ ポートがダウンした IHV 拡張 DLL に通知します。 オペレーティング システムが DLL を呼び出すことによって、後の関連付け操作が完了したかどうかに関係なく、この関数を呼び出す[ **Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)します。

ときに[ *Dot11ExtIhvStopPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)が呼び出されると、IHV 拡張する必要がありますリリースのすべてのデータ ポートに割り当てられたリソース。 後の関連付け操作がへの呼び出しで完了していないかどうかは[ **Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)、IHV 拡張機能の DLL は、内部的には、操作を取り消す必要がありますを呼び出してはならない**Dot11ExtPostAssociateCompletion**します。

 

 





