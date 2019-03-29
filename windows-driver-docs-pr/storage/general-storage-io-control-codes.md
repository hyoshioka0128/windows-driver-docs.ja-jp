---
title: 一般的なストレージの I/O 制御コード
description: 一連の標準的なサービスと記憶域デバイスでは頻繁に必要なデバイスの制御コードに付属するについて説明します。
keywords:
- ストレージ ドライバー WDK ストレージ
- wdk CD-ROM のドライバー
- Ioctl WDK CD-ROM
ms.date: 12/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: a88d7928de2e519f2bb7bdc11462053aa29b5a64
ms.sourcegitcommit: a678a339f09fbd56a3a6124c0fe86194fedb2ed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2019
ms.locfileid: "57560626"
---
# <a name="general-storage-io-control-codes"></a>一般的なストレージの I/O 制御コード

さまざまな種類の記憶装置には、多くの場合、同じサービスが必要です。 デバイスの種類ごとにこれらのサービスを提供する IOCTL 要求を複製するのではなく、このセクションでは、一連の標準的なサービスと記憶域デバイスでは頻繁に必要なデバイスの制御コードに付属するを定義します。 ここで定義されている I/O 制御コードがあるフォーム IOCTL_STORAGE_*XXX*と置き換え、IOCTL_*DeviceType_XXX*制御コード、場所*DeviceType*されたディスク、テープ、またはCD-ROM ドライブです。 たとえば、 **IOCTL_STORAGE_RESERVE**置き換えます**IOCTL_DISK_RESERVE**、 **IOCTL_TAPE_RESERVE**、および**IOCTL_CDROM_RESERVE**します。 IOCTL_STORAGE_*XXX*制御コードは、以前のディスク、テープ、および CD-ROM コードとして関数のコード、転送方法、および必要なアクセス権と同じ値を持つこと。 唯一の違いは、デバイスの種類です。

記憶域クラス ドライバーが、これらの要求の一部を開始しますが、通常はアプリケーションです。 記憶域クラス ドライバーは、ストレージ デバイスの種類に応じて、これらの要求の一部またはすべてを処理する必要があります。 記憶域クラス ドライバーが存在しない場合、アプリケーションは、ポート ドライバーに直接、要求を行うことがあります。

