---
title: 関連付け後の操作を停止しています
description: 関連付け後の操作を停止しています
ms.assetid: 28400cad-1e77-4bcd-9b9a-103df5f06d10
keywords:
- アソシエーション後の操作 WDK ネイティブ 802.11 IHV 拡張 DLL
- 関連付け後の操作を停止しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dd8c0029a4654a4c351784346d040b93998986e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841818"
---
# <a name="stopping-a-post-association-operation"></a>関連付け後の操作を停止しています




 

オペレーティングシステムは、次のいずれかが発生するたびに[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate) IHV ハンドラー関数を呼び出すことによって、関連付け後の操作を終了します。

-   ワイヤレス LAN (WLAN) アダプターは、AP を使用した関連付け操作を完了します。 この状況では、アダプターを管理するネイティブ802.11 ステーションによって、メディア固有の[NDIS\_ステータス\_DOT11\_関連付け](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-disassociation)が示されます。 関連付け操作の詳細については、「[関連付け操作](disassociation-operations.md)」を参照してください。

-   WLAN アダプターが無効になっているか、削除されています。 この場合、オペレーティングシステムは、 [*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)関数を呼び出す前に、 [*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)関数を呼び出します。

オペレーティングシステムは、 [*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)関数を呼び出して、AP との関連付け用に作成されたデータポートがダウンしていることを IHV 拡張 DLL に通知します。 [**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)の呼び出しによって、DLL が関連付け後の操作を完了したかどうかに関係なく、オペレーティングシステムはこの関数を呼び出します。

[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)が呼び出されると、IHV 拡張機能は、データポートに割り当てられているすべてのリソースを解放する必要があります。 [**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)の呼び出しで関連付け後の操作が完了しなかった場合、IHV 拡張 DLL は内部で操作をキャンセルする必要がありますが、 **Dot11ExtPostAssociateCompletion**を呼び出すことはできません。

 

 





