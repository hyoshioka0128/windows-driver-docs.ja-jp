---
title: ストレージドライバーについて
description: ストレージ ドライバー
ms.assetid: 5512a8f1-20ad-4b78-a60e-7418ac7f2117
keywords:
- 記憶域ドライバー WDK
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: bb02e9e0b15ac35ce812b253ce6e2f0ab4dea15e
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606472"
---
# <a name="about-storage-drivers"></a>ストレージドライバーについて

「記憶域ドライバーの設計ガイド」のこのセクションには、次の情報が含まれています。

[ストレージドライバーのアーキテクチャ](storage-driver-architecture.md)

[ストレージドライバーとデバイスオブジェクト](storage-drivers-and-device-objects.md)

[ストレージドライバーのシステムヘッダーファイル](system-header-files-for-storage-drivers.md)

[ストレージドライバーのページング可能コードに関する制限事項](restrictions-on-pageable-code-in-storage-drivers.md)

[書き込みキャッシュプロパティのクエリ](querying-for-the-write-cache-property.md)

[記憶装置のデバイス一意識別子 (DUIDs)](device-unique-identifiers--duids--for-storage-devices.md)

[一般的なストレージ i/o 制御コード](general-storage-io-control-codes.md)

以降のセクションには、次の種類の Windows カーネルモードのストレージドライバーを設計するためのガイドラインが含まれています。

- ベンダー固有の SCSI HBA 用のオペレーティングシステムに依存しないミニポートドライバー ( [Scsi ミニポートドライバー](scsi-miniport-drivers.md)を参照してください)

- 非 SCSI ストレージアダプター用のミニポートドライバー ( [Scsi ミニポートドライバー](scsi-miniport-drivers.md)を参照してください)

- 新しい種類の周辺機器のクラスドライバー (「[ストレージクラスドライバー](introduction-to-storage-class-drivers.md)」を参照)

- ベンダー固有のテープデバイス用のオペレーティングシステムに依存しないテープ miniclass ドライバー (「[テープドライバー](tape-drivers-overview.md)」を参照)

- ベンダー固有のメディアチェンジャーデバイス用のチェンジャー miniclass ドライバー (「[チェンジャードライバー](changer-drivers.md)」を参照)

- クラスドライバーが既に存在する種類の周辺機器のフィルタードライバー (「[ストレージフィルタードライバー](storage-filter-drivers.md)」を参照)
