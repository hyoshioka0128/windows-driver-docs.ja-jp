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
ms.openlocfilehash: f3e1f63499a162258ecb089f1ac6455e043013c3
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606526"
---
# <a name="storport-driver"></a>Storport ドライバー

SCSI ポートドライバーに加えて、Microsoft Windows Server 2003 以降のバージョンでは、Storport (*storport*) が提供されています。これは、ファイバーチャネルバスや RAID アダプターなどの高パフォーマンスのバスでの使用に特に適したストレージポートドライバーです。

SCSI ポートドライバーではなく、Storport を使用することにはいくつかの利点があります。

- スループットと使用されるシステムリソースの両方でパフォーマンスが向上しました。

- ハイエンドの記憶域ベンダー (特にホストベースの RAID およびファイバーチャネルベンダー) のニーズに対応する、改良されたミニポートドライバーインターフェイス。

SCSI ポートドライバーではなく、可能な限り Storport を使用することをお勧めします。 ただし、特定の制限が適用されます。 プラグアンドプレイをサポートしていないアダプターまたはデバイスで Storport を使用することはできません。 Storport では、プログラムによる i/o または下位モードの DMA はサポートされないため、すべての DMA デバイスにはバスマスタリング DMA 機能が必要です。 タグ付きのキュー、autorequest sense、WMI のサポート、デバイスが報告する必要がある SCSI の問い合わせデータの種類、アダプターの ROM BIOS から直接起動することに関して、その他の制限が適用されます。 Storport ドライバーの使用に関する制限の詳細な一覧については、「[アダプターで Storport を使用するための要件](requirements-for-using-storport-with-an-adapter.md)」を参照してください。

SCSI ポートミニポートドライバーでベンダーが行った投資をより効果的に活用するために、Storport は SCSI ポートミニポートドライバーのアーキテクチャに従いますが、わずかな変更が加えられています。 SCSI ポートドライバーのインターフェイスへの変更は、新しいアルゴリズムで測定可能な速度が向上した場合や、高速バスのサポートを追加する必要があった場合に行われます。
