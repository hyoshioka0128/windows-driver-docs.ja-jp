---
title: Storport によって提供される機能
description: Storport によって提供される機能
ms.assetid: 30b4d2e4-2004-4d71-8c91-f066e52dd256
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eeeb27ec4ae887cec0463370f1f5a57ea7f49c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368364"
---
# <a name="capabilities-provided-by-storport"></a>Storport によって提供される機能


Storport ドライバーは、次の機能を提供します。

アドレス指定

-   Microsoft Windows には、さまざまな種類 I/O バスや、同じ種類の複数の I/O バスにはが含まれているシステムがサポートしています。 一般的なアドレス指定スキームがさまざまな種類を処理するために必要です。

-   PCI デバイスには、I/O ポートとメモリ リソースの登録の両方を持つことができます。 論理アドレスは、ポート ドライバーにこの区別を透明に役立ちます。

-   いくつかのシステムには、Hba が 1 つ以上のバスに接続しています。このような HBA には、アドレス変換のいくつかのセットが必要です。

-   CISC および RISC ベースのコンピューター間で移植性のための論理アドレスが必要です。

再試行とエラー処理

-   デバイスがビジー状態のため、それを処理するときに、Irp を再試行しています。

    記憶域クラス ドライバーは、デバイスがビジー状態のため、それを処理するときに Irp の再試行のためのアルゴリズムを実装するためにはありません。 Storport ドライバーでは、この機能を実装します。

-   要求のタイムアウト値を適用します。

    クラス ドライバーは、要求のタイムアウト値を設定して、Storport、実施する責任を負います。 ただし、Storport ドライバーを適用できますクラス ドライバーのタイムアウト値、柔軟に考慮バスの状態を取得します。 たとえば、Storport によって管理されるファイバー チャネルのリンクは、20 秒の削除する場合のリンクが再び起動した後、10 秒まで 10 秒のタイムアウト設定された要求は失敗しません、ように、ダウンタイム中にタイムアウト カウンターが Storport に中断可能性があります。 Storport では、負荷の I/O トラフィックと、デバイスの要求を完了する時間がかかるため、I/O トラフィックが増加する応答内の要求に割り当てられたタイムアウト値が増加します。

-   ターゲットとコント ローラー、負荷の高いエラー、さらにトランスポート エラー条件 (つまり、実際に、バス上のデータの転送に関連するエラー) を処理します。 以下に例を示します。

    1.  バス パリティ エラー
    2.  選択範囲のタイムアウト

構成、キュー、および電源状態の管理

-   ホスト アダプターの制限に関する情報を含むクラス ドライバーを提供します。

    ホスト バス アダプター (Hba) の制限に合わせてデータ転送のサイズを制御するクラス ドライバーの役目です。 ただし、Storport は、このタスクを実行する必要がある情報を使用してクラス ドライバーを提供します。 Storport、アダプターの記述子では、この情報を提供する ([**ストレージ\_アダプター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)) IOCTL 要求に応答 ([ **IOCTL\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property))。 クラス ドライバーは、要求をこの記述子で報告される情報に基づいて適切なサイズのチャンクに分割します。

-   バスの相対アドレスを論理アドレスを変換しています。

    このクエリを実行すると、アダプターは I/O ポート、コマンドのレジスタ、およびコントロールの状態のレジスタのバスの相対アドレスを提供します。 ただし、ミニポート ドライバーでは、そのホスト バス アダプター (HBA) との通信にバスの相対アドレスを使用できません。 ミニポート ドライバーは、透過的な方法で bus アドレスにアクセスできるように、Storport は論理アドレスは、バスの相対アドレスを変換します。 これにはいくつかの理由があります。

-   あるデバイスとその基になるすべてのデバイス電源が入っている (D0 デバイスの電源の状態) で、デバイスを開始する前にすることです。

    デバイスの電源が供給される準備ができていないとき、Storport、デバイスが準備できるまで、デバイスの D0 要求がキューします。

-   クラスのドライバーからの非同期要求をキューとターゲット デバイスに非同期的に転送します。

    クラスのドライバーを次の要求を送信する前に完了する要求を待機する必要はありません。 Storport では、基になるハードウェアの処理能力が過負荷を回避するためにこれらの要求をキューの責任を負います。

-   内部の I/O 要求キューの内部と外部の両方の管理をサポートします。

    ほとんどのキューの管理操作は、Storport 自体によって開始されます。 たとえば、Storport フリーズ キュー エラーが発生し、クラスのドライバーにエラー状態をレポート クラス ドライバーがさらに要求が処理される前に応答できるようにします。 ただし、Storport も要求から応答クラス ドライバーまたはその他のより高度なドライバーをロック、ロックを解除、凍結または内部要求キューの保持を解除します。 高度なドライバーが Storport を SRB を使用して、内部キューの解除を強制できます\_関数\_リリース\_キュー要求。 「固定」の意味の詳細については、「ロック」または「ロックを解除」キューを参照してください[Storport キュー管理](storport-queue-management.md)します。

-   処理のための scsi-3 センス データ形式にクラス ドライバーによって、デバイスによって報告されるエラーを変換しています。

Storport では、Storport のライブラリ ルーチンを使用して、ミニポート ドライバーにサービスを提供します。 ミニポート ドライバーの作成者には、1 つのモノリシック ポート ドライバーに提供する機能をコーディングするのではなく、これらのルーチンを呼び出すことができます。 によって、これらのルーチンを使用して最も重要なサービスの一部としては、

-   Storport ミニポート ドライバーが Storport に多くの OS に依存する初期化操作を委任できます[ **StorPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)ライブラリ ルーチン。 たとえば、PnP に関連する詳細の処理、Storport ドライバーと DMA のマッピング。 これにより、オペレーティング システムのバージョンが異なって Storport ミニポート ドライバーが移植性にします。 Storport ミニポート ドライバーの初期化作業の詳細については、次を参照してください。 [Storport 使用した初期化をハードウェア](hardware-initialization-with-storport.md)します。

-   非 PnP デバイスの Storport ミニポート ドライバーには、アダプターを検索して、レポート、リソース、PnP マネージャーをタスクが消費されません。 これを行う[ **StorPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)します。

-   Storport ミニポート ドライバーはドライバー オブジェクト内のエントリ ポイントのディスパッチを初期化できません。 Storport ドライバーは、ミニポート ドライバーに代わって、ミニポート ドライバーを呼び出すと[ **StorPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)します。

-   Storport ミニポート ドライバーを使用して、論理アドレスにバスの相対アドレスは変換されない[ **HalTranslateBusAddress**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))します。 Storport ミニポート ドライバーでは、これを行うへの呼び出しによって[ **StorPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetdevicebase)します。

Storport が Storport ミニポート ドライバーを使用できるようにするライブラリ ルーチンの完全な一覧を参照してください。 [Storport ドライバー サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

 

 




