---
title: Storport ドライバーのミニポート ルーチン
description: Storport ミニポートドライバーのルーチンと、SCSI ポートドライバーと Storport ドライバーの設計の違いについて説明します。
ms.assetid: f035cf06-d2ef-41da-a59a-0c00c626e3fb
keywords:
- Storport ドライバーのサポート ルーチン
- ストレージ WDK
- ストレージサポートルーチン
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: a69c5f07a50bdb4624db65ed88a39a9e0cd68d29
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844459"
---
# <a name="storport-driver-miniport-routines"></a>Storport ドライバーのミニポート ルーチン

Storport ドライバーで動作するミニポートドライバーには、このセクションに記載されているルーチンの説明の実装が含まれている必要があります。また、ミニポートドライバーの初期化中に、 [HW_INITIALIZATION_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data)構造体を使用して公開する必要があります。フェーズ.

Storport ミニポートドライバーのルーチンは、対応する SCSI ポートに相当します (詳細については、「 [Scsi ミニポートドライバールーチン](scsi-miniport-driver-routines.md)」を参照してください)。 ただし、SCSI ポートドライバーの設計と Storport ドライバーの設計には、重要な違いがあります。これらのルーチンでは、これらの違いに対処する必要があります。

たとえば、Storport ドライバーで動作するミニポートドライバーは、 [HwStorStartIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)ルーチンが完了した後に、常に別の i/o 要求を受信できるように準備する必要があります。 SCSI ポートで動作するミニポートドライバーは、これを行うためには必要ありません。 SCSI ポートのバージョンは、別の要求を処理するための準備として[Storportnotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification)関数を使用してポートドライバーに明示的に通知するまで、新しい i/o 要求を受信しません。

送信時に、Storport バージョンのミニポートドライバーが要求を処理できない場合、SCSI ポートのバージョンでは使用できないキュー管理機能のセットが用意されているので、オーバーロードを処理できます。 SCSI ポートのバージョンと同様に、Storport バージョンのミニポートドライバーは**SRB_STATUS_BUSY**を使用して要求を完了しますが、scsi ポートのバージョンとは異なり、 [Storportdevicebusy](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportdevicebusy)ルーチンを使用して、デバイスキューをビジー状態としてマークすることもできます。 同様の関数を使用すると、ミニポートドライバーは、アダプター全体で処理を一時停止および再開できます。

Storport ドライバーによって提供されるサポートルーチンの詳細については、「 [storport ドライバーのサポートルーチン](storport-driver-support-routines.md)」を参照してください。

Storport ドライバーの詳細については、「[ストレージポートドライバー](storage-port-drivers.md)」を参照してください。

ミニポートドライバールーチンは次のとおりです。

| ルーチン | 説明 |
| ------- | ----------- |
| [HW_MESSAGE_SIGNALED_INTERRUPT_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_message_signaled_interrupt_routine) | メッセージシグナル割り込み (MSI) を処理します。 |
| [HW_ADAPTER_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control) | 電源管理用の HBA の停止や再起動など、アダプタの状態または動作を制御する同期操作を実行します。 |
| [HW_BUILDIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio) | **HwStorStartIo**に渡す前に、共有システムデータ構造への同期されていないアクセスで SRB を処理します。 |
| [HW_DPC_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_dpc_routine) | 遅延プロシージャ呼び出し (DPC) メカニズムによってディスパッチ IRQL で実行が遅延されるルーチン。 |
| [HW_FIND_ADAPTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter) | 指定された構成を使用して、特定の HBA がサポートされているかどうかを判断し、ある場合はそのアダプタに関する構成情報を返します。 |
| [HW_INITIALIZE](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize) | システムの再起動または電源障害が発生した後に、ミニポートドライバーを初期化します。 |
| [HW_INTERRUPT](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_interrupt) | Storport ドライバーは、HBA が割り込み要求を生成した後に**HwStorInterrupt**ルーチンを呼び出します。 |
| [HW_PASSIVE_INITIALIZE_ROUTINE](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_passive_initialize_routine) | 現在の IRQL が PASSIVE_LEVEL にあるときに、 **HwStorInitialize**ルーチンの後に呼び出されます。 |
| [HW_RESET_BUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_reset_bus) | エラー状態をクリアするために、ポートドライバーによって呼び出されます。 |
| [HW_STARTIO](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio) | Storport ドライバーは、受信した i/o 要求ごとに**HwStorStartIo**ルーチンを1回呼び出します。 |
| [HW_TIMER](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_timer) | **Requesttimercall** *NotificationType*値を使用して、ポートドライバーが**storportnotification**を呼び出したときに指定された間隔の後に呼び出されます。 |
| [HW_TRACING_ENABLED](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_tracing_enabled) | イベントトレースが有効になっていることを Storport に通知します。 |
| [HW_UNIT_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_unit_control) | ストレージユニットデバイスの状態を制御する同期操作を実行するために呼び出されます。 ミニポートドライバーは、ユニットを開始するか、ユニットデバイスの電源状態の移行を処理するように通知されます。 |
| [HW_WORKITEM](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_workitem) | Storport 作業項目要求を処理するためのミニポート提供のコールバック関数。 |
| [STORPORT_TELEMETRY_EVENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_storport_telemetry_event) | ミニポートテレメトリデータペイロードについて説明します。 |
| [StorPortLogTelemetry](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogtelemetry) | 有用な情報の診断または収集に役立つミニポートテレメトリイベントをログに記録します。 ミニポートでは、8つの汎用的な名前と値のペア、最大の長さ 4 KB のバッファー、および structure STORPORT_TELEMETRY_EVENT で定義されている複数のイベント関連フィールドをログに記録できます。 |
