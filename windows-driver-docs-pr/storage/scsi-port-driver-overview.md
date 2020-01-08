---
title: SCSI ポート ドライバーの概要
description: SCSI ポート ドライバーの概要
ms.assetid: e97ea5f2-7f20-4d3d-82a2-7d83e1eba30e
keywords:
- 記憶域ポートドライバー WDK、SCSI ポートドライバー
- SCSI ポートドライバー WDK 記憶域
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 61aaac571d5d8b06466f2001716903d2804cf3fa
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606502"
---
# <a name="scsi-port-driver-overview"></a>SCSI ポート ドライバーの概要

Microsoft では、SCSI ポートドライバーを Microsoft Windows ストレージアーキテクチャの標準機能として提供しています。 SCSI ポートドライバーは、簡略化された SCSI アダプターをエミュレートすることによって、Windows 記憶域サブシステムを合理化します。 ストレージクラスドライバーは、ポートドライバーの上に読み込まれます。 これは、各 SCSI アダプターの固有のハードウェア機能を最小限の問題で、Windows の記憶域クラスドライバーを記述できることを意味します。

SCSI ポートドライバーのエミュレーション機能では、モノリシックポートドライバーよりも設計とコーディングがはるかに簡単なミニドライバーを開発することもできます。 つまり、SCSI ポートドライバーを使用すると、アダプターの特定の機能を処理するミニポートドライバーの開発に専念することができます。

SCSI ポートサポートルーチンを使用するには、SCSI ポートサポートライブラリ、 *scsiport* 、または*scsiwmi*のいずれかにリンクします。 これらの SCSI ポートライブラリは、ミニポートドライバーとオペレーティングシステムのハードウェアアブストラクションレイヤー (HAL) との間のすべての通信を処理します。 ミニポート*ドライバーは、* hal サポートライブラリや*hal.dll*に直接リンクしたり、 *libcntpr*サポートライブラリに直接リンクしたりすることはできません。 SCSI ミニポートドライバーは、Windows ロゴの対象にはなりません。

次のセクションでは、SCSI ポートドライバーの主な機能について説明します。

- [SCSI ポートによって提供される機能](capabilities-provided-by-scsi-port.md)

- [SCSI ポートドライバーのサポートルーチン](scsi-port-driver-support-routines.md)

- [ストレージクラスドライバーを使用した SCSI ポートのインターフェイス](scsi-port-s-srb-interface-with-the-storage-class-driver.md)

- [Scsi ポートミニポートドライバーを使用した SCSI ポートのインターフェイス](scsi-port-s-interface-with-scsi-port-miniport-drivers.md)

- [SCSI ポート i/o モデル](scsi-port-i-o-model.md)

Scsi ミニポートドライバーについては、scsi[ミニ](scsi-miniport-drivers.md)ポートドライバーに関する一般的な説明があります。

Windows ストレージアーキテクチャでは、高パフォーマンスデバイス用の SCSI ポートの代替として、 [Storport ドライバー](storport-driver-overview.md)も提供しています。
