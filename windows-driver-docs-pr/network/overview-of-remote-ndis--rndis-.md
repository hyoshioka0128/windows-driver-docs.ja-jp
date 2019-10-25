---
title: リモート NDIS (RNDIS) の概要
description: リモート NDIS (RNDIS) の概要
ms.assetid: 03da539d-9613-4454-8f79-514e76767af6
keywords:
- リモート NDIS WDK ネットワーク, アーキテクチャ
- リモート NDIS WDK ネットワーク、USB トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 867803d43f142127c3bab565b28f5e53fdf11f73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843724"
---
# <a name="overview-of-remote-ndis-rndis"></a>リモート NDIS (RNDIS) の概要





リモート NDIS (RNDIS) を使用すると、ハードウェアベンダーは、USB バスに接続されたネットワークデバイス用の NDIS ミニポートデバイスドライバーを作成する必要がなくなります。 リモート NDIS では、バスに依存しないメッセージセットと、このメッセージセットが USB バス上でどのように動作するかについての説明を定義することで、これを実現しています。 このリモート NDIS インターフェイスは標準化されているため、1つのホストドライバーセットで、USB バスに接続されている任意の数のネットワークデバイスをサポートできます。 これにより、デバイスの製造元の開発負担が大幅に軽減され、新しいドライバーが必要ないため、システムの全体的な安定性が向上します。また、新しい USB をサポートするためにインストールするドライバーがないため、エンドユーザーエクスペリエンスが向上します。バスに接続されたネットワークデバイス。 現在、Microsoft Windows では、USB 経由のリモート NDIS がサポートされています。

次の図は、リモート NDIS ミニポートドライバーと USB 転送ドライバーの組み合わせを使用して、デバイス製造元の NDIS ミニポートを交換する方法を示しています。 このため、デバイスの製造元はデバイスの実装に専念できるため、Windows NDIS デバイスドライバーを開発する必要はありません。

![リモート ndis のアーキテクチャを示す図](images/remote-ndis-architecture.png)

Microsoft では、NDIS ミニポートドライバー Rndismp を提供しています。このドライバーは、リモート NDIS メッセージセットを実装し、汎用バストランスポートドライバーと通信します。このドライバーは、適切なバスドライバーと通信します。 この NDIS ミニポートドライバーは、Microsoft によって実装および管理され、Windows の一部として配布されます。

次のリモート NDIS メッセージセットは、NDIS ミニポートドライバーインターフェイスのセマンティクスを反映しています。

-   デバイス操作の初期化、リセット、および停止

-   ネットワークデータパケットの送受信

-   デバイスの操作パラメーターの設定とクエリ

-   メディアリンクの状態と監視デバイスの状態を示す

また、usb バス経由でリモート NDIS メッセージを送信するメカニズムを実装する USB バストランスポートドライバーも用意されています。 このドライバーは、リモート NDIS ミニポートドライバーとバス固有のドライバー (USB など) との間で標準化されたリモート NDIS メッセージを転送します。 バス固有のドライバーは、電源管理などのバス固有の要件を標準化されたリモート NDIS メッセージにマップするためにも必要です。 USB 1.1 および2.0 用のトランスポートドライバーは、Microsoft によって実装および管理され、Windows の一部として配布されます。

この構造により、バス固有のトランスポート層がある任意のリモート NDIS デバイスに対して1つのデバイスドライバーを使用できます。 また、特定のバス上のすべてのネットワークデバイスに対して必要なバストランスポート層は1つだけです。

ここでは、次のトピックについて説明します。

[リモート NDIS の利点](benefits-of-remote-ndis.md)

[リモート NDIS の概念と定義](remote-ndis-concepts-and-definitions.md)

[リモート NDIS ファイルの名前付け規則](remote-ndis-file-naming-conventions.md)

[リモート NDIS メッセージング](remote-ndis-messaging.md)

[リモート NDIS デバイス制御](remote-ndis-device-control.md)

[リモート NDIS INF テンプレート](remote-ndis-inf-template.md)

[リモート NDIS デバイスの種類](types-of-remote-ndis-devices.md)

## <a name="related-topics"></a>関連トピック


[Windows に含まれる USB クラスドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 






