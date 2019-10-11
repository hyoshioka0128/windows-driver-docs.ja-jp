---
title: SCSI ポートによって提供される機能
description: SCSI ポートによって提供される機能
ms.assetid: 549dc3f1-b62f-4047-bdc0-7e24d5bc6ad5
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: af6d7be4a08eb9293da3853d3d9802fa0c5a5c8f
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252444"
---
# <a name="capabilities-provided-by-scsi-port"></a>SCSI ポートによって提供される機能

SCSI ポートドライバーは、次の機能を備えています。

- Microsoft Windows では、さまざまな種類の i/o バスや、同じ種類の複数の i/o バスを含むシステムがサポートされています。 このようなさまざまな処理を行うには、一般的なアドレス指定スキームが必要です。

- PCI デバイスは、i/o ポートとメモリレジスタリソースの両方を持つことができます。 論理アドレスは、この区別をポートドライバーに対して透過的にするのに役立ちます。

- 複数のバスに接続されている Hba を含むシステムもあります。このような HBA では、複数のアドレス変換が必要になる場合があります。

- 論理アドレスは、CISC ベースおよび RISC ベースのマシン間での移植性を確保するために必要です。

- デバイスがビジー状態のために処理できない場合は、Irp を再試行します。

    ストレージクラスドライバーは、デバイスがビジー状態のために処理できない場合に、Irp を再試行するためのアルゴリズムを実装する必要はありません。 SCSI ポートドライバーは、この機能を実装します。

- 要求のタイムアウト値を適用します。

    クラスドライバーは、要求のタイムアウト値を設定し、SCSI ポートはそれを適用する役割を担います。 ただし、SCSI ポートドライバーでは、クラスドライバーのタイムアウト値を柔軟に適用し、バスの状態を考慮に入れることができます。 たとえば、SCSI ポートによって管理されるファイバーチャネルリンクが20秒間ドロップした場合、SCSI ポートはダウンタイム中にタイムアウトカウンターを中断する可能性があります。たとえば、タイムアウトが10秒である要求は、リンクがバックアップされてから10秒が経過しても失敗しません。 SCSI ポートを使用すると、i/o トラフィックの増加に応じて要求に割り当てられるタイムアウト値を増やすことができます。これは、大量の i/o トラフィックが発生した場合に、デバイスが要求を完了するためにより多くの時間を必要とするためです。

- ターゲットおよびコントローラーのビジーエラーと、トランスポートエラー条件 (つまり、バス上のデータの実際の転送に関連するエラー) を処理します。 以下に例を示します。

  - バスパリティエラー
  - 選択のタイムアウト

- ホストアダプターの制限に関する情報をクラスドライバーに提供します。

    ホストバスアダプター (HBA) の制限に合わせてデータ転送のサイズを制御するのは、クラスドライバーの役割です。 ただし、SCSI ポートは、このタスクを実行するために必要な情報をクラスドライバーに提供します。 SCSI ポートは、 [**IOCTL_STORAGE_QUERY_PROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property) IOCTL 要求に応答して、この情報をアダプター記述子 ([STORAGE_ADAPTER_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)) に提供します。 クラスドライバーは、この記述子で報告された情報に基づいて、適切なサイズのチャンクに要求を分割する役割を担います。

- バスの相対アドレスを論理アドレスに変換します。

    クエリを実行すると、アダプターは i/o ポート、コマンドレジスタ、およびコントロールステータスレジスタのバス相対アドレスを指定します。 ただし、ミニポートドライバーは、バス相対アドレスを使用してホストバスアダプター (HBA) と通信することはできません。 SCSI ポートは、バスの相対アドレスを論理アドレスに変換します。これにより、ミニポートドライバーは、透過的な方法でバスアドレスにアクセスできるようになります。 これにはいくつかの理由があります。

- デバイスとその基になるすべてのデバイスの電源が入っていることを確認する (デバイスの電源状態が D0 の場合)。

    デバイスの電源を入れる準備ができていない場合、デバイスの準備が整うまで、SCSI ポートはそのデバイスに対して D0 要求をキューに入れます。

- クラスドライバーからの非同期要求をキューに置いて、ターゲットデバイスに同期的に転送します。

    クラスドライバーは、要求が完了するまで待機してから、次の要求を送信する必要はありません。 SCSI ポートは、基になるハードウェアの処理能力が過剰にならないように、これらの要求をキューに入れていることを前提としています。

- 内部 i/o 要求キューの内部管理と外部管理の両方をサポートします。

    ほとんどのキュー管理操作は、SCSI ポート自体によって開始されます。 たとえば、SCSI ポートは、エラーが発生したときにキューをフリーズし、クラスドライバーにエラー状態を報告します。これにより、クラスドライバーは、さらに要求が処理される前に応答できるようになります。 ただし、SCSI ポートは、クラスドライバーまたはその他の上位レベルのドライバーからの要求にも応答して、内部要求キューをロック、ロック解除、固定、または凍結解除します。 上位レベルのドライバーでは、SRB_FUNCTION_RELEASE_QUEUE 要求を使用して、SCSI ポートが内部キューの固定を解除することができます。 キューを "凍結"、"ロック" または "ロック解除する" という意味については、「 [SCSI ポートドライバーのキュー管理](scsi-port-driver-s-queue-management.md)」を参照してください。

- デバイスによって報告されたエラーを、クラスドライバーによって処理するために、SCSI 2 sense データ形式に変換します。

Scsi ポートは、SCSI ポートライブラリルーチンを使用して、ミニポートドライバーにサービスを提供します。 ミニポートドライバーの作成者は、指定された機能を1つのモノリシックポートドライバーにコーディングするのではなく、これらのルーチンを呼び出すことができます。 これらのルーチンを使用して実行できる最も重要なサービスの一部を次に示します。

- SCSI ポートミニポートドライバーは、OS に依存する多くの初期化操作を SCSI ポートの[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)ライブラリルーチンに委任できます。 これにより、異なるバージョンのオペレーティングシステム間で SCSI ポートミニポートドライバーの移植性が向上します。 SCSI ポートミニポートドライバーの初期化作業の詳細については、「 [Scsi ミニポートドライバーの DriverEntry ルーチン](scsi-miniport-driver-s-driverentry-routine.md)」を参照してください。

- PnP 以外のデバイス用の SCSI ポートミニポートドライバーは、アダプターを検索し、そのリソースを PnP マネージャーに報告するタスクとは対応していません。 これは[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)で行われます。

- SCSI ポートミニポートドライバーは、ドライバーオブジェクト内のディスパッチエントリポイントを初期化しません。 SCSI ポートドライバーは、ミニポートドライバーが[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)を呼び出したときに、ミニポートドライバーに代わってこれを行います。

- SCSI ポートミニポートドライバーは、 [**HalTranslateBusAddress**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))を使用してバス相対アドレスを論理アドレスに変換しません。 SCSI ポートミニポートドライバーは、 [**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)を呼び出すことによってこれを行います。

Scsi ポートが SCSI ポートミニポートドライバーで使用できるライブラリルーチンの概要については、「 [Scsi ポートドライバーのサポートルーチン](scsi-port-driver-support-routines.md)」を参照してください。
