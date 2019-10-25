---
title: CD-ROM リアルタイム ストリーミング
description: ストリーミング (リアルタイムストリーミング) は、光ドライブによって提供される機能であり、高速な読み取りおよび書き込み要求を可能にします。
ms.assetid: A4093485-076A-4414-A3D2-9285B2AC097B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 585c02a4a388528122707f5650561375c2016324
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841628"
---
# <a name="span-idstoragecd-rom_real-time_streaming_spancd-rom-real-time-streaming"></a><span id="storage.cd-rom_real-time_streaming_"></span>CD-ROM のリアルタイムストリーミング


ストリーミング (リアルタイムストリーミング) は、光ドライブによって提供される機能であり、高速な読み取りおよび書き込み要求を可能にします。 Windows 7 以降、DVD ビデオのストリーミングのサポートは、ストレージスタックのすべてのレイヤー (たとえば、UDF ファイルシステムドライバー、Udf .sys、ビデオ再生サブシステムを含む) から Windows Media Player に実装されています。

## <a name="span-idabout_real-time_streaming_spanspan-idabout_real-time_streaming_spanspan-idabout_real-time_streaming_spanabout-real-time-streaming"></a><span id="About_real-time_streaming_"></span><span id="about_real-time_streaming_"></span><span id="ABOUT_REAL-TIME_STREAMING_"></span>リアルタイムストリーミングについて


一般に、光学メディアへの読み取り/書き込みアクセスには、信頼性と継続パフォーマンスの2つの特性があります。 これらのプロパティは相互に依存しており、同時に最大化することはできません (高い信頼性を実現するため、パフォーマンスが低下します)。

光学メディア用のアプリケーションの大部分は、信頼性 (つまり、データの整合性) に重点を置いています。 ただし、DVD レコーダーやデジタルビデオビデオカメラなどの特定のアプリケーションは、継続的なパフォーマンスを重視し、適切な操作のために一定レベルのデータスループットを必要とします。 仕様により、これらのアプリケーションは合理的なデータ損失に対する回復性を備えています (たとえば、ビデオコーデックでは、一部のフレームが失われる可能性があると仮定しています)。 これらのアプリケーションでは、信頼性が最高の優先順位ではありません。 光学ドライブは、特別な (いわゆるリアルタイムストリーミング) モードの操作を提供することによって、このニーズに対処します。 このモードのパフォーマンスを向上させるには、読み取りまたは書き込みエラーが無視され、ドライブは再試行やエラーの修正や防止を実行しません。

## <a name="span-iddeveloper_support_for_real-time_streaming_in_windowsspanspan-iddeveloper_support_for_real-time_streaming_in_windowsspanspan-iddeveloper_support_for_real-time_streaming_in_windowsspandeveloper-support-for-real-time-streaming-in-windows"></a><span id="Developer_support_for_real-time_streaming_in_Windows"></span><span id="developer_support_for_real-time_streaming_in_windows"></span><span id="DEVELOPER_SUPPORT_FOR_REAL-TIME_STREAMING_IN_WINDOWS"></span>Windows でのリアルタイムストリーミングの開発者サポート


Windows 7 以降では、CD-ROM クラスドライバーである Cdrom は、低レベルのストリーミングの読み取りおよび書き込み要求 (MMC 仕様の READ12/WRITE12 コマンド) をサポートしています。 ユーザーモードアプリケーションでは、 [**ioctl\_CDROM\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)使用して\_streaming i/o 制御コード (ioctl) を有効にし、生の読み取り要求と書き込み要求のストリーミングを有効または無効にすることができます。 これらの読み取り要求と書き込み要求は、未加工の CD/DVD-ROM デバイス用に開かれたハンドルを使用して実行されます。

