---
title: SCSI ポートへのハードウェア情報のクエリ
description: SCSI ポートへのハードウェア情報のクエリ
ms.assetid: 2f3adc40-6e5a-4a70-8298-60359b77f04f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cefec842b0c88ad27a6ffc32fa83fcfadb12c94
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842720"
---
# <a name="querying-scsi-port-for-hardware-information"></a>SCSI ポートへのハードウェア情報のクエリ


## <span id="ddk_querying_scsi_port_for_hardware_information_kg"></span><span id="DDK_QUERYING_SCSI_PORT_FOR_HARDWARE_INFORMATION_KG"></span>


ストレージクラスドライバーおよびその他の上位レベルのドライバーは、クエリプロパティ要求 ([**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)) を使用して、デバイスの機能とホストバスアダプターの機能に関する情報を SCSI ポートに照会できます。 クエリプロパティ要求は、レガシシステムにおける問い合わせと機能の要求に相当する PnP です ([**ioctl\_scsi\_\_の照会\_データを取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data)し、 [**ioctl\_SCSI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities)\_\_機能を取得します。). 記憶装置の場合、scsi の照会データまたはそれと同等ではない scsi を含む記憶装置記述子 ([**記憶域\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)) が返されます。ホストアダプターの scsi ポートでは、記憶域アダプター記述子が返されます ([**ストレージ\_アダプターの\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor))。機能と制限のデータが含まれています。

上位レベルのドライバーは、クエリのプロパティ要求を使用して、[**ストレージ\_プロパティ\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_property_query)構造を SCSI ポートに渡す必要があります。 上位レベルのドライバーによって、 **QueryType** MEMBER of STORAGE\_プロパティが設定されている場合\_**storageadapterproperty**にクエリを実行すると、SCSI ポートからストレージアダプター記述子が返されます。 上位レベルのドライバーで**QueryType**メンバーが**storagedeviceproperty**に設定されている場合、SCSI ポートは記憶装置記述子を返します。

上位レベルのドライバーが、 **QueryType**が**storagedeviceproperty**に設定されているアダプターの FDO にクエリプロパティ request IRP を送信すると、SCSI ポートが irp に失敗します。 クラスドライバーが、 **QueryType**が**storageadapterproperty**に設定されたデバイスの PDO にこの irp を送信する場合、SCSI ポートは irp をアダプター FDO に転送します。

ストレージデバイス記述子とストレージアダプター記述子の詳細については、[ストレージクラスドライバーの GetDescriptor ルーチン](storage-class-driver-s-getdescriptor-routine.md)に関するページと、STORAGE [ **\_プロパティ\_QUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_property_query)、 [**storage\_のリファレンスページを参照してください。デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)、および[**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)。

 

 




