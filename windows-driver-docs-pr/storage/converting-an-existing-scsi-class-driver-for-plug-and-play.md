---
title: 既存の SCSI クラス ドライバーをプラグ アンド プレイ対応に変換
description: 既存の SCSI クラス ドライバーをプラグ アンド プレイ対応に変換
ms.assetid: b6570eef-f425-4b73-aa8a-7084f53bb10a
keywords:
- 記憶域クラス ドライバー WDK、SCSI を変換するクラスのドライバー
- SCSI クラス ドライバーの変換クラス ドライバー WDK ストレージ
- 記憶域クラス ドライバー WDK、PnP
- ドライバー WDK の記憶域クラス PnP
- PnP WDK ストレージ
- プラグ アンド プレイ WDK ストレージ
- SCSI クラス ドライバーの変換
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5699ca81b8297f3fbb0eb484eb909a37de804f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392752"
---
# <a name="converting-an-existing-scsi-class-driver-for-plug-and-play"></a>既存の SCSI クラス ドライバーをプラグ アンド プレイ対応に変換


## <span id="ddk_converting_an_existing_scsi_class_driver_for_plug_and_play_kg"></span><span id="DDK_CONVERTING_AN_EXISTING_SCSI_CLASS_DRIVER_FOR_PLUG_AND_PLAY_KG"></span>


PnP ドライバーとして正常に実行するに既存の SCSI クラス ドライバーとしては、次のように変更する必要があります。

-   ドライバーの初期化コードは、プラグ アンド プレイ ドライバーの初期化の規則に従う必要があります。 機能、 **DriverEntry**既存の SCSI ドライバーのルーチンに分割されている、 **DriverEntry**、 *AddDevice*、および*DispatchPnP* 」の説明に従って記憶域クラス ドライバーのルーチン[記憶域クラス ドライバー DriverEntry ルーチン](storage-class-driver-s-driverentry-routine.md)、[記憶域クラス ドライバー AddDevice ルーチン](storage-class-driver-s-adddevice-routine.md)、および[処理、ストレージ クラス ドライバーの PnP 開始](handling-pnp-start-in-a-storage-class-driver.md)します。

-   される Srb をビルドするコードを設定する必要がありますいない**PathId**、 **TargetId**、および**Lun**ターゲット デバイスのアドレスをフィールドおよび 0 xff までこれらのフィールドを初期化する必要があります。 デバイスのアドレスは、デバイスを表す pdo 暗黙的で、ドライバーは、デバイスのアドレスを提供するクラス ドライバーの必要はありませんので、このようなデバイス オブジェクトとのみ通信する必要があります。

-   SCSI の照会と機能のデータを発行して取得するコードを[ **IOCTL\_SCSI\_取得\_照会\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff560509)と[ **IOCTL\_SCSI\_取得\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff560502)要求を発行する必要があります[ **IOCTL\_ストレージ\_クエリ\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff560590)を代わりにデバイスとアダプターの記述子を取得する要求。

-   ドライバーは、開始、停止、およびデバイスを削除する PnP の要求を処理する必要があり、データの転送やシステム操作に支障をきたす処理する場合、このような要求は失敗するためのメカニズムがあります。 たとえば、ドライバーがそのデバイスには、システムのページング ファイルが含まれている場合、クエリの削除、クエリの停止または停止要求を失敗する必要があります。 このようなドライバーがページング通知要求を処理する必要があります (IRP\_MJ\_で PNP [ **IRP\_MN\_デバイス\_使用状況\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841)の通知の種類と**DeviceUsageTypePaging**) デバイス上でページのファイルの数を管理します。

-   ドライバーは、デバイスの電源状態を変更する要求を処理する必要があります (IRP\_MJ\_を含む POWER [ **IRP\_MN\_クエリ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)と[ **IRP\_MN\_設定\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744))、し、デバイスに電源の状態遷移中に I/O をブロックする必要があります。

 

 




