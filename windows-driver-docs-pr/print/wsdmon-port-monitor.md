---
title: WSDMON ポート モニター
description: WSDMON ポート モニター
ms.assetid: fd6b0136-ca6e-4882-b6b9-be868f0dfc18
keywords:
- 印刷モニター WDK、WSDMON
- WSDMON ポート モニター WDK
- WDK のポート モニターを印刷する WSDMON
- デバイスの WDK WIA、ポート モニター用の web サービス
- WSD コンプライアンス WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dd20426087a054acc693411e02c4fa5c9e9f831
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354902"
---
# <a name="wsdmon-port-monitor"></a>WSDMON ポート モニター


WSDMON ポート モニターに準拠しているネットワーク プリンターに印刷をサポートするプリンター ポート モニター、 [Web Services for Devices (WSD) テクノロジ](https://msdn.microsoft.com/library/windows/hardware/ff563758)します。 WSDMON ポート モニターは、WSD イベントをリッスンし、それに応じてプリンターの状態を更新します。 このポート モニターは Windows Vista の新機能です。

WSDMON ポート モニターを実行できます。

-   ネットワーク プリンターを検出し、それらをインストールします。

-   WSD プリンターにジョブを送信します。

-   WSD プリンターの構成と状態を監視し、それに応じてプリンター オブジェクトの状態を更新します。

-   サポートされているは、双方向 (bidi) クエリに応答する[bidi スキーマ](bidirectional-communication-schema.md)します。

-   Bidi スキーマの値の変更を監視し、通知を送信

TCP/IP ポート モニターと同様の方法で動作する WSDMON ([TCPMON](tcpmon-xcv-interface.md))。 次の TCPMON コマンドは WSDMON でサポートされていません。

AddPort

DeletePort

MonitorUI

WSDMON には、次の Xcv コマンドがサポートされています。

[CleanupPort](cleanupport.md)

[DeviceID](deviceid2.md)

[PnPXID](pnpxid.md)

[ResetCommunication](resetcommunication.md)

[ServiceID](serviceid.md)

デバイスの Web サービスの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




