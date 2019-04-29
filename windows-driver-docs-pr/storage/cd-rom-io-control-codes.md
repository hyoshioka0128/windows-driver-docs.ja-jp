---
title: CD-ROM I/O 制御コード
description: Cd-rom クラス ドライバーは、追加パブリック I/O 制御コード、このトピックで説明を処理します。
keywords:
- CD-ROM ドライバー WDK ストレージ
- Ioctl WDK CD-ROM
ms.date: 12/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8dbff0e504ed489843bba098ceaba315ecaa7b4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338368"
---
# <a name="cd-rom-io-control-codes"></a>CD-ROM I/O 制御コード

パブリックのすべての I/O 制御コードが CD-ROM デバイスのドライバーでは、バッファー内の I/O を使用します。 その結果、入力または出力データは、これらの要求を Irp で]-> [AssociatedIrp.SystemBuffer します。

Cd-rom クラス ドライバーは処理追加パブリック I/O 制御コード、このセクションで説明したものとします。 記憶域クラス ドライバーの要件の詳細については、次を参照してください。[全般ストレージ I/O 制御コード](general-storage-io-control-codes.md)します。

|I/O 制御コード|説明|
|----|----|
|[IOCTL_CDROM_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_check_verify)|この IOCTL が置き換え[IOCTL_STORAGE_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_check_verify)します。 2 つの Ioctl の唯一の違いは、基本値です。|
|**IOCTL_CDROM_CLOSE_DOOR**|この I/O 制御コードは置き換えられました[IOCTL_STORAGE_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_load_media)します。|
|[IOCTL_CDROM_ENABLE_STREAMING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)|有効または cd-rom ドライブ ハンドルごとにモードを生の読み取りおよび書き込み要求のストリーミングを無効にします。 この操作を実行するには、呼び出し、 **DeviceIoControl**関数を指定、 **IOCTL_CDROM_ENABLE_STREAMING**として I/O コントロール要求、 *dwIoControlCode*パラメーター。|
|[IOCTL_CDROM_EXCLUSIVE_ACCESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)|CD-ROM デバイスのアクセスの状態をエクスポート、CD-ROM デバイスへの排他アクセスをロックおよび排他アクセスの CD-ROM デバイスのロック解除には、CD-ROM クラス ドライバーに指示します。|
|[IOCTL_CDROM_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_find_new_devices)|この IOCTL が置き換え[IOCTL_STORAGE_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_find_new_devices)します。 2 つの Ioctl の唯一の違いは、基本値です。|
|[IOCTL_CDROM_GET_CONFIGURATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_configuration)|CD-ROM デバイスから機能とプロファイルの情報を要求します。|
|[IOCTL_CDROM_GET_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_control)|この IOCTL 要求は廃止されています。 使わないでください。|
|[IOCTL_CDROM_GET_DRIVE_GEOMETRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_drive_geometry)|CD-ROM のジオメトリ (メディアの種類、シリンダー数、シリンダーあたりのトラック、トラック、あたりのセクターとセクターあたりのバイト数) に関する情報を返します。|
|[IOCTL_CDROM_GET_DRIVE_GEOMETRY_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_drive_geometry_ex)|CD-ROM のジオメトリ (メディアの種類、シリンダー数、シリンダーあたりのトラック、トラック、あたりのセクターとセクターあたりのバイト数) に関する情報を返します。|
|[IOCTL_CDROM_GET_INQUIRY_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_inquiry_data)|CD-ROM デバイスの SCSI 問い合わせデータを返します。 デバイスが排他的にロックをされている場合、この IOCTL を使用できます[IOCTL_CDROM_EXCLUSIVE_ACCESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)します。|
|[IOCTL_CDROM_GET_LAST_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_last_session)|最初の完全なセッション数、最後の完全なセッション数、および最後の完全なセッションの開始アドレスのデバイスを照会します。|
|[IOCTL_CDROM_GET_PERFORMANCE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance)|デバイスから、サポートされている速度を取得します。 **IOCTL_CDROM_GET_PERFORMANCE** I/O 制御要求は、MMC のコマンドを取得のパフォーマンス上のラッパーです。|
|[IOCTL_CDROM_GET_VOLUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_volume)|使われていません。 各デバイスのオーディオ ポートを現在のボリュームを決定します。|
|[IOCTL_CDROM_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_load_media)|ドライブに戻る protruding CD-ROM トレイを描画します。|
|[IOCTL_CDROM_PAUSE_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_pause_audio)|使われていません。 オーディオ再生を中断します。|
|[IOCTL_CDROM_PLAY_AUDIO_MSF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_play_audio_msf)|使われていません。 指定されたメディアの範囲を再生します。|Raw モードで CD-ROM からのデータを読み取ります。|
|[IOCTL_CDROM_READ_Q_CHANNEL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_q_channel)|使われていません。 現在の位置、メディアのカタログ、または ISRC 追跡データを返します。|
|[IOCTL_CDROM_READ_TOC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_toc)|使われていません。 メディアの内容の一覧を返します。|
|[IOCTL_CDROM_READ_TOC_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_toc_ex)|目次 (TOC)、プログラムのメモリ領域 (PMA) および pregroove (ATIP) の絶対時間のターゲット デバイスを照会します。|
|[IOCTL_CDROM_RESUME_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_resume_audio)|使われていません。 中断されたオーディオの操作を再開します。|
|[IOCTL_CDROM_SEEK_AUDIO_MSF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_seek_audio_msf)|使われていません。 メディアの指定、MSF にヘッドを移動します。|
|[IOCTL_CDROM_SEND_OPC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)|ファイル システムとストリーミングの最初の書き込みが完了する手順については待機する必要があるないように、事前に最適な電源の調整 (OPC) の手順を実行するその他の実装で使用されます。|
|[IOCTL_CDROM_SET_SPEED](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)|CD-ROM ドライブのスピンドルの速度を設定します。|
|[IOCTL_CDROM_SET_VOLUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_volume)|使われていません。 デバイスのオーディオ ポートのボリュームをリセットします。|
|[IOCTL_CDROM_STOP_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_stop_audio)|使われていません。 オーディオ再生を終了します。|
