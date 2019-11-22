---
title: 既存の SCSI クラス ドライバーをプラグ アンド プレイ対応に変換
description: 既存の SCSI クラス ドライバーをプラグ アンド プレイ対応に変換
ms.assetid: b6570eef-f425-4b73-aa8a-7084f53bb10a
keywords:
- ストレージクラスドライバー WDK、SCSI クラスドライバーの変換
- クラスドライバー WDK storage、SCSI クラスドライバーの変換
- ストレージクラスドライバー WDK、PnP
- クラスドライバー WDK storage、PnP
- PnP WDK ストレージ
- WDK ストレージのプラグアンドプレイ
- SCSI クラスドライバーの変換
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09c2d3e4f278870aa9a7be39906ec26189b3e624
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844580"
---
# <a name="converting-an-existing-scsi-class-driver-for-plug-and-play"></a>既存の SCSI クラス ドライバーをプラグ アンド プレイ対応に変換


## <span id="ddk_converting_an_existing_scsi_class_driver_for_plug_and_play_kg"></span><span id="DDK_CONVERTING_AN_EXISTING_SCSI_CLASS_DRIVER_FOR_PLUG_AND_PLAY_KG"></span>


PnP ドライバーとして正常に実行するには、既存の SCSI クラスドライバーを次のように変更する必要があります。

-   ドライバー初期化コードは、プラグアンドプレイドライバーを初期化するための規則に従う必要があります。 既存の SCSI ドライバーの**driverentry**ルーチンの機能は、記憶域クラスドライバーの**driverentry**、 *AddDevice*、 *DispatchPnP*の各ルーチンに分かれています。詳細については、「ストレージクラス[ドライバーの Driverentry ルーチン](storage-class-driver-s-driverentry-routine.md)」、「ストレージ[クラスドライバーの AddDevice ルーチン](storage-class-driver-s-adddevice-routine.md)」、「[ストレージクラスドライバーでの PnP 開始の処理](handling-pnp-start-in-a-storage-class-driver.md)」を参照してください。

-   SRBs をビルドするコードでは、 **PathId**、 **Targetid**、および**Lun**フィールドをターゲットデバイスアドレスに設定することはできません。これらのフィールドを0xff に初期化する必要があります。 デバイスアドレスは、PDO では暗黙的にデバイスを表し、ドライバーはそのようなデバイスオブジェクトとのみ通信する必要があるため、クラスドライバーがデバイスアドレスを指定する必要はありません。

-   Scsi\_scsi を発行することによって SCSI の照会と機能のデータを取得するコード[ **\_\_の照会\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_inquiry_data)の取得と ioctl\_の\_の[**取得\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_get_capabilities)の要求は ioctl を発行する必要があり[ **\_ストレージ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)は、代わりにデバイスとアダプターの記述子を取得するためのプロパティ要求\_クエリを実行します。

-   ドライバーは、デバイスを開始、停止、および削除するための PnP 要求を処理する必要があります。また、データ転送やシステム操作を妨害する場合は、このような要求を失敗させるメカニズムが必要です。 たとえば、ドライバーは、そのデバイスにシステムページファイルが含まれている場合、クエリ削除、クエリ停止、または停止要求を失敗させる必要があります。 このようなドライバーでは、ポケットベルによる通知要求を処理する必要があります (IRP\_MJ\_、 [**irp\_\_により、デバイス\_使用\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)と通知の種類、 **Device使用 typepaging**) を保持します。デバイス上のページファイル。

-   ドライバーは、デバイスの電源状態を変更するための要求を処理する必要があります (IRP\_MJ\_、Irp\_によって[ **\_クエリ\_パワー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)と[**IRP\_\_電力を設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)\_)、およびは、電源状態遷移中にデバイスへの i/o をブロックする必要があります。

 

 




