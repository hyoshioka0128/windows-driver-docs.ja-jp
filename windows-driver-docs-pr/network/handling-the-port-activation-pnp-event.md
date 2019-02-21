---
title: ポート アクティベーション PnP イベントを処理します。
description: ポート アクティベーション PnP イベントを処理します。
ms.assetid: 433018bf-daf5-4ea1-be3f-63349558f6b7
keywords:
- WDK NDIS、PnP イベント通知をポートします。
- NDIS ポート WDK、PnP イベント通知
- PnP イベント通知 WDK NDIS ポート
- PnP イベント WDK NDIS ポートのアクティブ化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b40a36ccc7fcb83110e1c8a684977bd2b5ac453e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532356"
---
# <a name="handling-the-port-activation-pnp-event"></a>ポート アクティベーション PnP イベントを処理します。





ドライバーの関連を処理する必要があります、 **NetEventPortActivation** PnP イベント ミニポート ドライバーには、NDIS ポートがアクティブにするとします。 NDIS では、既定のポートがアクティブ化されてまでプロトコル ドライバーとミニポート アダプター間のバインドは開始しません。 そのため、プロトコルのドライバーがへの呼び出しを扱う必要があります、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)既定のポートがアクティブである通知として機能します。

プロトコル ドライバーは、いない、ドライバーは、そのポートがアクティブで、バインド パラメーター、またはを通じて通知を受信した場合を除き、NDIS 要求のポート番号を使用する必要があります、 **NetEventPortActivation** PnP イベント。

NDIS イベントが生成されますポート アクティベーション PnP、ミニポート ドライバーにはいくつかのポートがアクティブにした後。 (ミニポート ドライバーを指定、 **NetEventPortActivation**イベントのコードでの PnP、 [ **NET\_PNP\_イベント\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff568752)構造体、 *NetPnPEvent*への呼び出しでパラメーターが指す[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616) NDIS ポートをアクティブにします)。

ミニポート ドライバーを使用して 1 つの PnP 通知で複数のポートのアクティブ化を示すことができます、**次**内のメンバー、 [ **NDIS\_ポート**](https://msdn.microsoft.com/library/windows/hardware/ff566769)をリンクする構造体複数の NDIS\_ポート構造体。 NDIS の詳細リンクのリストについて\_ポートの構造を参照してください[ライセンス NDIS ポート](activating-an-ndis-port.md)します。

NDIS 生成、 **NetEventPortDeactivation**ミニポートにいくつかのポートが非アクティブ化時にバインドされているプロトコル ドライバーに PnP イベント。 詳細については、 **NetEventPortDeactivation** PnP イベントは、「[ポート非アクティブ化の PnP イベントを処理する](handling-the-port-deactivation-pnp-event.md)します。

 

 





