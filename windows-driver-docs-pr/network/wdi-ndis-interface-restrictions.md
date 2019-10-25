---
title: WDI NDIS インターフェイスの制限
description: WDI IHV ミニポートドライバーは、NDIS と KMDF によって提供されるすべての機能にアクセスできます。
ms.assetid: 08996045-674B-465D-8880-088320770D2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18a45fbe5e3c2229e66039f1767ddb1de9464093
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842915"
---
# <a name="wdi-ndis-interface-restrictions"></a>WDI NDIS インターフェイスの制限


WDI IHV ミニポートドライバーは、NDIS と KMDF によって提供されるすべての機能にアクセスできます。 可能な場合は、オペレーティングシステムの他の部分と通信するために、IHV ドライバーで KMDF プリミティブを使用することをお勧めします。 このモデルでは、IHV ミニポートを NDIS Api の呼び出しから制限していませんが、一部の NDIS Api は Microsoft WLAN コンポーネントによって呼び出されます。そのため、IHV ドライバーはこれらを呼び出すことができません。

WDI IHV ミニポートドライバーは、NDIS インターフェイスに関して次の制限を認識している必要があります。

関数 | 制限 | ソリューション 
---|---|--- 
[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) | Disallowed |  [**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver) 
[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver) | Disallowed |  [**NdisMDeregisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismderegisterwdiminiportdriver) 
[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) | **Miniportattributes**型では許可されません。<br />[**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)<br />[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)<br />[**NDIS\_ミニポート\_アダプター\_ネイティブ\_802\_11\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff565926(v=vs.85)) | なし。 これらは、WDI コマンドを使用して照会されます。 
[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) | Disallowed | 受信パケットを示す WDI data path 受信ハンドラー。 
[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) | Disallowed | 送信されたパケットを完了するための WDI データパス送信ハンドラー。

 





