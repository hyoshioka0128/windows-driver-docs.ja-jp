---
title: WDI NDIS インターフェイスの制限
description: WDI IHV ミニポート ドライバーでは、すべての NDIS および KMDF によって提供される機能にアクセス権を持ちます。
ms.assetid: 08996045-674B-465D-8880-088320770D2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f81c75d19a1f3a45773116f0f78d1da1617d153
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528115"
---
# <a name="wdi-ndis-interface-restrictions"></a>WDI NDIS インターフェイスの制限


WDI IHV ミニポート ドライバーでは、すべての NDIS および KMDF によって提供される機能にアクセス権を持ちます。 IHV ドライバーが可能であれば、オペレーティング システムの残りの部分と通信するため、KMDF プリミティブを使用することをお勧めします。 モデルは、NDIS Api のいずれかの呼び出しから IHV ミニポートを制限していない、IHV ドライバーに呼び出す必要がありますしないように NDIS Api がいくつかは、Microsoft の WLAN コンポーネントによって呼び出されます。

WDI IHV ミニポート ドライバーでは、NDIS インターフェイスには、次の制限を意識する必要があります。

関数 | 制限 | 代わりに 
---|---|--- 
[**NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654) | Disallowed |  [**NdisMRegisterWdiMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/mt297596) 
[**NdisMDeregisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563578) | Disallowed |  [**NdisMDeregisterWdiMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/mt297595) 
[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672) | 許可されていない**MiniportAttributes**型。<br />[**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)<br />[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)<br />[**NDIS\_ミニポート\_アダプター\_ネイティブ\_802\_11\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565926) | なし。 これらは、WDI コマンドを使用して照会されます。 
[**NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598) | Disallowed | WDI データ パスの受信ハンドラーを受信したパケットを示します。 
[**NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668) | Disallowed | WDI データ パスは、ハンドラーが送信されたパケットを完了するを送信します。

 





