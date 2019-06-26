---
title: 802.11 WLAN アダプターのリセット
description: 802.11 WLAN アダプターのリセット
ms.assetid: 1f993977-b4a1-42ec-8de3-2f4855db93a7
keywords:
- WDK 802.11 の WLAN のアダプターをリセットします。
- WLAN アダプター、WDK をリセットします。
- WLAN のアダプターをリセットします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb5e4871fd94b36c4ecd83fc79d04fd66a7ba4b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379305"
---
# <a name="80211-wlan-adapter-reset"></a>802.11 WLAN アダプターのリセット




 

オペレーティング システムの呼び出し[ *Dot11ExtIhvAdapterReset* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)たびにする必要が生じたワイヤレス LAN (WLAN) アダプターを初期化済み状態に復元します。 オペレーティング システムは、次のイベントのいずれかが発生するたびに、この関数を呼び出します。

-   WLAN アダプターは、切断操作を実行します。 この操作の詳細については、次を参照してください。[切断操作](disconnection-operations.md)します。

-   オペレーティング システムのセットに要求を介して、アダプターを管理するネイティブの 802.11 ミニポート ドライバーをリセットする[OID\_DOT11\_リセット\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request)します。

ときに[ *Dot11ExtIhvAdapterReset* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)が呼び出されると、IHV 拡張機能の DLL は次のガイドラインを従う必要があります。

-   IHV 拡張機能の DLL が同じ状態にした後にその状態を復元する必要があります、 [ *Dot11ExtIhvInitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter)関数が呼び出されました。 後であった同じ状態にこれらの設定を復元する必要があります、DLL には、WLAN アダプターで独自の設定が構成されている場合、 *Dot11ExtIhvInitAdapter*が呼び出されました。

-   IHV 拡張機能の DLL を呼び出すことによって開始された保留中の関連付け前操作がある場合、 [ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) IHV ハンドラー関数の場合は、DLL を呼び出す必要があります[**Dot11ExtPreAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)操作をキャンセルします。 このような状況では、DLL、設定、 *dwWin32Error*パラメーターの**Dot11ExtPreAssociateCompletion**エラー\_キャンセルします。

    前の関連付け操作の詳細については、次を参照してください。[関連付け前操作](pre-association-operations.md)します。

-   DLL を呼び出すことによって開始された保留中の後の関連付け操作がある場合、 [ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) IHV ハンドラー関数の場合は、DLL を呼び出す必要があります[ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)操作をキャンセルします。 このような状況では、DLL、設定、 *dwWin32Error*パラメーターの**Dot11ExtPostAssociateCompletion**エラー\_キャンセルします。

    詳細については、後の関連付け操作は、次を参照してください。[後関連付け操作](post-association-operations.md)します。

 

 





