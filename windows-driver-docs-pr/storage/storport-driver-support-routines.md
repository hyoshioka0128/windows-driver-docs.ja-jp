---
title: Storport ドライバー サポート ルーチン
description: Storport ミニポート ドライバー ルーチンと SCSI ポート ドライバーの設計および Storport ドライバーの間の相違点について説明します。
ms.assetid: ''
keywords:
- Storport ドライバー サポート ルーチン
- WDK のストレージ
- 記憶域サポート ルーチン
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1fd96a9cbdc562474ea758901e1ec2391ebb9a1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557484"
---
# <a name="storport-driver-support-routines"></a>Storport ドライバー サポート ルーチン

Storport ドライバーで動作するミニポート ドライバーは、このセクションで、日常的な説明の実装を含める必要がありますありを通じてそれらを公開する必要があります、 [HW_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_hw_initialization_data)ミニポート中に構造体ドライバーの初期化フェーズ。 

Storport ミニポート ドライバーのルーチンは、対応する SCSI ポートと同じ多くの点では (を参照してください[SCSI ミニポート ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/storage/required-and-optional-scsi-miniport-driver-routines)詳細については)。 ただし、SCSI ポート ドライバーの設計および Storport ドライバーの重要な違いがあるし、これらのルーチンは、これらの違いに対応する必要があります。 

たとえば、要求のミニポート ドライバーが Storport ドライバーを使用した作業はもう 1 つの I/O を受信する常に準備する必要がありますの後、 [HwStorStartIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)ルーチンが完了しました。 SCSI ポートで動作するミニポート ドライバーは、これを行う必要はありません。 SCSI ポートのバージョンは、ポート ドライバーを明示的に通知するまでに新しい I/O 要求を受信しなかったを使用して、 [StorPortNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportnotification)関数は、別の要求を処理する準備が整っています。 

Storport のバージョンのミニポート ドライバーは、一連のキューの管理機能、SCSI ポートのバージョンには使用できませんが、送信される時に要求を処理できない場合、オーバー ロードを扱うことができます。 SCSI ポート版と同様のミニポート ドライバー、Storport のバージョンを使用して要求が完了すると[SRB_STATUS_BUSY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdevicebusy)、SCSI ポート バージョンとは異なり、StorPortDeviceBusy ルーチンを使用してビジー状態としてデバイスのキューをマークことできますも。 ような関数は、一時停止と再開のアダプター全体で処理するには、ミニポート ドライバーを使用します。

Storport ドライバーによって提供されるサポート ルーチンの詳細については、[Storport ドライバー ルーチンをサポートする] を参照してください。

Storport ドライバーの詳細については、次を参照してください。[ストレージ ポート ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-port-drivers)します。 

次に、Storport ドライバー サポート ルーチンを示します。

| ルーチン  |説明   |
|---|---|
|[HW_MESSAGE_SIGNALED_INTERRUPT_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_message_signaled_interrupt_routine)| メッセージの処理には、割り込み (MSI) が通知されます。 |
|[HW_ADAPTER_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_adapter_control)|ミニポート ドライバーの**HwStorAdapterControl**状態または停止や電源管理の HBA の再起動など、アダプターの動作を制御する同期操作を実行するルーチンが呼び出されます。|
|[HW_BUILDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)|**HwStorBuildIo**ルーチンに渡す前にシステムの共有データ構造体に同期されていないアクセス権を持つ SRB を処理する[HwStorStartIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)します。|
|[HW_DPC_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_dpc_routine)|**HwStorDpcRoutine**ルーチンが遅延プロシージャ呼び出し (DPC) のメカニズムを使用してディスパッチ IRQL での実行が遅延するルーチン。|
|[HW_FIND_ADAPTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)|**HwStorFindAdapter**ルーチンが場合はそのアダプターに関する構成情報を返す、および特定の HBA がサポートされているかどうかを決定する指定された構成を使用します。|
|[HW_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_initialize)|HwStorInitialize ルーチンは、システムの再起動後、ミニポート ドライバーを初期化または電源障害が発生します。|
|[HW_INTERRUPT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_interrupt)|Storport ドライバーの呼び出し、 **HwStorInterrupt**ルーチン、HBA が割り込み要求を生成した後。|
|[HW_PASSIVE_INITIALIZE_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_passive_initialize_routine)|**HwStorPassiveInitializeRoutine**コールバック ルーチンが呼び出された後、 **HwStorInitialize**ルーチンの現在の IRQL が PASSIVE_LEVEL にある場合。|
|[HW_RESET_BUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_reset_bus)|**HwStorResetBus**ルーチンがエラー状態をクリアするポート ドライバーによって呼び出されます。|
|[HW_STARTIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)|Storport ドライバーの呼び出し、 **HwStorStartIo**ルーチン受信の I/O 要求ごとに 1 回です。|
|[HW_TIMER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_timer)|**HwStorTimer**ミニポート ドライバーが呼び出されたときに、間隔が指定した後に、ルーチンを呼び出す[StorPortNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportnotification)で、  *[RequestTimerCall](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportnotification)* NotificationType 値。|
|[]()||