|IOCTL|説明|
|----|----|
|[IOCTL_STORAGE_BREAK_RESERVATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_break_reservation)|ディスクの予約を分割します。|
|[IOCTL_STORAGE_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_check_verify)|呼び出し元が読み取りまたは書き込みアクセス用に開かれているリムーバブル メディア デバイスでメディアが変更されたかどうかを判断します。|
|[IOCTL_STORAGE_CHECK_VERIFY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_check_verify2)|メディアがリムーバブル メディア デバイスで変更されたかどうか、-で呼び出し元が開かれて決定**FILE_READ_ATTRIBUTES**します。|
|[IOCTL_STORAGE_DEVICE_POWER_CAP](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_device_power_cap)|記憶域デバイスに対する動作可能な最大電力消費レベルを指定します。|
|[IOCTL_STORAGE_EJECT_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_eject_media)|により、デバイスの取り出し機能をサポートしている場合は、メディアを取り出すデバイス。|
|[IOCTL_STORAGE_EJECTION_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_ejection_control)|メディアの削除を防ぐためにデバイスをロックします。|
|[IOCTL_STORAGE_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_find_new_devices)|システムが起動されてから、または最後に、ドライバーは、この要求を処理するために、ドライバーがサポートする別のデバイスが I/O バスに接続されたかどうかを判断します。|
|[IOCTL_STORAGE_FIRMWARE_ACTIVATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_firmware_activate)|記憶域デバイスのファームウェア イメージをアクティブにします。|
|[IOCTL_STORAGE_FIRMWARE_DOWNLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_firmware_download)|ストレージ デバイスにファームウェア イメージをダウンロードするが、有効にはなりません。|
|[IOCTL_STORAGE_FIRMWARE_GET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_firmware_get_info)|詳細なファームウェアの情報のストレージ デバイスを照会します。|
|[IOCTL_STORAGE_GET_DEVICE_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_device_number)|返します、 **STORAGE_DEVICE_NUMBER** FILE_DEVICE_XXX を含む構造体型、デバイスの数、および、分割可能なデバイス、デバイスが開始されると、ドライバーによって、デバイスに割り当てられているパーティション番号。|
|[IOCTL_STORAGE_GET_HOTPLUG_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_hotplug_info)|指定したデバイスのホットプラグ構成を取得します。|
|[IOCTL_STORAGE_GET_LB_PROVISIONING_MAP_RESOURCES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_lb_provisioning_map_resources)|**IOCTL_STORAGE_GET_LB_PROVISIONING_MAP_RESOURCES**要求は、記憶装置にマッピングが使用可能で使用されるリソースを決定する記憶域クラス ドライバーに送信されます。|
|[IOCTL_STORAGE_GET_MEDIA_SERIAL_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_media_serial_number)|USB の一般的な親ドライバーを USB デバイスのシリアル番号を照会します。|
|[IOCTL_STORAGE_GET_MEDIA_TYPES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_media_types)|フロッピー ディスク ドライブのジオメトリに関する情報を返します。|
|[IOCTL_STORAGE_GET_MEDIA_TYPES_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_media_types_ex)|デバイスでサポートされているメディアの種類に関する情報を返します。|
|[IOCTL_STORAGE_GET_PHYSICAL_ELEMENT_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_physical_element_status)|**IOCTL_STORAGE_GET_PHYSICAL_ELEMENT_STATUS**制御コードを照会して、デバイスから物理的な要素の状態を返します。|
|[IOCTL_STORAGE_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_load_media)|呼び出し元が読み取りまたは書き込みアクセス用に開かれているデバイスに読み込まれるメディアをによりします。|
|[IOCTL_STORAGE_LOAD_MEDIA2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_load_media2)|メディアで、呼び出し元が開かれているデバイスに読み込まれると、 **FILE_READ_ATTRIBUTES**します。|
|[IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_manage_data_set_attributes)|これは、 **IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES**要求を使用して、記憶域デバイスに管理データ セットの属性要求を送信します。|
|[IOCTL_STORAGE_MCN_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_mcn_control)|一時的に有効またはカスタムの PnP イベントの配信を無効に**GUID_IO_MEDIA_ARRIVAL**と**GUID_IO_MEDIA_REMOVAL**リムーバブル メディア デバイスにします。|
|[IOCTL_STORAGE_MEDIA_REMOVAL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_media_removal)|メディアの削除を防ぐためにデバイスをロックします。|
|[IOCTL_STORAGE_PERSISTENT_RESERVE_IN](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_persistent_reserve_in)|汎用記憶域クラス ドライバー (classpnp.sys) は、永続的な予約のコマンドを発行するための I/O 制御 (IOCTL) インターフェイスを公開します。|
|[IOCTL_STORAGE_PERSISTENT_RESERVE_OUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_persistent_reserve_out)|汎用記憶域クラス ドライバー (classpnp.sys) は、永続的な予約 Out コマンドを発行するための I/O 制御 (IOCTL) インターフェイスを公開します。|
|[IOCTL_STORAGE_PREDICT_FAILURE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_predict_failure)|デバイスの障害の予測をポーリングします。|
|[IOCTL_STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)|ドライバーを使用できる**IOCTL_STORAGE_PROTOCOL_COMMAND**記憶装置にベンダー固有のコマンドを渡す|
|[IOCTL_STORAGE_QUERY_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)|ドライバーを使用できる**IOCTL_STORAGE_QUERY_PROPERTY**をストレージ デバイスまたはアダプターのプロパティを返します。|
|[IOCTL_STORAGE_READ_CAPACITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_read_capacity)|**IOCTL_STORAGE_READ_CAPACITY**要求は、ターゲット記憶域デバイスの読み取り能力の情報を返します。|
|[IOCTL_STORAGE_REINITIALIZE_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_reinitialize_media)|ドライバーを使用できる、 **IOCTL_STORAGE_REINITIALIZE_MEDIA**デバイスの消去/再初期化するコードを制御します。|
|[IOCTL_STORAGE_RELEASE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_release)|複数のイニシエーターをサポートするバスの呼び出し元が排他的に使用し、SCSI バスなどのデバイスの予約の概念を以前に予約されたデバイスを解放します。|
|[IOCTL_STORAGE_RESERVE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_reserve)|複数のイニシエーターをサポートするバスの呼び出し元が排他的に使用し、SCSI バスなどのデバイスの予約の概念のデバイスを要求します。|
|[IOCTL_STORAGE_RESET_BUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_reset_bus)|I/O バスと間接的には、バス上の各デバイスをリセットします。|
|[IOCTL_STORAGE_RESET_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_reset_device)|可能であれば、バス上の他のデバイスに影響を与えずに、非 SCSI 記憶域デバイスをリセットします。|
|[IOCTL_STORAGE_SET_HOTPLUG_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_set_hotplug_info)|指定したデバイスのホットプラグ構成を設定します。|
|[IOCTL_STORAGE_SET_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_set_property)|プロパティを変更する要求が成功したかどうかを示します。 またはエラーが発生します。
|[IOCTL_STORAGE_SET_TEMPERATURE_THRESHOLD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_set_temperature_threshold)|ドライバーを使用できる**IOCTL_STORAGE_SET_TEMPERATURE_THRESHOLD** (ハードウェアでサポートされている) 場合は、ストレージ デバイスの温度のしきい値を設定します。|