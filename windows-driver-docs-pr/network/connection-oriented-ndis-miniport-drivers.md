---
title: 接続指向の NDIS ミニポート ドライバー
description: 接続指向の NDIS ミニポート ドライバー
ms.assetid: 58f9bed1-274c-4f60-87cd-f0b44871eb60
keywords:
- ミニポート ドライバー WDK ネットワークの種類
- NDIS ミニポート ドライバー WDK、種類
- 接続指向のドライバー WDK ネットワー キング、ミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4727d82145ea9936b1c0064f28dd58342b3ab93e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532576"
---
# <a name="connection-oriented-ndis-miniport-drivers"></a>接続指向の NDIS ミニポート ドライバー





A*接続指向のミニポート ドライバー*接続指向のメディアの 1 つまたは複数のミニポート アダプターを制御します。 接続指向のミニポート ドライバーを逆シリアル化する必要があります。 逆シリアル化されたドライバーの詳細については、次を参照してください。 [NDIS ミニポート ドライバーの逆シリアル化](deserialized-ndis-miniport-drivers.md)します。

接続指向のミニポート ドライバーでは、接続指向プロトコル ドライバー (クライアントの接続指向とコール マネージャー) と NIC のハードウェア (物理ミニポート アダプターなど) 間のインターフェイスを提供します。 接続指向のミニポート ドライバーによって実行された接続指向の操作の概要については、次を参照してください。 [Connection-Oriented ミニポート ドライバーによって操作が実行される](connection-oriented-operations-performed-by-miniport-drivers.md)します。

接続指向のミニポート ドライバーは、次を登録する必要があります*MiniportXxx*接続指向の操作に固有の機能。

-   [**MiniportCoCreateVc**](https://msdn.microsoft.com/library/windows/hardware/ff559354)

-   [**MiniportCoDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff559358)

-   [**MiniportCoActivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff559351)

-   [**MiniportCoDeactivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff559356)

-   [**MiniportCoSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff559365)

-   [**MiniportCoOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559362)

これらの関数の登録の詳細については、次を参照してください。 [ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)します。

 

 





