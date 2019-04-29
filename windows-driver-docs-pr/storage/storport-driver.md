---
title: Storport ドライバー
description: Storport ドライバー
ms.assetid: d5bda2f6-c4bb-4b90-a149-131785295687
keywords:
- 記憶域ポート ドライバー WDK、Storport ドライバー
- Storport ドライバー WDK
- Storport ドライバー WDK、Storport ドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75eec4c3bcd6edc2b1b95de2832c84ed03a474cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322121"
---
# <a name="storport-driver"></a>Storport ドライバー


## <span id="ddk_storport_driver_kg"></span><span id="DDK_STORPORT_DRIVER_KG"></span>


SCSI ポート ドライバーだけでなく Microsoft Windows Server 2003 およびそれ以降のバージョン指定 Storport (*storport.sys*)、ファイバー チャネルなどの高パフォーマンスのバスで使用するために特に適したストレージ ポート ドライバーバスや RAID アダプター。

これには、SCSI ポート ドライバーではなく、Storport を使用するいくつかの利点があります。

-   パフォーマンスの向上、両方の面でスループットと使用されているシステム リソース。

-   強化されたミニポート ドライバー インターフェイスのアドレス ハイエンドの記憶域ベンダー、特に、ホストベース RAID とファイバーのニーズがベンダーをチャネルします。

すべてのベンダーは、可能であれば、Storport を使用する、SCSI ポート ドライバーではなく。 特定ただし制限が適用されます。 Storport は、アダプターまたはプラグ アンド プレイをサポートしていないデバイスでは使用できません。 DMA のすべてのデバイスは、Storport しないプログラミング サポート I/O または下位モードの DMA ために、DMA 機能、バス マスターにすることが必要です。 タグが付けられたキュー、autorequest 意味、WMI のサポート、デバイスを報告する必要があります、SCSI 問い合わせデータの並べ替えとアダプターの BIOS から直接起動に関するその他の制限が適用されます。 Storport ドライバーの使用に関する制限の詳細な一覧についてを参照してください。[を使用しての Storport のアダプターを使用するための要件](requirements-for-using-storport-with-an-adapter.md)します。

SCSI ポート ミニポート ドライバーのベンダーが行った投資を有効に活用するには、Storport は非常にいくつかの変更と SCSI ポート ミニポート ドライバーのアーキテクチャに従います。 新しいアルゴリズムが測定可能な速度の増加を生成できるまたはバスの高速のサポートを追加する必要がありました場所、領域で SCSI ポート ドライバー インターフェイスへの変更が行われました。

ここでは、次のトピックについて説明します。

[Storport ドライバーのライフ サイクル](life-cycle-of-a-storport-driver.md)

[Storport の履歴](history-of-storport.md)

[Storport によって提供される機能](capabilities-provided-by-storport.md)

[記憶域クラス ドライバーを使用した、Storport のインターフェイス](storport-s-interface-with-the-storage-class-driver.md)

[Storport ミニポート ドライバー、Storport のインターフェイス](storport-s-interface-with-storport-miniport-drivers.md)

[Storport の I/O モデル](storport-i-o-model.md)

[Storport のキューの管理](storport-queue-management.md)

[Storport イベント ログの拡張機能](storport-event-log-extensions.md)

[Storport エラー管理](storport-error-management.md)

[Storport のアイドル状態の電源管理](storport-idle-power-management.md)

[Storport で行う SCSI ポート ミニポート ドライバーの作業](making-scsi-port-miniport-drivers-work-with-storport.md)

 

 




