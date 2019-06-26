---
title: NDIS ポート状態表示の処理
description: NDIS ポート状態表示の処理
ms.assetid: ba3794de-b17e-4878-a65e-6c9f5f8ebbbc
keywords:
- WDK NDIS、状態インジケーターをポートします。
- NDIS ポート WDK、状態インジケーター
- 状態インジケーターの WDK ネットワー キング、NDIS ポート
- ポートの状態が WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 187f81134460364eb5119f7cafb8686f6b213f69
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379806"
---
# <a name="handling-ndis-ports-status-indications"></a>NDIS ポート状態表示の処理





ミニポート ドライバーを使用する必要があります、NDIS ポートが状態表示のソースの場合は、 **PortNumber**内のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)ソース ポートを指定する構造体。 ミニポート ドライバーは、決して非アクティブなポートの状態を示します。

ミニポート ドライバーを使用する必要があります、 [ **NDIS\_状態\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state) NDIS ポートの状態の変化を示すステータスを示す値。 この状態表示のミニポート ドライバーでポート番号を設定する必要があります、 **PortNumber**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体。 **StatusBuffer**の NDIS メンバー\_状態\_を示す値構造体にはへのポインターが含まれています、 [ **NDIS\_ポート\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)構造体。

 

 





