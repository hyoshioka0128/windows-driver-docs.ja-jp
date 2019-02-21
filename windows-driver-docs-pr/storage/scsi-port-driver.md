---
title: SCSI ポート ドライバー
description: SCSI ポート ドライバー
ms.assetid: e97ea5f2-7f20-4d3d-82a2-7d83e1eba30e
keywords:
- 記憶域ポート ドライバー WDK、SCSI ポート ドライバー
- SCSI ポート ドライバー WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143c54eb27bfb203d03cc951499d1de284ca57f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557485"
---
# <a name="scsi-port-driver"></a>SCSI ポート ドライバー


## <span id="ddk_scsi_port_driver_kg"></span><span id="DDK_SCSI_PORT_DRIVER_KG"></span>


Microsoft では、Microsoft Windows 記憶域アーキテクチャの標準機能として SCSI ポート ドライバーを提供します。 SCSI ポート ドライバーでは、簡略化された SCSI アダプタをエミュレートすることにより、Windows 記憶域サブシステムを効率化します。 記憶域クラス ドライバーは、ポート、ドライバーの上に読み込みます。 つまり、ストレージ クラス ドライバーの各 SCSI アダプター固有のハードウェア機能の問題を最小限に Windows を記述できます。

SCSI ポート ドライバーのエミュレーション機能では、モノリシック ポート ドライバーよりも設計とコードをシンプル ミニドライバーを開発することもできます。 つまり、SCSI ポート ドライバーを使用して使用するアダプターの特定の機能を処理するミニポート ドライバーの開発に集中できます。

SCSI ポート サポート ルーチンを使用する、SCSI ポート サポート ライブラリのいずれかにリンク*scsiport.lib*または*scsiwmi.lib*します。 これらの SCSI ポート ライブラリは、ミニポート ドライバーとオペレーティング システムのハードウェア アブストラクション レイヤー (HAL) 間のすべての対話を処理します。 ミニポート ドライバーが、HAL サポート ライブラリに直接リンクする必要があります*hal.lib*への直接リンクする必要がありますも、 *ntoskrnl.lib*または*関数*ライブラリをサポートします。 ような SCSI ミニポート ドライバーは、Windows ロゴの対象ではありません。

次のセクションでは、SCSI ポート ドライバーの主な機能を確認します。

1.  [SCSI ポートによって提供される機能](capabilities-provided-by-scsi-port.md)

2.  [記憶域クラス ドライバーを使用した SCSI ポートのインターフェイス](scsi-port-s-interface-with-the-storage-class-driver.md)

3.  [SCSI ポート ミニポート ドライバーと SCSI ポートのインターフェイス](scsi-port-s-interface-with-scsi-port-miniport-drivers.md)

4.  [SCSI ポート I/O モデル](scsi-port-i-o-model.md)

SCSI ポート ミニポート ドライバーの概要についてで提供される[SCSI ミニポート ドライバー](scsi-miniport-drivers.md)します。

Windows のストレージ アーキテクチャにも用意されています、 [Storport ドライバー](storport-driver.md)高性能なデバイスの SCSI ポートへの代替。

 

 




