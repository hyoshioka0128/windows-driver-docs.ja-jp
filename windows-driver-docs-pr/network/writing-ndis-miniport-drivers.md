---
title: 書き込みの NDIS ミニポート ドライバー
description: 書き込みの NDIS ミニポート ドライバー
ms.assetid: ebcc06a1-bc3a-454b-9437-8c38bf9b4434
keywords:
- ミニポート ドライバー WDK ネットワーク、ミニポート ドライバーの記述
- ネットワーク ドライバー WDK、ミニポート ドライバー
- NDIS WDK、ミニポート ドライバー
- NDIS ミニポート ドライバー WDK、ミニポート ドライバーの記述
- NDIS ミニポート ドライバー WDK ネットワークの作成
- NDIS ミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c2cae199f5b862f78c1988665c80b9b5079c883
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557310"
---
# <a name="writing-ndis-miniport-drivers"></a>書き込みの NDIS ミニポート ドライバー





このセクションでは、ドライバー操作の NDIS ミニポートの概要を示します。 NDIS ミニポート ドライバー提供*MiniportXxx*関数呼び出し、NDIS、操作を開始します。 NDIS 提供**Ndis * Xxx*** そのミニポート ドライバーの呼び出し操作を実行する関数。

ここでは、次のトピックについて説明します。

[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)

[ミニポート ドライバーをアンロード](unloading-a-miniport-driver.md)

[ミニポート アダプタの状態と操作](miniport-adapter-states-and-operations.md)

[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)

[ミニポート アダプターを停止します。](halting-a-miniport-adapter.md)

[開始およびミニポート アダプターを一時停止](starting-and-pausing-a-miniport-adapter.md)

[省略可能なミニポート ドライバー サービスを構成します。](configuring-optional-miniport-driver-services.md)

[ミニポート ドライバーの送信し、受信操作](miniport-driver-send-and-receive-operations.md)

[DMA のスキャッター/ギャザー](scatter-gather-dma2.md)

[割り込みを管理します。](managing-interrupts.md)

[ミニポート アダプタの OID 要求](miniport-adapter-oid-requests.md)

[Minioprt アダプター状態のインジケーター](miniport-adapter-status-indications.md)

[ミニポート アダプター デバイス PnP イベント通知](miniport-adapter-device-pnp-event-notifications.md)

[ミニポート アダプタのチェック-ハング用とリセットの操作](miniport-adapter-check-for-hang-and-reset-operations.md)

[ミニポート アダプタのシャット ダウン](miniport-adapter-shutdown.md)

 

 





