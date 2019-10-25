---
title: NDIS ポート状態表示の処理
description: NDIS ポート状態表示の処理
ms.assetid: ba3794de-b17e-4878-a65e-6c9f5f8ebbbc
keywords:
- ポート WDK NDIS、状態のインジケーター
- NDIS ポート WDK、状態のインジケーター
- WDK ネットワーク、NDIS ポートを示す状態
- ポートの状態 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b20cbb2a4303b18dc11cf26929c3a132a6bb702e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842582"
---
# <a name="handling-ndis-ports-status-indications"></a>NDIS ポート状態表示の処理





NDIS ポートがステータス表示のソースである場合、ミニポートドライバーでは、ソースポートを指定するために、 [**ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造**のポート番号メンバーを**使用する必要があります。 ミニポートドライバーは、非アクティブなポートの状態を示しません。

ミニポートドライバーでは、ndis [ **\_ステータス\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)の状態の表示を使用して、ndis ポートの状態の変化を示す必要があります。 この状態を示すために、ミニポートドライバーは、 [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体**のポート番号メンバーに**ポート番号を設定する必要があります。 NDIS\_ステータス\_表示構造体の**Statusbuffer**メンバーには、 [**ndis\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)構造体へのポインターが含まれています。

 

 





