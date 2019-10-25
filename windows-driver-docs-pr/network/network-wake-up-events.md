---
title: ネットワーク ウェイクアップ イベントについて
description: ネットワーク ウェイクアップ イベントについて
ms.assetid: 85195d44-4d79-4feb-af35-c478dc4319c5
keywords:
- ウェイクアップ機能 WDK ネットワーク、種類
- Nic WDK ネットワーク、ウェイクアップイベント
- ネットワークインターフェイスカード WDK ネットワーク、ウェイクアップイベント
- マジックパケット WDK ネットワーク
- 'ウェイクアップ機能: WDK ネットワーク、ウェイクアップ機能について'
- ネットワークウェイクアップイベントの WDK ネットワーク
- 電源管理 WDK NDIS ミニポート、ウェイクアップ機能
- ウェイクアップフレームの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 621a51521ae498ef7f0c25b1563f6056892ed017
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827129"
---
# <a name="about-network-wake-up-events"></a>ネットワーク ウェイクアップ イベントについて





*ネットワークウェイクアップイベント*は、ネットワークアダプターがシステムをスリープ解除する原因となる外部イベントです。 ネットワークアダプターは、バス固有のウェイクアップシグナルをアサートすることによってシステムをスリープ解除し、最終的にシステムがスリープ状態から動作状態に移行します。

NDIS は、次の2つのネットワークウェイクアップイベントを定義します。

-   バインドされたプロトコルドライバーによって指定されたパターンを含むネットワークウェイクアップフレームの受信。

-   マジックパケットの受信。

ネットワークアダプターは、何も含まないネットワークウェイクアップイベントの任意の組み合わせをサポートできます。 ミニポートドライバーが[**ndis\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)の**PowerManagementCapabilities**メンバーを**NULL**に設定している場合、ndis は、ミニポートドライバーを電源管理非対応として扱います。

ネットワークアダプターの機能によっては、最も高い電力状態 (D0) を含め、任意のデバイスの電源状態からネットワークウェイクアップイベントが発生する可能性があります。

### <a name="network-wake-up-frames"></a>ネットワークウェイクアップフレーム

初期化中に、ネットワークアダプターが、指定されたパターンを含むパケットの受信時にウェイクアップを通知できることを示している場合、バインドされたプロトコルはネットワークアダプターでパターンベースのウェイクアップ方法を有効にし、ウェイクアップを指定できます。タン. この種類のウェイクアップを有効にするために、プロトコルドライバは、NDIS\_PNP\_WAKE\_UP\_PATTERN\_PNP に設定し\_復帰\_を[有効に](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)します。

プロトコルドライバーは、 [OID\_\_PNP を使用して\_wake\_UP\_パターンを追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)してウェイクアップパターンを指定します。また、受信パケットのどのバイトをパターンと比較するかを示すマスクも追加します。 プロトコルドライバーでは、OID\_PNP を使用してウェイクアップパターンを削除し、 [\_ウェイク\_up\_パターンを削除\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern)ことができます。

ネットワークウェイクアップフレームの詳細については、「[ネットワークデバイスの電源管理](https://go.microsoft.com/fwlink/p/?linkid=9945)」を参照してください。

### <a name="magic-packet-wake-up"></a>マジック-パケットウェイクアップ

*マジックパケット*は、受信側のネットワークアダプターの MAC アドレスの連続した16個のコピーを含むパケットです。

このセクションの内容:

[ウェイクアップイベントを有効にする](enabling-wake-up-events.md)

[ウェイクアップイベントの処理](handling-wake-up-events.md)

 

 