さらに、カーネルモードのコンポーネントの場合は、 [**MJ が irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read) MJ を処理する方法が変更されています。\_READ および[**irp\_\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求です。 クラスドライバーは、リアルタイムストリーミング要求がデバイスの機能を満たしているかどうかを検証します。 この機能を実装するために、Windows 7 では、ドライバーの[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)に、のストリーミングフラグ、 **SL\_リアルタイム\_ストリーム**が導入されました。 このフラグは、すべてのストリーミング読み取り要求または書き込み要求に対してアサートされ、すべての非ストリーミング要求に対して消去されます。

ストレージドライバースタックでのこれらの変更により、より高いレイヤー (特にファイルシステムのドライバーとアプリケーション) が、リアルタイムデータを含むファイルに対して保証された速度で読み取り/書き込み操作を実行できるようになります。 Windows 7 以降では、 [**FSCTL\_マーク**](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_mark_handle)を使用してファイルをリアルタイムストリーミング用にマークすることができます。これを行うには、コントロールコードを処理\_、マーク **\_ハンドル\_リアル**タイムフラグを設定してストリーミングモードを指定し[ **\_\_情報**](https://docs.microsoft.com/windows/desktop/api/winioctl/ns-winioctl-mark_handle_info)構造体を処理します。

図1は、通常の読み取りと書き込みの要求と、UDF ファイルシステムと CDROM クラスのドライバーの関係を示しています。

![図 1: cdrom および udf のリアルタイムストリーミングのサポート](images/cdromstreaming.png)

DVD 再生アプリケーションとファイルシステムドライバーでは、Ioctl を使用して、Cdrom (最下位レベル) の未加工のストリーミングサポートにアクセスするか、またはファイルシステムのサポートを使用して、Udf に導入されたストリーミングモードをサポートするかを選択できます。 アプリケーションには、Windows video 再生サブシステム全体を含めることもできます。 また、Cd-rom とファイルシステムのレイヤーは、再生に加えて、ストリーミング記録もサポートしています。

## <a name="span-idverifying_device_support_for_real-time_streaming_using_ioctlsspanspan-idverifying_device_support_for_real-time_streaming_using_ioctlsspanspan-idverifying_device_support_for_real-time_streaming_using_ioctlsspanverifying-device-support-for-real-time-streaming-using-ioctls"></a><span id="Verifying_device_support_for_real-time_streaming_using_IOCTLs"></span><span id="verifying_device_support_for_real-time_streaming_using_ioctls"></span><span id="VERIFYING_DEVICE_SUPPORT_FOR_REAL-TIME_STREAMING_USING_IOCTLS"></span>Ioctl を使用したリアルタイムストリーミングのデバイスサポートの検証


-   [**IOCTL\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_configuration)を使用して\_構成を取得し、ストリーミング機能が存在し、最新のものかどうかを確認します。

## <a name="span-idenabling_or_disabling_real-time_streaming_using_ioctlsspanspan-idenabling_or_disabling_real-time_streaming_using_ioctlsspanspan-idenabling_or_disabling_real-time_streaming_using_ioctlsspanenabling-or-disabling-real-time-streaming-using-ioctls"></a><span id="Enabling_or_disabling_real-time_streaming_using_IOCTLs"></span><span id="enabling_or_disabling_real-time_streaming_using_ioctls"></span><span id="ENABLING_OR_DISABLING_REAL-TIME_STREAMING_USING_IOCTLS"></span>Ioctl を使用したリアルタイムストリーミングの有効化または無効化


-   [**IOCTL\_CDROM\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)使用して\_streaming i/o 制御コードを有効にし、生の読み取り要求と書き込み要求のストリーミングモードを有効または無効にします。 この IOCTL は出力パラメーターを持たず、 [**CDROM\_STREAMING\_制御**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_streaming_control)構造を入力パラメーターとしてサポートしています。

    この IOCTL は、ハンドルごとにストリーミングモードを有効または無効にします。 既定では、新しく開かれたすべての未処理の CD-ROM ハンドルに対して、ストリーミングは無効になっています。 ファイルシステムを使用せず、生データを操作する再生アプリケーションでは、同じデバイスに対して2つのファイルハンドルを開く必要があります。1つはファイルシステムメタデータ用で、もう1つはリアルタイムファイル用のストリーミングです。

## <a name="span-idspecifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requestsspanspan-idspecifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requestsspanspan-idspecifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requestsspanspecifying-real-time-streaming-for-irp_mj_read-and-irp_mj_write-requests"></a><span id="Specifying_real-time_streaming_for_IRP_MJ_READ_and_IRP_MJ_WRITE_requests"></span><span id="specifying_real-time_streaming_for_irp_mj_read_and_irp_mj_write_requests"></span><span id="SPECIFYING_REAL-TIME_STREAMING_FOR_IRP_MJ_READ_AND_IRP_MJ_WRITE_REQUESTS"></span>IRP\_MJ\_READ および IRP\_MJ のリアルタイムストリーミングの指定\_書き込み要求


-   [**IogetMJ Enti Stacklocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)(irp)-&gt;Flags フィールドの SL\_リアルタイム\_ストリームフラグは、読み取りおよび書き込みのストリーミング要求 ([**irp\_\_read**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read)および[**Irp\_MJ\_write**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write)) を制御します. フラグは、すべてのストリーミング読み取りおよび書き込み要求に対して設定され、すべての非ストリーミング要求に対して消去されます。 SL\_リアルタイム\_ストリームフラグが設定されている場合、READ12 および WRITE12 scsi コマンドを使用して、READ10 または WRITE10 SCSI コマンドではなく、ストリーミング要求が実行されます。 SL\_のリアルタイム\_ストリームフラグが IRP で設定されているにもかかわらず、デバイスが現在挿入されているメディアのストリーミングをサポートしていない場合、IRP は、状態コードの状態\_無効\_デバイス\_要求で拒否されます。

## <a name="span-idspecifying_real-time_streaming_for_a_file_using_fsctlsspanspan-idspecifying_real-time_streaming_for_a_file_using_fsctlsspanspan-idspecifying_real-time_streaming_for_a_file_using_fsctlsspanspecifying-real-time-streaming-for-a-file-using-fsctls"></a><span id="Specifying_real-time_streaming_for_a_file_using_FSCTLs"></span><span id="specifying_real-time_streaming_for_a_file_using_fsctls"></span><span id="SPECIFYING_REAL-TIME_STREAMING_FOR_A_FILE_USING_FSCTLS"></span>FSCTLs を使用してファイルのリアルタイムストリーミングを指定する


-   ファイルの種類に関係なく、任意のファイルにリアルタイムの読み取り動作をマークすることができます。 これを行うには[ **\_INFO 構造体\_ハンドル**](https://docs.microsoft.com/windows/desktop/api/winioctl/ns-winioctl-mark_handle_info) **\_リアルタイム**フラグとしてマーク\_ハンドルを設定し、 [**FSCTL\_mark\_handle**](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_mark_handle)コントロールコードを送信します。 このフラグでマークされたファイルは、バッファーなしの i/o に対して開く必要があります。
-   以前にリアルタイムの動作のフラグが設定されていたファイルのマークを解除するには、マーク\_ハンドルを設定して、\_INFO 構造体\_ハンドルに **\_リアル**タイムの\_を設定します。
-   FSCTL\_MARK\_ハンドル制御コードがマーク\_ハンドル\_リアルタイムで送信され、CD-ROM/DVD ドライブまたはメディアによってリアルタイムストリーミング機能がサポートされていないことが示されている場合、IOCTL は状態\_無効\_を返しデバイス\_要求。 ハンドルがバッファリングなしで開かれている場合は、状態\_無効\_デバイス\_要求も返されます。

## <a name="span-idperforming_optimum_power_calibration__opc__before_writingspanspan-idperforming_optimum_power_calibration__opc__before_writingspanspan-idperforming_optimum_power_calibration__opc__before_writingspanperforming-optimum-power-calibration-opc-before-writing"></a><span id="Performing_Optimum_Power_Calibration__OPC__before_writing"></span><span id="performing_optimum_power_calibration__opc__before_writing"></span><span id="PERFORMING_OPTIMUM_POWER_CALIBRATION__OPC__BEFORE_WRITING"></span>書き込み前に最適な電力調整 (OPC) を実行する


一部のアプリケーションでは、最初のストリーミング書き込みで OPC が終了するまで待機する必要がないように、事前に OPC プロシージャを実行することが必要になる場合があります。 これを行うために、Cdrom は Ioctl\_CDROM と呼ばれる IOCTL を提供し、 [ **\_OPC\_情報を送信\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)ます。

## <a name="span-iddetermining_the_read_write_speed_for_the_drivespanspan-iddetermining_the_read_write_speed_for_the_drivespanspan-iddetermining_the_read_write_speed_for_the_drivespandetermining-the-readwrite-speed-for-the-drive"></a><span id="Determining_the_read_write_speed_for_the_drive"></span><span id="determining_the_read_write_speed_for_the_drive"></span><span id="DETERMINING_THE_READ_WRITE_SPEED_FOR_THE_DRIVE"></span>ドライブの読み取り/書き込み速度を決定する


MMC の仕様では、アプリケーションで、ストリーミング i/o を使用する前に推奨される読み取り速度と書き込み速度を示すことを推奨しています。これにより、読み取りと書き込みの品質とスループットのバランスを取ることができます。 アプリケーションでは、 [**IOCTL\_CDROM\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)使用して\_速度を設定して、優先速度を示すことができます。 Windows 7 では、ドライブのサポートされている機能を確認するために、\_のパフォーマンス制御コードを取得するために、cdrom [ **\_パフォーマンス\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_performance_request)構造を入力として使用する[**IOCTL\_cdrom\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance)導入されました。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[ **\_ストリーミングを有効にするために、IOCTL\_CDROM\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_enable_streaming)  
[**IOCTL\_CDROM\_\_のパフォーマンスを得る**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_get_performance)  
[**IOCTL\_CDROM\_\_OPC\_情報を送信する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_send_opc_information)  
[**IOCTL\_CDROM\_設定\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)  
[**FSCTL\_マーク\_ハンドル**](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-fsctl_mark_handle)  
[ **\_情報をマーク\_ハンドル**](https://docs.microsoft.com/windows/desktop/api/winioctl/ns-winioctl-mark_handle_info)  
[**CDROM\_のパフォーマンス\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_performance_request)  



