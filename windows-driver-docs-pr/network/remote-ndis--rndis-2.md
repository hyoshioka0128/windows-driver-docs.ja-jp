---
title: リモート NDIS (RNDIS)
description: リモート NDIS (RNDIS)
ms.assetid: 857cec9c-6098-4fd3-9528-fa592da997f4
keywords:
- リモートの NDIS WDK ネットワーク
- ネットワーク ドライバー WDK、リモートの NDIS
- RNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc549cad806a7863478d06a1c728d0c580912bbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574008"
---
# <a name="remote-ndis-rndis"></a>リモート NDIS (RNDIS)





リモート NDIS (RNDIS) は、1394、Bluetooth、または InfiniBand イーサネット (802.3) ネットワーク デバイス、USB などの動的のプラグ アンド プレイ (PnP) バスのバスに依存しないクラス仕様です。 リモートの NDIS は、抽象コントロールとデータ チャネル経由でのホスト コンピューターとリモートの NDIS デバイス間のバスに依存しないメッセージ プロトコルを定義します。 リモートの NDIS は、ホスト コンピューターでリモート NDIS デバイスのベンダーに依存しないクラス ドライバーのサポートを許可するのに十分な正確です。

Microsoft Windows のバージョン Windows XP 以降にはでは、USB デバイス用のリモート NDIS ドライバーが含まれます。 IHV の USB デバイスには、このドライバーを使用して、テンプレートに続く INF ファイルを提供する必要があります[リモート NDIS INF テンプレート](remote-ndis-inf-template.md)します。

リモートの NDIS メッセージは、ホストから NDIS リモート デバイスに送信され、リモート NDIS デバイスが適切な完了メッセージを返します。 メッセージはもホストにリモート NDIS デバイスから要請されていない方法で送信します。

このセクションの内容:

[リモートの NDIS (RNDIS) の概要](overview-of-remote-ndis--rndis-.md)

[リモートの NDIS 通信](remote-ndis-communication.md)

[リモートの NDIS と USB のマッピング](remote-ndis-to-usb-mapping.md)


 

 





