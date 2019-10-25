---
title: 一般的なストレージの I/O 制御コード
description: 記憶装置で頻繁に必要とされる標準サービスとそれに付随するデバイス制御コードのセットについて説明します。
keywords:
- 記憶域ドライバー WDK 記憶域
- wdk CD-ROM ドライバー
- Ioctl WDK CD-ROM
ms.date: 12/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6edb466fa1a980b138f01659d7976a40daaf1d07
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843404"
---
# <a name="general-storage-io-control-codes"></a>一般的なストレージの I/O 制御コード

種類が異なるストレージデバイスは、多くの場合、同じサービスを必要とします。 このセクションでは、デバイスの種類ごとにこれらのサービスを提供する IOCTL 要求を複製するのではなく、一連の標準的なサービスと、記憶装置で頻繁に必要となるデバイス制御コードのセットを定義します。 ここで定義されている i/o 制御コードの形式は IOCTL_STORAGE_*XXX*で、 *(devicetype*が DISK、TAPE、または CDROM である IOCTL_*DeviceType_XXX*制御コードが置き換えられます。 たとえば、 **IOCTL_STORAGE_RESERVE**は、 **IOCTL_DISK_RESERVE**、 **IOCTL_TAPE_RESERVE**、および**IOCTL_CDROM_RESERVE**に置き換えられます。 IOCTL_STORAGE_*XXX*の制御コードの値は、関数コード、転送方法、以前のディスク、テープ、および cd-rom コードと同じです。 唯一の違いはデバイスの種類です。

ストレージクラスドライバーは、これらの要求の一部を開始しますが、通常はそのようなアプリケーションです。 ストレージクラスドライバーは、記憶装置の種類に応じて、これらの要求の一部またはすべてを処理する必要があります。 ストレージクラスドライバーが存在しない場合、アプリケーションはポートドライバーに直接要求を加える可能性があります。

|IOCTL|説明|
|----|----|
|[IOCTL_STORAGE_BREAK_RESERVATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_break_reservation)|ディスク予約を解除します。|
|[IOCTL_STORAGE_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_check_verify)|呼び出し元が読み取りアクセスまたは書き込みアクセス用に開いたリムーバブルメディアデバイス上でメディアが変更されたかどうかを判断します。|
|[IOCTL_STORAGE_CHECK_VERIFY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_check_verify2)|メディアがリムーバブルメディアデバイスで変更されたかどうかを判断します。呼び出し元は**FILE_READ_ATTRIBUTES**を使用して開かれています。|
|[IOCTL_STORAGE_DEVICE_POWER_CAP](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_device_power_cap)|記憶装置の最大操作電力消費レベルを指定します。|
|[IOCTL_STORAGE_EJECT_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_eject_media)|デバイスで取り出し機能がサポートされている場合、デバイスがメディアを取り出すようにします。|
|[IOCTL_STORAGE_EJECTION_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_ejection_control)|メディアが削除されないように、デバイスをロックします。|
|[IOCTL_STORAGE_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_find_new_devices)|システムが起動された後、またはドライバーがこの要求を最後に処理した後に、ドライバーがサポートしている別のデバイスが i/o バスに接続されているかどうかを判断します。|
|[IOCTL_STORAGE_FIRMWARE_ACTIVATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_firmware_activate)|記憶装置のファームウェアイメージをアクティブにします。|
|[IOCTL_STORAGE_FIRMWARE_DOWNLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_firmware_download)|は、ファームウェアイメージをストレージデバイスにダウンロードしますが、ライセンス認証を行いません。|
|[IOCTL_STORAGE_FIRMWARE_GET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_firmware_get_info)|詳細なファームウェア情報を記憶装置に照会します。|
|[IOCTL_STORAGE_GET_DEVICE_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_device_number)|**STORAGE_DEVICE_NUMBER**構造体を返します。これには、FILE_DEVICE_XXX の種類とデバイス番号が含まれ、パーティション分割されたデバイスの場合は、デバイスの起動時にドライバーによってデバイスに割り当てられたパーティション番号が格納されます。|
|[IOCTL_STORAGE_GET_HOTPLUG_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_hotplug_info)|指定されたデバイスの hotplug 構成を取得します。|
|[IOCTL_STORAGE_GET_LB_PROVISIONING_MAP_RESOURCES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_lb_provisioning_map_resources)|**IOCTL_STORAGE_GET_LB_PROVISIONING_MAP_RESOURCES**要求は、ストレージクラスドライバーに送信され、記憶域デバイスで使用可能なマッピングリソースと使用されているマッピングリソースが特定されます。|
|[IOCTL_STORAGE_GET_MEDIA_SERIAL_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_serial_number)|Usb 汎用親ドライバーに USB デバイスのシリアル番号を照会します。|
|[IOCTL_STORAGE_GET_MEDIA_TYPES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_types)|フロッピードライブのジオメトリに関する情報を返します。|
|[IOCTL_STORAGE_GET_MEDIA_TYPES_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_types_ex)|デバイスでサポートされているメディアの種類に関する情報を返します。|
|[IOCTL_STORAGE_GET_PHYSICAL_ELEMENT_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_physical_element_status)|**IOCTL_STORAGE_GET_PHYSICAL_ELEMENT_STATUS**制御コードは、デバイスから物理要素の状態を照会して返します。|
|[IOCTL_STORAGE_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_load_media)|呼び出し元が読み取りアクセスまたは書き込みアクセス用に開いたデバイスにメディアを読み込みます。|
|[IOCTL_STORAGE_LOAD_MEDIA2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_load_media2)|呼び出し元が**FILE_READ_ATTRIBUTES**を使用して開いたデバイスにメディアを読み込みます。|
|[IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_manage_data_set_attributes)|この**IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES**要求は、データセットの属性の管理要求をストレージデバイスに送信するために使用されます。|
|[IOCTL_STORAGE_MCN_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_mcn_control)|リムーバブルメディアデバイスでのカスタム PnP イベント**GUID_IO_MEDIA_ARRIVAL**と**GUID_IO_MEDIA_REMOVAL**の配信を一時的に有効または無効にします。|
|[IOCTL_STORAGE_MEDIA_REMOVAL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_media_removal)|メディアが削除されないように、デバイスをロックします。|
|[IOCTL_STORAGE_PERSISTENT_RESERVE_IN](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_persistent_reserve_in)|汎用ストレージクラスドライバー (classpnp) は、コマンドで永続的な予約を発行するための i/o 制御 (IOCTL) インターフェイスを公開します。|
|[IOCTL_STORAGE_PERSISTENT_RESERVE_OUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_persistent_reserve_out)|汎用ストレージクラスドライバー (classpnp) は、永続的な予約 Out コマンドを発行するための i/o 制御 (IOCTL) インターフェイスを公開します。|
|[IOCTL_STORAGE_PREDICT_FAILURE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_predict_failure)|デバイス障害の予測をポーリングします。|
|[IOCTL_STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)|ドライバーは**IOCTL_STORAGE_PROTOCOL_COMMAND**を使用して、ベンダー固有のコマンドを記憶装置に渡すことができます。|
|[IOCTL_STORAGE_QUERY_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)|ドライバーは、 **IOCTL_STORAGE_QUERY_PROPERTY**を使用して、ストレージデバイスまたはアダプターのプロパティを返すことができます。|
|[IOCTL_STORAGE_READ_CAPACITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_read_capacity)|**IOCTL_STORAGE_READ_CAPACITY**要求は、ターゲットストレージデバイスの読み取り容量に関する情報を返します。|
|[IOCTL_STORAGE_REINITIALIZE_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_reinitialize_media)|ドライバーは、 **IOCTL_STORAGE_REINITIALIZE_MEDIA**制御コードを使用して、デバイスの再初期化/消去を行うことができます。|
|[IOCTL_STORAGE_RELEASE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_release)|複数のイニシエーターをサポートするバス上の呼び出し元を排他的に使用するために予約されていたデバイスを解放します。また、SCSI バスなどのデバイスを予約するという概念もあります。|
|[IOCTL_STORAGE_RESERVE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_reserve)|複数のイニシエーターをサポートするバス上の呼び出し元を排他的に使用するデバイスを要求します。また、SCSI バスなどのデバイスを予約するという概念もあります。|
|[IOCTL_STORAGE_RESET_BUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_reset_bus)|バス上の各デバイスを間接的に、i/o バスをリセットします。|
|[IOCTL_STORAGE_RESET_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_reset_device)|可能な場合は、バス上の他のデバイスに影響を与えずに、SCSI 以外の記憶装置をリセットします。|
|[IOCTL_STORAGE_SET_HOTPLUG_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_set_hotplug_info)|指定されたデバイスの hotplug 構成を設定します。|
|[IOCTL_STORAGE_SET_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_set_property)|プロパティを変更する要求が成功したか、エラーが発生したかを示します。
|[IOCTL_STORAGE_SET_TEMPERATURE_THRESHOLD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_set_temperature_threshold)|ドライバーは、 **IOCTL_STORAGE_SET_TEMPERATURE_THRESHOLD**を使用して、(ハードウェアでサポートされている場合) 記憶装置の温度のしきい値を設定できます。|