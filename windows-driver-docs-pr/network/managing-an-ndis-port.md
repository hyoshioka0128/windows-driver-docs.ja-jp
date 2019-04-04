---
title: NDIS ポートの管理
description: NDIS ポートの管理
ms.assetid: 08bb6623-aa9f-483e-a3cd-7dea676f3478
keywords:
- ポート WDK NDIS、管理します。
- NDIS、WDK のポートを管理します。
- ポートの状態が WDK NDIS
- ポート番号の WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 925ed4de88ae2bf0a0d9420de116b81da09bbadb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571124"
---
# <a name="managing-an-ndis-port"></a>NDIS ポートの管理





目的の NDIS ドライバーとユーザー モード アプリケーションでは、NDIS ポートを管理できます。 NDIS は、ポートを管理するためにサービスを提供します。

NDIS は、関連付けられている状態のインジケーターと PnP イベントを発行して、目的の NDIS ドライバーとポートの状態変化のユーザー モード アプリケーションを通知します。

送信操作のターゲット ポートまたは受信を示す値を発信元ポート、送信し、受信機能に渡されるポート番号を識別します。 同様に、関連付けられた構造内のポート番号は、状態インジケーター、OID 要求、および PnP イベントのポートを識別します。 ポート番号の詳細については、[NDIS ポート概要](overview-of-ndis-ports.md)を参照してください。

NDIS ポートを管理するは、以下の構造体は、ポート番号を含めます。

<a href="" id="ndis-oid-request"></a>[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)  
OID 要求をについて説明します。

<a href="" id="ndis-status-indication"></a>[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)  
NDIS 状態インジケーターをについて説明します。

<a href="" id="net-pnp-event-notification"></a>[**NET\_PNP\_EVENT\_NOTIFICATION**](https://msdn.microsoft.com/library/windows/hardware/ff568752)  
PnP イベント通知をについて説明します。

このセクションの内容:

[NDIS ポートの送信し、受信操作](ndis-port-send-and-receive-operations.md)

[NDIS ポート OID 要求](ndis-port-oid-requests.md)

[処理の NDIS ポートの状態インジケーター](handling-ndis-ports-status-indications.md)

[処理の NDIS ポート PnP イベント通知](handling-ndis-ports-pnp-event-notifications.md)

 

 





