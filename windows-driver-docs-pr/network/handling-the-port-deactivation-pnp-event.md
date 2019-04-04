---
title: ポート非アクティブ化 PnP イベントの処理
description: ポート非アクティブ化 PnP イベントの処理
ms.assetid: 0e3b10a7-5ab5-48e1-a5cc-c7bc6ce26410
keywords:
- WDK NDIS、PnP イベント通知をポートします。
- NDIS ポート WDK、PnP イベント通知
- PnP イベント通知 WDK NDIS ポート
- 非アクティブ化の PnP イベント WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bd47e09d1e1e783d6384e112096f06963ee8d45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579060"
---
# <a name="handling-the-port-deactivation-pnp-event"></a>ポート非アクティブ化 PnP イベントの処理





ドライバーの関連を処理する必要があります、 **NetEventPortDeactivation**ミニポート ドライバーには、NDIS ポートが非アクティブ化したときに PnP イベント。 ポートの非アクティブ化イベントについての上にあるドライバーを通知するには、NDIS は、基になるミニポート ドライバーからポートの非アクティブ化の PnP イベントを伝達します。

プロトコル ドライバーには、ポートの非アクティブ化の PnP イベントの処理が完了すると、前に、未処理のすべての OID 要求とポートに関連付けられている送信要求が完了したことを確認する必要があります。 プロトコル ドライバーには、PnP イベントが完了すると、ドライバーはこと、OID 要求を発行したりしないポートに対する要求を送信することを確認する必要があります。

ミニポート ドライバーを指定、 **NetEventPortDeactivation**イベントのコードでの PnP、 [ **NET\_PNP\_イベント\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff568752)構造体、 *NetPnPEvent*への呼び出しでパラメーターが指す、 [ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)ポートの一部であったレポートする関数非アクティブ化します。 ミニポート ドライバーは、NDIS の配列を指定します\_ポート\_番号の値を非アクティブ化されたポートを一覧表示します。 ポート番号の詳細については、配列は、[Deactivating NDIS ポート](deactivating-an-ndis-port.md)を参照してください。

 

 





