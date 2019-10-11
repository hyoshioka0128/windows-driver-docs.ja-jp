---
title: Storport によって提供される機能
description: Storport によって提供される機能
ms.assetid: 30b4d2e4-2004-4d71-8c91-f066e52dd256
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 93e56204734e1acf66a0ab196741dd1d3e85b632
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252442"
---
# <a name="capabilities-provided-by-storport"></a>Storport によって提供される機能

Storport ドライバーは、次の機能を備えています。

- **取り組む**

  Microsoft Windows では、さまざまな種類の i/o バスや、同じ種類の複数の i/o バスを含むシステムがサポートされています。 このようなさまざまな処理を行うには、一般的なアドレス指定スキームが必要です。

  PCI デバイスは、i/o ポートとメモリレジスタリソースの両方を持つことができます。 論理アドレスは、この区別をポートドライバーに対して透過的にするのに役立ちます。

  複数のバスに接続されている Hba を含むシステムもあります。このような HBA では、複数のアドレス変換が必要になる場合があります。

  論理アドレスは、CISC ベースおよび RISC ベースのマシン間での移植性を確保するために必要です。

- **エラー処理**

  - ストレージクラスドライバーは、デバイスがビジー状態のために処理できない場合に、Irp を再試行するためのアルゴリズムを実装する必要はありません。 この機能は、Storport ドライバーによって実装されます。

  - クラスドライバーは、要求のタイムアウト値を設定し、Storport がそれを適用する役割を担います。 ただし、Storport ドライバーは、クラスドライバーのタイムアウト値を柔軟に適用し、バスの状態を考慮に入れることができます。 たとえば、Storport によって管理されているファイバーチャネルリンクが20秒間ドロップした場合、Storport はダウンタイム中にタイムアウトカウンターを中断する可能性があります。たとえば、タイムアウトが10秒の要求は、リンクが戻ってから10秒後に失敗することはありません。 また、i/o トラフィックの増加に応じて要求に割り当てられるタイムアウト値が増加します。これは、大量の i/o トラフィックが発生した場合、デバイスが要求を完了するためにより多くの時間が必要になるためです。

  - Storport では、ターゲットとコントローラーのビジーエラーに加え、トランスポートエラー状態 (バス上のデータの実際の転送に関連するエラー) も処理されます。 以下に例を示します。
    - バスパリティエラー
    - 選択のタイムアウト

- **構成、キュー、電源状態の管理**

  - ホストアダプターの制限に関する情報をクラスドライバーに提供する:ホストバスアダプター (Hba) の制限に合わせてデータ転送のサイズを制御するのは、クラスドライバーの役割です。 ただし、Storport は、このタスクを実行するために必要な情報をクラスドライバーに提供します。 Storport は、IOCTL 要求 ([**IOCTL_STORAGE_QUERY_PROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)) に応答して、この情報をアダプター記述子 ([STORAGE_ADAPTER_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)) に提供します。 クラスドライバーは、この記述子で報告された情報に基づいて、適切なサイズのチャンクに要求を分割する役割を担います。

  - バスの相対アドレスを論理アドレスに変換します。クエリを実行すると、アダプターは i/o ポート、コマンドレジスタ、およびコントロールステータスレジスタのバス相対アドレスを指定します。 ただし、ミニポートドライバーは、バス相対アドレスを使用してホストバスアダプター (HBA) と通信することはできません。 Storport はバスの相対アドレスを論理アドレスに変換し、ミニポートドライバーがバスアドレスに透過的にアクセスできるようにします。 これにはいくつかの理由があります。

  - デバイスとその基になるすべてのデバイスの電源が入っていることを確認する (デバイスの電源状態が D0 の場合)。デバイスの電源を入れる準備ができていない場合、Storport はデバイスの準備が整うまでそのデバイスに対して D0 要求をキューに入れます。

  - クラスドライバーからの非同期要求をキューに置いて、それらを非同期的にターゲットデバイスに転送します。クラスドライバーは、要求が完了するまで待機してから、次の要求を送信する必要はありません。 Storport は、基になるハードウェアの処理能力が過剰にならないように、これらの要求をキューに入れていることを前提としています。

  - 内部 i/o 要求キューの内部管理と外部管理の両方をサポートします。ほとんどのキュー管理操作は、Storport によって開始されます。 たとえば、Storport は、エラーが発生したときにキューをフリーズし、クラスドライバーにエラー状態を報告します。これにより、要求が処理される前にクラスドライバーが応答できるようになります。 ただし、Storport は、クラスドライバーまたはその他の上位レベルのドライバーからの要求にも応答して、内部要求キューをロック、ロック解除、固定、または凍結解除します。 上位レベルのドライバーは、SRB_FUNCTION_RELEASE_QUEUE 要求を使用して、Storport が内部キューの凍結を解除することを強制できます。 キューを "凍結"、"ロック" または "ロック解除する" という意味については、「 [Storport キュー管理](storport-queue-management.md)」を参照してください。

  - クラスドライバーによって処理するために、デバイスによって報告されたエラーを SCSI 3 sense データ形式に変換します。

Storport は、Storport ライブラリルーチンを使用して、ミニポートドライバーにサービスを提供します。 ミニポートドライバーの作成者は、指定された機能を1つのモノリシックポートドライバーにコーディングするのではなく、これらのルーチンを呼び出すことができます。 これらのルーチンを使用して実行できる最も重要なサービスの一部を次に示します。

- Storport ミニポートドライバーでは、多くの OS 依存の初期化操作を Storport の[**Storportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)ライブラリルーチンに委任できます。 たとえば、Storport ドライバーは、PnP と DMA のマッピングに関連する詳細を処理します。 これにより、異なるバージョンのオペレーティングシステム間で、Storport ミニポートドライバーの移植性が向上します。 Storport ミニポートドライバーの初期化作業の詳細については、「 [storport を使用したハードウェアの初期化](hardware-initialization-with-storport.md)」を参照してください。

- PnP 以外のデバイス用の Storport ミニポートドライバーは、アダプターを検索し、そのリソースを PnP マネージャーに報告するタスクに対応していません。 これは[**Storportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)で行われます。

- Storport ミニポートドライバーは、ドライバーオブジェクト内のディスパッチエントリポイントを初期化しません。 このドライバーは、ミニポートドライバーが[**Storportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)を呼び出したときに、ミニポートドライバーに代わってこれを行います。

- Storport ミニポートドライバーは、 **HalTranslateBusAddress**を使用してバス相対アドレスを論理アドレスに変換しません。 Storport ミニポートドライバーは、 [**Storportgetdevicebase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetdevicebase)を呼び出してこれを行います。

Storport が Storport ミニポートドライバーで使用できるライブラリルーチンの完全な一覧については、「 [Storport ドライバーサポートルーチン](storport-driver-support-routines.md)」を参照してください。
