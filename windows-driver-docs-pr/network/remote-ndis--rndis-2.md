---
title: リモート NDIS の概要 (RNDIS)
description: リモート NDIS の概要 (RNDIS)
ms.assetid: 857cec9c-6098-4fd3-9528-fa592da997f4
keywords:
- リモート NDIS WDK ネットワーク
- ネットワークドライバー WDK、リモート NDIS
- RNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad9a4499897ed2b382e450b6c1dee4f71bdc4fd4
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565702"
---
# <a name="introduction-to-remote-ndis-rndis"></a>リモート NDIS の概要 (RNDIS)





リモート NDIS (RNDIS) は、USB、1394、Bluetooth、InfiniBand などの動的プラグアンドプレイ (PnP) バス上のイーサネット (802.3) ネットワークデバイス向けのバス非依存クラス仕様です。 リモート NDIS は、抽象コントロールとデータチャネルを介して、ホストコンピューターとリモート NDIS デバイスとの間でバスに依存しないメッセージプロトコルを定義します。 リモート NDIS は、ホストコンピューター上のリモート NDIS デバイスに対してベンダーに依存しないクラスドライバーのサポートを許可するのに十分な精度を備えています。

Windows XP 以降の Microsoft Windows のバージョンには、USB デバイス用のリモート NDIS ドライバーが含まれています。 このドライバーを USB デバイスで使用するには、IHV が、[リモート NDIS Inf テンプレート](remote-ndis-inf-template.md)のテンプレートに従う INF ファイルを提供する必要があります。

リモート ndis メッセージはホストからリモート NDIS デバイスに送信され、リモート NDIS デバイスは適切な完了メッセージで応答します。 また、リモート NDIS デバイスからホストにメッセージが送信されることもありません。

このセクションの内容:

[リモート NDIS の概要 (RNDIS)](overview-of-remote-ndis--rndis-.md)

[リモート NDIS 通信](remote-ndis-communication.md)

[リモート NDIS から USB へのマッピング](remote-ndis-to-usb-mapping.md)


 

 





