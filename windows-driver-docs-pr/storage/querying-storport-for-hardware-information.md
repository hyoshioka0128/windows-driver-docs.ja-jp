---
title: Storport へのハードウェア情報のクエリ
description: Storport へのハードウェア情報のクエリ
ms.assetid: 1e807e42-d03f-44be-a0a4-8187e2d5667a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df73a2ff4d6406868b7274bfbffc758c30af196b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842719"
---
# <a name="querying-storport-for-hardware-information"></a>Storport へのハードウェア情報のクエリ


ストレージクラスドライバーおよびその他の上位レベルのドライバーは、クエリプロパティ要求 ([**IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)) を使用して、デバイスの機能とホストバスアダプターの機能に関する情報を Storport に照会できます。 クエリプロパティ要求は、レガシシステムにおける問い合わせと機能の要求に相当する PnP です ([**ioctl\_scsi\_\_の照会\_データを取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data)し、 [**ioctl\_SCSI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities)\_\_機能を取得します。). 記憶装置の場合、Storport は SCSI の問い合わせデータまたはそれと同等でない scsi を含む記憶装置記述子 ([**記憶域\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)) を返し、ホストアダプターの場合はストレージアダプター記述子を返します ([**ストレージ\_アダプターの\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor))。機能と制限のデータが含まれています。

上位レベルのドライバーは、クエリプロパティ要求を使用して、[**ストレージ\_プロパティ\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_property_query)構造を Storport に渡す必要があります。 上位レベルのドライバーによって、 **PropertyId** Member of **storage\_プロパティ**が設定されている場合\_**storageadapterproperty**にクエリを実行すると、Storport によってストレージアダプター記述子が返されます。 上位レベルのドライバーで**PropertyId**メンバーが**storagedeviceproperty**に設定されている場合、Storport は記憶装置記述子を返します。

上位レベルのドライバーが、 **PropertyId**が**storagedeviceproperty**に設定されているアダプターの FDO にクエリプロパティ request IRP を送信した場合、Storport は IRP を失敗させることになります。 クラスドライバーが、 **PropertyId**が**storageadapterproperty**に設定されているデバイスの PDO にこの irp を送信する場合、Storport は irp をアダプター FDO に転送します。

ストレージデバイス記述子とストレージアダプター記述子の詳細については、[ストレージクラスドライバーの GetDescriptor ルーチン](storage-class-driver-s-getdescriptor-routine.md)に関するページと、STORAGE [ **\_プロパティ\_QUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_property_query)、 [**storage\_のリファレンスページを参照してください。デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)、および[**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)。

 

 




