---
title: リモート NDIS (RNDIS) の概要
description: リモート NDIS (RNDIS) の概要
ms.assetid: 03da539d-9613-4454-8f79-514e76767af6
keywords:
- リモートの NDIS WDK のネットワーク アーキテクチャ
- リモートの NDIS WDK のネットワーク、USB transport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfcc0748f952439cf1de6b2b8380a855f9d2b7b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376984"
---
# <a name="overview-of-remote-ndis-rndis"></a>リモート NDIS (RNDIS) の概要





リモート NDIS (RNDIS) ハードウェア ベンダーで、USB バスに接続されたネットワーク デバイスの NDIS ミニポート デバイス ドライバーを作成する必要はありません。 リモートの NDIS は、バスに依存しないメッセージのセットと、USB バス経由でこのメッセージのセットの動作方法の説明を定義することでこれを実現します。 このリモート NDIS インターフェイスが標準化されているために、ホスト ドライバーのセットを 1 つは、USB バスに接続されているネットワーク デバイスの数をサポートできます。 これが大幅にデバイスの製造元の開発の負担を軽減でき、必要な場合は、新しいドライバーがないため、システムの全体的な安定性が向上および新しい USB をサポートするためにインストールするドライバーがないため、エンド ユーザー エクスペリエンスの向上バスに接続されたネットワーク デバイス。 現在 Microsoft Windows では、USB 経由でリモートの NDIS のサポートを提供します。

次の図は、リモートの NDIS ミニポート ドライバーと USB トランスポート ドライバーの組み合わせでデバイスの製造元の NDIS ミニポートの置換を示します。 デバイスの製造元では、そのため、デバイスの実装に集中でき、Windows の NDIS ドライバーを開発する必要がないすることができます。

![リモートの ndis のアーキテクチャを示す図](images/remote-ndis-architecture.png)

Microsoft では、NDIS ミニポート ドライバー、Rndismp.sys、リモート NDIS メッセージ セットを実装し、ジェネリック bus トランスポート ドライバーは、さらに、適切なバス ドライバーとの通信とは通信を提供します。 この NDIS ミニポート ドライバーが実装され、Microsoft によって管理されると、Windows の一部として配布されます。

次のリモートの NDIS メッセージは、NDIS ミニポート ドライバー インターフェイスのセマンティクスのミラーを設定します。

-   初期化、リセット、およびデバイスの操作を停止します。

-   ネットワークのデータ パケットを送受信します。

-   設定とデバイスの操作パラメーターのクエリを実行します。

-   示すメディア リンクの状態とデバイスの監視の状態

Microsoft では、USB バスで NDIS リモート メッセージを実行するためのメカニズムを実装する USB バス トランスポート ドライバーも提供します。 このドライバーは、リモートの NDIS ミニポート ドライバーと USB など、bus 固有のドライバーの標準化の NDIS リモート メッセージを転送します。 Bus 固有のドライバーは、標準化されたリモート NDIS メッセージに、電源管理などのバス固有要件をマップするも必要です。 トランスポートのドライバーを USB 1.1 および 2.0 が実装され、Microsoft によって管理される、Windows の一部として配布されます。

この構造体は、バスに固有のトランスポート層が存在する任意のリモートの NDIS デバイスに使用する 1 つのデバイス ドライバーをできます。 さらに、1 つだけのバス トランスポート層は、特定のバス上のすべてのネットワーク デバイスに必要なは。

このセクションには、次の補足トピックが含まれています。

[リモートの NDIS の利点](benefits-of-remote-ndis.md)

[リモートの NDIS 概念と定義](remote-ndis-concepts-and-definitions.md)

[リモートの NDIS ファイルの名前付け規則](remote-ndis-file-naming-conventions.md)

[リモートの NDIS メッセージング](remote-ndis-messaging.md)

[リモートの NDIS デバイスの制御](remote-ndis-device-control.md)

[リモートの NDIS INF テンプレート](remote-ndis-inf-template.md)

[リモートの NDIS デバイスの種類](types-of-remote-ndis-devices.md)

## <a name="related-topics"></a>関連トピック


[Windows に含まれる USB クラス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff538820)

 

 






