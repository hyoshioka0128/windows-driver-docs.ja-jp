---
title: Storport へのハードウェア情報のクエリ
description: Storport へのハードウェア情報のクエリ
ms.assetid: 1e807e42-d03f-44be-a0a4-8187e2d5667a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbaadb46da97dc083a081fdbf38cc33b17d83c7b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369565"
---
# <a name="querying-storport-for-hardware-information"></a>Storport へのハードウェア情報のクエリ


記憶域クラスおよびその他の上位レベルのドライバーできます Storport をデバイスの機能に関する情報のクエリし、クエリ プロパティ要求を使用してホスト バス アダプター ([**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property))。 クエリ プロパティ要求が、レガシ システムの PnP と同等の照会と機能の要求 ([**IOCTL\_SCSI\_取得\_照会\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data)と[ **IOCTL\_SCSI\_取得\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities))。 Storport 記憶装置、ストレージ デバイスの記述子を返します ([**ストレージ\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)) SCSI 問い合わせデータまたは非 SCSI と同等の格納しているとホスト アダプター Storport 記憶域アダプター記述子を返します ([**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)) 機能と制限事項のデータを格納しています。

高度なドライバーが渡す必要があります、 [**ストレージ\_プロパティ\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_property_query) Storport プロパティのクエリ要求に構造体。 高度なドライバーを設定した場合、 **PropertyId**のメンバー**ストレージ\_プロパティ\_クエリ**に**StorageAdapterProperty**、Storport記憶域アダプターの記述子を返します。 上位レベルのドライバーを設定した場合、 **PropertyId**メンバー **StorageDeviceProperty**、Storport 記憶域デバイス記述子を返します。

高度なドライバーは、クエリのプロパティを送信する場合のアダプターの FDO に IRP の要求**PropertyId**設定**StorageDeviceProperty**、Storport IRP が失敗しました。 クラス ドライバーが使用したデバイスの PDO をこの IRP を送信するかどうか**PropertyId**設定**StorageAdapterProperty**、Storport アダプター FDO に IRP を転送します。

記憶域デバイス記述子と記憶域アダプター記述子の詳細については、次を参照してください[記憶域クラス ドライバーいる出力ルーチン](storage-class-driver-s-getdescriptor-routine.md)、とのリファレンス ページ[**ストレージ\_。プロパティ\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_property_query)、 [**ストレージ\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)、および[ **ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)します。

 

 




