---
title: Storport ドライバー
description: Storport ドライバー
ms.assetid: d5bda2f6-c4bb-4b90-a149-131785295687
keywords:
- ストレージポートドライバー WDK、Storport ドライバー
- Storport ドライバー WDK
- Storport ドライバー WDK、Storport ドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75eec4c3bcd6edc2b1b95de2832c84ed03a474cb
ms.sourcegitcommit: 0610366df5de756bf8aa6bfc631eba5e3cd84578
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72271823"
---
# <a name="storport-driver"></a>Storport ドライバー


## <span id="ddk_storport_driver_kg"></span><span id="DDK_STORPORT_DRIVER_KG"></span>


SCSI ポートドライバーに加えて、Microsoft Windows Server 2003 以降のバージョンでは、Storport (*storport*) が提供されています。これは、ファイバーチャネルバスや RAID アダプターなどの高パフォーマンスのバスでの使用に特に適したストレージポートドライバーです。

SCSI ポートドライバーではなく、Storport を使用することにはいくつかの利点があります。

-   スループットと使用されるシステムリソースの両方でパフォーマンスが向上しました。

-   ハイエンドの記憶域ベンダー (特にホストベースの RAID およびファイバーチャネルベンダー) のニーズに対応する、改良されたミニポートドライバーインターフェイス。

SCSI ポートドライバーではなく、可能な限り Storport を使用することをお勧めします。 ただし、特定の制限が適用されます。 プラグアンドプレイをサポートしていないアダプターまたはデバイスで Storport を使用することはできません。 Storport では、プログラムによる i/o または下位モードの DMA はサポートされないため、すべての DMA デバイスにはバスマスタリング DMA 機能が必要です。 タグ付きのキュー、autorequest sense、WMI のサポート、デバイスが報告する必要がある SCSI の問い合わせデータの種類、アダプターの ROM BIOS から直接起動することに関して、その他の制限が適用されます。 Storport ドライバーの使用に関する制限の詳細な一覧については、「[アダプターで Storport を使用するための要件](requirements-for-using-storport-with-an-adapter.md)」を参照してください。

SCSI ポートミニポートドライバーでベンダーが行った投資をより効果的に活用するために、Storport は SCSI ポートミニポートドライバーのアーキテクチャに従いますが、わずかな変更が加えられています。 SCSI ポートドライバーのインターフェイスへの変更は、新しいアルゴリズムで測定可能な速度が向上した場合や、高速バスのサポートを追加する必要があった場合に行われます。

ここでは、次のトピックについて説明します。

[Storport ドライバーのライフサイクル](life-cycle-of-a-storport-driver.md)

[Storport の履歴](history-of-storport.md)

[Storport によって提供される機能](capabilities-provided-by-storport.md)

[ストレージクラスドライバーを使用した Storport のインターフェイス](storport-s-interface-with-the-storage-class-driver.md)

[Storport ミニポートドライバーを使用した storport のインターフェイス](storport-s-interface-with-storport-miniport-drivers.md)

[Storport i/o モデル](storport-i-o-model.md)

[Storport キュー管理](storport-queue-management.md)

[Storport イベントログの拡張機能](storport-event-log-extensions.md)

[Storport エラーの管理](storport-error-management.md)

[Storport アイドル状態の電源管理](storport-idle-power-management.md)

[SCSI ポートミニポートドライバーを Storport で動作させる](making-scsi-port-miniport-drivers-work-with-storport.md)

 

 




