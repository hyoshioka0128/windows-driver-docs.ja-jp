---
title: Storport ドライバーのミニポート ルーチン
description: Storport ミニポート ドライバー ルーチンと SCSI ポート ドライバーの設計および Storport ドライバーの間の相違点について説明します。
ms.assetid: ''
keywords:
- Storport ドライバーのサポート ルーチン
- WDK のストレージ
- 記憶域サポート ルーチン
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: d2a41b99c22ddd6b189b42379926cdd58bf8416b
ms.sourcegitcommit: 132f0c2d827982b808053ecd3b4d137a2883cca1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "56582724"
---
# <a name="storport-driver-miniport-routines"></a>Storport ドライバーのミニポート ルーチン

Storport ドライバーで動作するミニポート ドライバーは、このセクションで、日常的な説明の実装を含める必要がありますありを通じてそれらを公開する必要があります、 [HW_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_hw_initialization_data)ミニポート中に構造体ドライバーの初期化フェーズ。

Storport ミニポート ドライバーのルーチンは、対応する SCSI ポートと同じ多くの点では (を参照してください[SCSI ミニポート ドライバー ルーチン](https://technet.microsoft.com/ff565312(v=vs.96))詳細については)。 ただし、SCSI ポート ドライバーの設計および Storport ドライバーの重要な違いがあるし、これらのルーチンは、これらの違いに対応する必要があります。

たとえば、要求のミニポート ドライバーが Storport ドライバーを使用した作業はもう 1 つの I/O を受信する常に準備する必要がありますの後、 [HwStorStartIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)ルーチンが完了しました。 SCSI ポートで動作するミニポート ドライバーは、これを行う必要はありません。 SCSI ポートのバージョンは、ポート ドライバーを明示的に通知するまでに新しい I/O 要求を受信しなかったを使用して、 [StorPortNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportnotification)関数は、別の要求を処理する準備が整っています。

Storport のバージョンのミニポート ドライバーは、一連のキューの管理機能、SCSI ポートのバージョンには使用できませんが、送信される時に要求を処理できない場合、オーバー ロードを扱うことができます。 SCSI ポート版と同様のミニポート ドライバー、Storport のバージョンを使用して要求が完了すると**SRB_STATUS_BUSY**、SCSI ポート バージョンとは異なり、ビジー状態を使用してデバイスのキューをマークことできますもが、 [StorPortDeviceBusy](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdevicebusy)ルーチン。 ような関数は、一時停止と再開のアダプター全体で処理するには、ミニポート ドライバーを使用します。

Storport ドライバーによって提供されるサポート ルーチンの詳細については、次を参照してください。 [Storport ドライバー サポート ルーチン](storport-driver-support-routines.md)します。

Storport ドライバーの詳細については、次を参照してください。[ストレージ ポート ドライバー](storage-port-drivers.md)します。

次に、ミニポート ドライバー ルーチンを示します。

|                                                                               ルーチン                                                                               |                                                                                                                                                              説明                                                                                                                                                              |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [HW_MESSAGE_SIGNALED_INTERRUPT_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_message_signaled_interrupt_routine) |                                                                                                                           **HwMSInterruptRoutine**日常的なハンドルが、メッセージ シグナル割り込み (MSI)。                                                                                                                            |
|                    [HW_ADAPTER_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_adapter_control)                    |                                                             ミニポート ドライバーの**HwStorAdapterControl**状態または停止や電源管理の HBA の再起動など、アダプターの動作を制御する同期操作を実行するルーチンが呼び出されます。                                                             |
|                            [HW_BUILDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)                            |                                                                                          **HwStorBuildIo**ルーチンに渡す前にシステムの共有データ構造体に同期されていないアクセス権を持つ SRB を処理する**HwStorStartIo**します。                                                                                          |
|                        [HW_DPC_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_dpc_routine)                        |                                                                                        **HwStorDpcRoutine**ルーチンが遅延プロシージャ呼び出し (DPC) のメカニズムを使用してディスパッチ IRQL での実行が遅延するルーチン。                                                                                         |
|                       [HW_FIND_ADAPTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)                       |                                                                       **HwStorFindAdapter**ルーチンが場合はそのアダプターに関する構成情報を返す、および特定の HBA がサポートされているかどうかを決定する指定された構成を使用します。                                                                       |
|                         [HW_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_initialize)                         |                                                                                                            **HwStorInitialize**ルーチンは、システムの再起動後、ミニポート ドライバーを初期化または電源障害が発生します。                                                                                                            |
|                          [HW_INTERRUPT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_interrupt)                          |                                                                                                                Storport ドライバーの呼び出し、 **HwStorInterrupt**ルーチン、HBA が割り込み要求を生成した後。                                                                                                                |
|         [HW_PASSIVE_INITIALIZE_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_passive_initialize_routine)         |                                                                                          **HwStorPassiveInitializeRoutine**コールバック ルーチンが呼び出された後、 **HwStorInitialize**ルーチンの現在の IRQL が PASSIVE_LEVEL にある場合。                                                                                          |
|                          [HW_RESET_BUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_reset_bus)                          |                                                                                                                        **HwStorResetBus**ルーチンがエラー状態をクリアするポート ドライバーによって呼び出されます。                                                                                                                         |
|                            [HW_STARTIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)                            |                                                                                                                    Storport ドライバーの呼び出し、 **HwStorStartIo**ルーチン受信の I/O 要求ごとに 1 回です。                                                                                                                    |
|                              [HW_TIMER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_timer)                              |                                                                      **HwStorTimer**ミニポート ドライバーが呼び出されたときに、間隔が指定した後に、ルーチンを呼び出す**StorPortNotification**で、 **RequestTimerCall** *NotificationType*値。                                                                      |
|                    [HW_TRACING_ENABLED](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_tracing_enabled)                    |                                                                                                        **HwStorTracingEnabled**コールバック ルーチンにより、Storport ミニポート イベントのトレースが有効になっていることを通知します。                                                                                                         |
|                       [HW_UNIT_CONTRO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_unit_control)                        |                                           ミニポート ドライバーの**HwStorUnitControl**ストレージ ユニットのデバイスの状態を制御する同期操作を実行するルーチンが呼び出されます。 単位を開始またはユニットのデバイスの電源の状態遷移を処理するミニポート ドライバーに通知されます。                                            |
|                           [HW_WORKITEM](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_workitem)                           |                                                                                                                          Storport の作業項目の要求を処理するためのミニポート-用意されているコールバック関数。                                                                                                                           |
|             [STORPORT_TELEMETRY_EVENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_storport_telemetry_event)              |                                                                                                                       **STORPORT_TELEMETRY_EVENT**構造がミニポート テレメトリ データ ペイロードを記述します。                                                                                                                       |
|                  [StorPortLogTelemetry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogtelemetry)                  | **StorPortLogTelemetry**ルーチンには、診断に有用な情報を収集したりするミニポート テレメトリ イベントがログ記録します。 8 つの汎用名前/値ペアのログに記録できますミニポートとの関連するいくつかのイベントと同様に 4 KB、最大長を保持するバッファー フィールドを構造に定義されて**STORPORT_TELEMETRY_EVENT**します。 |
