---
title: CD-ROM I/O 制御コード
description: CD-ROM デバイス用のクラスドライバーは、このトピックで説明されている追加のパブリック i/o 制御コードを処理します。
keywords:
- CD-ROM ドライバー WDK ストレージ
- Ioctl WDK CD-ROM
ms.date: 12/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0c1fcaabcefc3a78f98b7dd57c8f643bca35aacd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841630"
---
# <a name="cd-rom-io-control-codes"></a>CD-ROM I/O 制御コード

CD-ROM デバイスのドライバーのすべてのパブリック i/o 制御コードは、バッファー i/o を使用します。 そのため、これらの要求の入力データまたは出力データは、Irp-> AssociatedIrp にあります。

CD-ROM デバイス用のクラスドライバーは、このセクションで説明されている追加のパブリック i/o 制御コードを処理します。 ストレージクラスドライバーの要件の詳細については、「[一般的なストレージ I/o 制御コード](general-storage-io-control-codes.md)」を参照してください。

|I/o 制御コード|説明|
|----|----|
|[IOCTL_CDROM_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_check_verify)|この IOCTL は[IOCTL_STORAGE_CHECK_VERIFY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_check_verify)に置き換えられています。 2つの Ioctl の唯一の違いは、基本値です。|
|**IOCTL_CDROM_CLOSE_DOOR**|この i/o 制御コードは[IOCTL_STORAGE_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_load_media)に置き換えられました。|
|[IOCTL_CDROM_ENABLE_STREAMING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)|未処理の読み取り要求と書き込み要求のために、ハンドルごとに CDROM ストリーミングモードを有効または無効にします。 この操作を実行するには、 **DeviceIoControl**関数を呼び出し、 *Dwiocontrolcode*パラメーターとして**IOCTL_CDROM_ENABLE_STREAMING** i/o control 要求を指定します。|
|[IOCTL_CDROM_EXCLUSIVE_ACCESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)|Cd-rom デバイスのアクセス状態をエクスポートするように cd-rom クラスドライバーに指示し、排他アクセス用の CD-ROM デバイスをロックし、CD-ROM デバイスのロックを解除して排他アクセスできるようにします。|
|[IOCTL_CDROM_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_find_new_devices)|この IOCTL は[IOCTL_STORAGE_FIND_NEW_DEVICES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_find_new_devices)に置き換えられています。 2つの Ioctl の唯一の違いは、基本値です。|
|[IOCTL_CDROM_GET_CONFIGURATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_configuration)|CD-ROM デバイスの機能とプロファイル情報を要求します。|
|[IOCTL_CDROM_GET_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_control)|この IOCTL 要求は互換性のために残されています。 使わないでください。|
|[IOCTL_CDROM_GET_DRIVE_GEOMETRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_drive_geometry)|CD-ROM のジオメトリに関する情報を返します (メディアの種類、シリンダー数、シリンダーあたりのトラック、トラックあたりのセクター、セクターあたりのバイト数)。|
|[IOCTL_CDROM_GET_DRIVE_GEOMETRY_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_drive_geometry_ex)|CD-ROM のジオメトリに関する情報を返します (メディアの種類、シリンダー数、シリンダーあたりのトラック、トラックあたりのセクター、セクターあたりのバイト数)。|
|[IOCTL_CDROM_GET_INQUIRY_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_inquiry_data)|CD-ROM デバイスの SCSI 照会データを返します。 この IOCTL は、デバイスが[IOCTL_CDROM_EXCLUSIVE_ACCESS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_exclusive_access)で排他的にロックされている場合に使用できます。|
|[IOCTL_CDROM_GET_LAST_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_last_session)|デバイスに対して、最初の完全なセッション番号、最後に完了したセッション番号、最後に完了したセッションの開始アドレスを照会します。|
|[IOCTL_CDROM_GET_PERFORMANCE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance)|デバイスからサポートされている速度を取得します。 **IOCTL_CDROM_GET_PERFORMANCE** i/o 制御要求は、MMC コマンドのラッパーであり、パフォーマンスを取得します。|
|[IOCTL_CDROM_GET_VOLUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_volume)|使われていません。 デバイスの各オーディオポートの現在のボリュームを確認します。|
|[IOCTL_CDROM_LOAD_MEDIA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_load_media)|Protruding CDROM トレイをドライブに戻します。|
|[IOCTL_CDROM_PAUSE_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_pause_audio)|使われていません。 オーディオ再生を中断します。|
|[IOCTL_CDROM_PLAY_AUDIO_MSF](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_play_audio_msf)|使われていません。 指定されたメディアの範囲を再生します。|Raw モードで CD-ROM からデータを読み取ります。|
|[IOCTL_CDROM_READ_Q_CHANNEL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_q_channel)|使われていません。 現在の位置、メディアカタログ、または ISRC track データを返します。|
|[IOCTL_CDROM_READ_TOC](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_toc)|使われていません。 メディアの内容のテーブルを返します。|
|[IOCTL_CDROM_READ_TOC_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_read_toc_ex)|ターゲットデバイスに対して、目次 (目次)、プログラムのメモリ領域 (PMA)、および pregroove の絶対時間 (列単位) を照会します。|
|[IOCTL_CDROM_RESUME_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_resume_audio)|使われていません。 中断されたオーディオ操作を再開します。|
|[IOCTL_CDROM_SEEK_AUDIO_MSF](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_seek_audio_msf)|使われていません。 メディア上の指定した MSF にヘッドを移動します。|
|[IOCTL_CDROM_SEND_OPC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)|ファイルシステムおよびその他の実装で最適な電力調整 (OPC) の手順を事前に実行する必要がある場合に使用します。これにより、最初のストリーミング書き込みでは、プロシージャが終了するまで待機する必要がなくなります。|
|[IOCTL_CDROM_SET_SPEED](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)|CD-ROM ドライブのスピンドル速度を設定します。|
|[IOCTL_CDROM_SET_VOLUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_volume)|使われていません。 デバイスのオーディオポートのボリュームをリセットします。|
|[IOCTL_CDROM_STOP_AUDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_stop_audio)|使われていません。 オーディオ再生を終了します。|
