---
title: ストレージ ドライバー
description: ストレージ ドライバー
ms.assetid: 5512a8f1-20ad-4b78-a60e-7418ac7f2117
keywords:
- ストレージ ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 200e26dfc878ab56ddfdf84dd776b82a538ce4f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331705"
---
# <a name="storage-drivers"></a>ストレージ ドライバー


## <span id="ddk_storage_drivers_kg"></span><span id="DDK_STORAGE_DRIVERS_KG"></span>


このセクションには、次の情報が含まれています。

[ストレージ ドライバーのアーキテクチャ](storage-driver-architecture.md)

[記憶装置ドライバーとデバイス オブジェクト](storage-drivers-and-device-objects.md)

[記憶装置ドライバーのシステム ヘッダー ファイル](system-header-files-for-storage-drivers.md)

[ページング可能なコード記憶装置ドライバーの制約](restrictions-on-pageable-code-in-storage-drivers.md)

[書き込みキャッシュのプロパティのクエリを実行します。](querying-for-the-write-cache-property.md)

[記憶域デバイス (Duid) の一意の識別子をデバイス](device-unique-identifiers--duids--for-storage-devices.md)

後続のセクションには、次の種類の Windows カーネル モードの記憶装置ドライバーを設計するためのガイドラインが含まれます。

-   ベンダー固有の SCSI HBA のオペレーティング システムに依存しないミニポート ドライバー (を参照してください[SCSI ミニポート ドライバー](scsi-miniport-drivers.md))

-   非 SCSI 記憶域アダプターのミニポート ドライバー (を参照してください[SCSI ミニポート ドライバー](scsi-miniport-drivers.md))

-   周辺機器のデバイスの新しい種類のクラス ドライバー (を参照してください[ストレージ クラス ドライバー](storage-class-drivers.md))

-   ベンダー固有のテープ デバイスのオペレーティング システムに依存しないテープ miniclass ドライバー (を参照してください[テープ ドライバー](tape-drivers.md))

-   メディア チェンジャーのベンダー固有のデバイスのチェンジャー miniclass ドライバー (を参照してください[チェンジャー ドライバー](changer-drivers.md))

-   既にクラス ドライバーを持つ型の周辺機器のフィルター ドライバー (を参照してください[ストレージ フィルター ドライバー](storage-filter-drivers.md))

 

 




