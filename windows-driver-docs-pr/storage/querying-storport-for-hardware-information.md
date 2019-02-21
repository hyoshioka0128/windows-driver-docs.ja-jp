---
title: Storport は、ハードウェア情報の照会
description: Storport は、ハードウェア情報の照会
ms.assetid: 1e807e42-d03f-44be-a0a4-8187e2d5667a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27a746adc7e6fd5983e963906fd6ffc5e8344e42
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529144"
---
# <a name="querying-storport-for-hardware-information"></a>Storport は、ハードウェア情報の照会


記憶域クラスおよびその他の上位レベルのドライバーできます Storport をデバイスの機能に関する情報のクエリし、クエリ プロパティ要求を使用してホスト バス アダプター ([**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff560590))。 クエリ プロパティ要求が、レガシ システムの PnP と同等の照会と機能の要求 ([**IOCTL\_SCSI\_取得\_照会\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff560509)と[ **IOCTL\_SCSI\_取得\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff560502))。 Storport 記憶装置、ストレージ デバイスの記述子を返します ([**ストレージ\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566971)) SCSI 問い合わせデータまたは非 SCSI と同等の格納しているとホスト アダプター Storport 記憶域アダプター記述子を返します ([**ストレージ\_アダプター\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566346)) 機能と制限事項のデータを格納しています。

高度なドライバーが渡す必要があります、 [**ストレージ\_プロパティ\_クエリ**](https://msdn.microsoft.com/library/windows/hardware/ff566997) Storport プロパティのクエリ要求に構造体。 高度なドライバーを設定した場合、 **PropertyId**のメンバー**ストレージ\_プロパティ\_クエリ**に**StorageAdapterProperty**、Storport記憶域アダプターの記述子を返します。 上位レベルのドライバーを設定した場合、 **PropertyId**メンバー **StorageDeviceProperty**、Storport 記憶域デバイス記述子を返します。

高度なドライバーは、クエリのプロパティを送信する場合のアダプターの FDO に IRP の要求**PropertyId**設定**StorageDeviceProperty**、Storport IRP が失敗しました。 クラス ドライバーが使用したデバイスの PDO をこの IRP を送信するかどうか**PropertyId**設定**StorageAdapterProperty**、Storport アダプター FDO に IRP を転送します。

記憶域デバイス記述子と記憶域アダプター記述子の詳細については、次を参照してください[記憶域クラス ドライバーいる出力ルーチン](storage-class-driver-s-getdescriptor-routine.md)、とのリファレンス ページ[**ストレージ\_。プロパティ\_クエリ**](https://msdn.microsoft.com/library/windows/hardware/ff566997)、 [**ストレージ\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566971)、および[ **ストレージ\_アダプター\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566346)します。

 

 




