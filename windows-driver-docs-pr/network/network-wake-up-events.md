---
title: ネットワーク ウェイクアップ イベント
description: ネットワーク ウェイクアップ イベント
ms.assetid: 85195d44-4d79-4feb-af35-c478dc4319c5
keywords:
- ウェイク アップ機能 WDK ネットワー キング、種類
- Nic の WDK ネットワー キング、ウェイク アップ イベント
- ネットワーク インターフェイス カードの WDK ネットワー キング、ウェイク アップ イベント
- マジック パケット WDK ネットワーク
- ウェイク アップ機能 WDK ネットワークでは、ウェイク アップ機能について
- ウェイク アップ イベント WDK ネットワークをネットワークします。
- WDK の NDIS ミニポート、ウェイク アップ機能の電源管理
- ウェイク アップ フレーム WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41451f070183f8a4eb39363530c6eeb8079faeb6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371210"
---
# <a name="network-wake-up-events"></a>ネットワーク ウェイクアップ イベント





A*ネットワーク ウェイク アップ イベント*ネットワーク アダプターがシステムをスリープ解除するを原因となる外部イベントです。 ネットワーク アダプターでは、最終的にスリープ状態から作業の状態に遷移を作成しているシステム バス固有ウェイク アップ信号をアサートすることで、システムを解除します。

NDIS は、次の 2 つのネットワークのウェイク アップ イベントを定義します。

-   バインドされているプロトコル ドライバーによって指定されたパターンを含むネットワーク ウェイク アップ フレームを受信します。

-   マジック パケットの受信を確認します。

ネットワーク アダプターには、まったくなしを含む、ネットワークのウェイク アップ イベントの任意の組み合わせをサポートできます。 NDIS ミニポート ドライバーが設定されている場合、ミニポート ドライバーとして電源管理に対応が扱われます、**デバイス**のメンバー [ **NDIS\_ミニポート\_アダプター\_一般的な\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)に**NULL**します。

ネットワーク アダプターの機能、に応じて highest-powered 状態 (D0) も含め、デバイスの電源の状態からネットワーク ウェイク アップのイベントが発生します。

### <a name="network-wake-up-frames"></a>ネットワークのウェイク アップ フレーム

初期化中に、ミニポート ドライバーでは、ネットワーク アダプターが、指定したパターンを含むパケットの受信時にウェイク アップを通知できることを示します場合、バインドされているプロトコルできますパターンに基づくウェイク アップ ネットワーク アダプター上のメソッドを有効にし、ウェイク アップを指定パターン。 この種類のウェイク アップを有効にするプロトコル ドライバーに設定、NDIS\_PNP\_WAKE\_を\_パターン\_の一致フラグ[OID\_PNP\_を有効にする\_WAKE\_を](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)します。

プロトコル ドライバーを使用して[OID\_PNP\_追加\_WAKE\_を\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)着信パケットのデータの量を示すマスクと共に、ウェイク アップのパターンを指定するにはパターンと比較する必要があります。 プロトコル ドライバーにウェイク アップのパターンを削除できます[OID\_PNP\_削除\_WAKE\_を\_パターン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern)します。

ネットワークのウェイク アップのフレームの詳細については、次を参照してください。[ネットワーク デバイスの電源管理](https://go.microsoft.com/fwlink/p/?linkid=9945)します。

### <a name="magic-packet-wake-up"></a>マジック パケットのウェイク アップ

A*マジック パケット*は受信側のネットワーク アダプターの MAC アドレスの 16 個の連続したコピーを含むパケットです。

このセクションの内容:

[ウェイク アップのイベントを有効にします。](enabling-wake-up-events.md)

[ウェイク アップのイベントの処理](handling-wake-up-events.md)

 

 





