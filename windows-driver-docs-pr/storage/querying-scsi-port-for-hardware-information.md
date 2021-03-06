---
title: SCSI ポートへのハードウェア情報のクエリ
description: SCSI ポートへのハードウェア情報のクエリ
ms.assetid: 2f3adc40-6e5a-4a70-8298-60359b77f04f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7396a044933a1a211aa8651815660b1029e5d8b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386289"
---
# <a name="querying-scsi-port-for-hardware-information"></a>SCSI ポートへのハードウェア情報のクエリ


## <span id="ddk_querying_scsi_port_for_hardware_information_kg"></span><span id="DDK_QUERYING_SCSI_PORT_FOR_HARDWARE_INFORMATION_KG"></span>


記憶域クラスおよびその他の上位レベルのドライバーできる機能については、デバイスの SCSI ポートをクエリし、クエリ プロパティ要求を使用してホスト バス アダプター ([**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property))。 クエリ プロパティ要求が、レガシ システムの PnP と同等の照会と機能の要求 ([**IOCTL\_SCSI\_取得\_照会\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data)と[ **IOCTL\_SCSI\_取得\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities))。 記憶域デバイスの場合は、SCSI ポートは記憶域デバイス記述子を返します ([**ストレージ\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)) SCSI 問い合わせデータまたは非 SCSI と同等の、格納していると。ホスト アダプターの SCSI ポートは、ストレージ アダプター記述子を返します ([**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)) 機能と制限事項のデータを格納しています。

高度なドライバーが渡す必要があります、 [**ストレージ\_プロパティ\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_property_query) SCSI ポート プロパティのクエリ要求に構造体。 高度なドライバーを設定した場合、 **QueryType**記憶域のメンバー\_プロパティ\_クエリ**StorageAdapterProperty**、SCSI ポートは、ストレージ アダプター記述子を返します。 上位レベルのドライバーを設定した場合、 **QueryType**メンバー **StorageDeviceProperty**、SCSI ポートは、記憶域デバイス記述子を返します。

高度なドライバーは、クエリのプロパティを送信する場合のアダプターの FDO に IRP の要求**QueryType**設定**StorageDeviceProperty**、SCSI ポート IRP が失敗しました。 クラス ドライバーが使用したデバイスの PDO をこの IRP を送信するかどうか**QueryType**設定**StorageAdapterProperty**、SCSI ポート アダプター FDO に IRP を転送します。

記憶域デバイス記述子と記憶域アダプター記述子の詳細については、次を参照してください[記憶域クラス ドライバーいる出力ルーチン](storage-class-driver-s-getdescriptor-routine.md)、とのリファレンス ページ[**ストレージ\_。プロパティ\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_property_query)、 [**ストレージ\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)、および[ **ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)します。

 

 




