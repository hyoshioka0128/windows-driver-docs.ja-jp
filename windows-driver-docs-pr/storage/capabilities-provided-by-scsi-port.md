---
title: SCSI ポートによって提供される機能
description: SCSI ポートによって提供される機能
ms.assetid: 549dc3f1-b62f-4047-bdc0-7e24d5bc6ad5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e5f7714f7c41045a4fcf165b0a1d64f7465fc3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368362"
---
# <a name="capabilities-provided-by-scsi-port"></a>SCSI ポートによって提供される機能


## <span id="ddk_capabilities_provided_by_scsi_port_kg"></span><span id="DDK_CAPABILITIES_PROVIDED_BY_SCSI_PORT_KG"></span>


SCSI ポート ドライバーは、次の機能を提供します。

-   Microsoft Windows には、さまざまな種類 I/O バスや、同じ種類の複数の I/O バスにはが含まれているシステムがサポートしています。 一般的なアドレス指定スキームがさまざまな種類を処理するために必要です。

-   PCI デバイスには、I/O ポートとメモリ リソースの登録の両方を持つことができます。 論理アドレスは、ポート ドライバーにこの区別を透明に役立ちます。

-   いくつかのシステムには、Hba が 1 つ以上のバスに接続しています。このような HBA には、アドレス変換のいくつかのセットが必要です。

-   CISC および RISC ベースのコンピューター間で移植性のための論理アドレスが必要です。

<!-- -->

-   デバイスがビジー状態のため、それを処理するときに、Irp を再試行しています。

    記憶域クラス ドライバーは、デバイスがビジー状態のため、それを処理するときに Irp の再試行のためのアルゴリズムを実装するためにはありません。 SCSI ポート ドライバーでは、この機能を実装します。

-   要求のタイムアウト値を適用します。

    クラス ドライバーは、要求のタイムアウト値を設定し、SCSI ポートが実施する責任を負います。 ただし、SCSI ポート ドライバーを適用できますクラス ドライバーのタイムアウト値、柔軟に考慮バスの状態を取得します。 たとえば、SCSI ポートによって管理されるファイバー チャネルのリンクは、20 秒の削除する場合のリンクが再び起動した後、10 秒まで 10 秒のタイムアウト設定された要求は失敗しません、ように、ダウンタイム中にタイムアウト カウンターが SCSI ポートに中断可能性があります。 SCSI ポートは、負荷の I/O トラフィックと、デバイスの要求を完了する時間がかかるために、I/O トラフィックが増加する応答内の要求に割り当てられたタイムアウト値を増加します。

-   ターゲットとコント ローラー、負荷の高いエラー、さらにトランスポート エラー条件 (つまり、実際に、バス上のデータの転送に関連するエラー) を処理します。 以下に例を示します。

-   1.  バス パリティ エラー
    2.  選択範囲のタイムアウト

<!-- -->

-   ホスト アダプターの制限に関する情報を含むクラス ドライバーを提供します。

    ホスト バス アダプター (HBA) の制限に合わせてデータ転送のサイズを制御するクラス ドライバーの役目です。 ただし、SCSI ポートは、このタスクを実行する必要がある情報を使用してクラス ドライバーを提供します。 SCSI ポートは、アダプターの記述子では、この情報を提供 ([**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)) への応答、 [ **IOCTL\_記憶域\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property) IOCTL 要求。 クラス ドライバーは、要求をこの記述子で報告される情報に基づいて適切なサイズのチャンクに分割します。

-   バスの相対アドレスを論理アドレスを変換しています。

    このクエリを実行すると、アダプターは I/O ポート、コマンドのレジスタ、およびコントロールの状態のレジスタのバスの相対アドレスを提供します。 ただし、ミニポート ドライバーでは、そのホスト バス アダプター (HBA) との通信にバスの相対アドレスを使用できません。 SCSI ポートは、ミニポート ドライバーは、透過的な方法で bus アドレスにアクセスできるように、論理アドレスは、バスの相対アドレスを変換します。 これにはいくつかの理由があります。

-   あるデバイスとその基になるすべてのデバイス電源が入っている (D0 デバイスの電源の状態) で、デバイスを開始する前にすることです。

    デバイスの電源が供給される準備ができていないとき、デバイスが準備できるまで、デバイスの SCSI ポートのキュー、D0 を要求します。

-   クラスのドライバーからの非同期要求をキューとターゲット デバイスに同期的に転送します。

    クラスのドライバーを次の要求を送信する前に完了する要求を待機する必要はありません。 SCSI ポートでは、基になるハードウェアの処理能力が過負荷を回避するためにこれらの要求をキューの責任を負います。

-   内部の I/O 要求キューの内部と外部の両方の管理をサポートします。

    ほとんどのキューの管理操作は、SCSI ポート自体によって開始されます。 たとえば、SCSI ポートがフリーズする、キュー、エラーが発生し、クラスのドライバーにエラー状態をレポート クラス ドライバーがさらに要求が処理される前に応答できるようにします。 ただし、SCSI ポートも要求から応答クラス ドライバーまたはその他のより高度なドライバーをロック、ロックを解除、凍結または内部要求キューの保持を解除します。 高度なドライバーは、SRB を使用して、内部キューを固定解除する SCSI ポートを強制できます\_関数\_リリース\_キュー要求。 「固定」の意味の詳細については、「ロック」または「ロックを解除」キューを参照してください[SCSI ポート ドライバーのキュー管理](scsi-port-driver-s-queue-management.md)します。

-   クラス ドライバーによって処理のセンス データ形式のデバイスの 2 つに、デバイスによって報告されるエラーを変換しています。

SCSI ポートは、SCSI ポート ライブラリのルーチンを使用して、ミニポート ドライバーにサービスを提供します。 ミニポート ドライバーの作成者には、1 つのモノリシック ポート ドライバーに提供する機能をコーディングするのではなく、これらのルーチンを呼び出すことができます。 によって、これらのルーチンを使用して最も重要なサービスの一部としては、

-   SCSI ポート ミニポート ドライバーは、SCSI ポートの多くの OS に依存する初期化操作を委任できます[ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)ライブラリ ルーチン。 これにより、オペレーティング システムのバージョンが異なって SCSI ポート ミニポート ドライバーが移植性にします。 SCSI ポート ミニポート ドライバーの初期化作業の詳細については、次を参照してください。 [SCSI ミニポート ドライバー DriverEntry ルーチン](scsi-miniport-driver-s-driverentry-routine.md)します。

-   非 PnP デバイスの SCSI ポート ミニポート ドライバーには、アダプターを検索して、レポート、リソース、PnP マネージャーをタスクが消費されません。 これを行う[ **ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)します。

-   SCSI ポート ミニポート ドライバーはドライバー オブジェクト内のエントリ ポイントのディスパッチを初期化できません。 SCSI ポート ドライバーは、ミニポート ドライバーに代わって、ミニポート ドライバーを呼び出すと[ **ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)します。

-   SCSI ポート ミニポート ドライバーを使用して、論理アドレスにバスの相対アドレスは変換されない[ **HalTranslateBusAddress**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))します。 SCSI ポート ミニポート ドライバーでは、これを行うへの呼び出しによって[ **ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)します。

SCSI ポートのミニポート ドライバー SCSI ポートが利用できるようにするライブラリ ルーチンの完全な一覧を参照してください。 [SCSI ポート ライブラリ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 




