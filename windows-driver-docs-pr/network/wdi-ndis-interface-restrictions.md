---
title: WDI NDIS インターフェイスの制限
description: WDI IHV ミニポート ドライバーでは、すべての NDIS および KMDF によって提供される機能にアクセス権を持ちます。
ms.assetid: 08996045-674B-465D-8880-088320770D2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b61885b461d5c78315be0068a4704a6cd1fbad3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381156"
---
# <a name="wdi-ndis-interface-restrictions"></a>WDI NDIS インターフェイスの制限


WDI IHV ミニポート ドライバーでは、すべての NDIS および KMDF によって提供される機能にアクセス権を持ちます。 IHV ドライバーが可能であれば、オペレーティング システムの残りの部分と通信するため、KMDF プリミティブを使用することをお勧めします。 モデルは、NDIS Api のいずれかの呼び出しから IHV ミニポートを制限していない、IHV ドライバーに呼び出す必要がありますしないように NDIS Api がいくつかは、Microsoft の WLAN コンポーネントによって呼び出されます。

WDI IHV ミニポート ドライバーでは、NDIS インターフェイスには、次の制限を意識する必要があります。

関数 | 制限 | 代わりに 
---|---|--- 
[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver) | Disallowed |  [**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver) 
[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterminiportdriver) | Disallowed |  [**NdisMDeregisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nf-dot11wdi-ndismderegisterwdiminiportdriver) 
[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes) | 許可されていない**MiniportAttributes**型。<br />[**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)<br />[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)<br />[**NDIS\_ミニポート\_アダプター\_ネイティブ\_802\_11\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff565926(v=vs.85)) | なし。 これらは、WDI コマンドを使用して照会されます。 
[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists) | Disallowed | WDI データ パスの受信ハンドラーを受信したパケットを示します。 
[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete) | Disallowed | WDI データ パスは、ハンドラーが送信されたパケットを完了するを送信します。

 





