---
title: オフロード データ転送
description: オフロード データ転送
appliesto:
- Windows Server 2019
- Windows Server 2016
ms.assetid: EDFA6AFB-7D14-44F8-A105-E74182D26398
ms.date: 07/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: 95d9f5311a5a67f8883ad992bf1954dfc6f8926f
ms.sourcegitcommit: 69261fa09a48b70a681bec0b4cf7afa8b84c73b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2019
ms.locfileid: "68415097"
---
# <a name="offloaded-data-transfer"></a>オフロード データ転送


## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要


オフロードデータ転送 (ODX) では、記憶装置上のデータを移動するためのトークン化された操作が導入されています。 ソースファイルとターゲットファイルは、同じボリューム、同じマシンでホストされている2つの異なるボリューム、SMB2 を介したローカルボリュームとリモートボリューム、または SMB2 を介して2つの異なるマシン上の2つのボリュームに配置できます。 オフロードデータ転送は、Windows 8 で導入されました。

次に、ODX を使用したコピーオフロード操作のプロセスを示します。

1.  コピーオフロードアプリケーションは、ソースストレージデバイスのコピーマネージャーにオフロード読み取り要求を送信します。
2.  アプリケーションは、receive offload read result 要求をコピーマネージャーに送信し、トークンでを返します。 トークンは、コピーされるデータの表現です。
3.  アプリケーションは、トークンを使用して、変換先のストレージデバイスのコピーマネージャーにオフロード書き込み要求を送信します。
4.  アプリケーションは、受信オフロード書き込みの結果要求をコピーマネージャーに送信します。 コピーマネージャーは、コピー元からコピー先にデータを移動し、オフロード書き込み結果をアプリケーションに返します。

## <a name="span-ididentifyanodx-capablesourceanddestinationspanspan-ididentifyanodx-capablesourceanddestinationspanspan-ididentifyanodx-capablesourceanddestinationspanidentify-an-odx-capable-source-and-destination"></a><span id="Identify_an_ODX-Capable_Source_and_Destination"></span><span id="identify_an_odx-capable_source_and_destination"></span><span id="IDENTIFY_AN_ODX-CAPABLE_SOURCE_AND_DESTINATION"></span>ODX 対応のソースと宛先を特定する


ODX をサポートするには、記憶域配列で、関連する T10 標準仕様を実装する必要があります。 ODX 対応のストレージアレイ、オフロードの読み取りと書き込みの操作、および既知のトークンによるオフロードの書き込みが指定されています。 LUN デバイスの列挙中 (システムブートまたはプラグアンドプレイイベント)。 Windows は、次の手順に従って、ストレージターゲットデバイスの ODX 機能情報を収集または更新します。

1.  クエリコピーオフロード機能。
2.  コピーオフロード操作と制限に必要なパラメーターを収集します。

既定では、コピー元とコピー先の両方の Lun が ODX 対応である場合、Windows は最初に ODX パスをコピー操作のために試行します。 ストレージデバイスが最初の ODX 要求に失敗した場合、Windows はソースと宛先の LUN の組み合わせを "非 ODX 対応" パスとしてマークします。

## <a name="span-idodxreadwriteoperationsspanspan-idodxreadwriteoperationsspanspan-idodxreadwriteoperationsspanodx-readwrite-operations"></a><span id="ODX_Read_Write_Operations"></span><span id="odx_read_write_operations"></span><span id="ODX_READ_WRITE_OPERATIONS"></span>ODX 読み取り/書き込み操作


### <a name="span-idsynchronouscommandadoptionandapisspanspan-idsynchronouscommandadoptionandapisspanspan-idsynchronouscommandadoptionandapisspansynchronous-command-adoption-and-apis"></a><span id="Synchronous_Command_Adoption_and_APIs"></span><span id="synchronous_command_adoption_and_apis"></span><span id="SYNCHRONOUS_COMMAND_ADOPTION_AND_APIS"></span>同期コマンドの導入と Api

Windows 同期オフロードの読み取りと書き込み操作。 大きなオフロード書き込み要求は、次のアルゴリズムを使用して分割され、信頼性の高い同期オフロード書き込みを保証します。

-   ターゲットのストレージデバイスが最適な転送サイズを提供しない場合は、最適な転送サイズを 64 MB に設定します。
-   ストレージターゲットデバイスによって指定された最適な転送サイズ-最適な転送サイズが0より大きく 256 MB 未満です。
-   ターゲットデバイスによって設定された最適な転送サイズが 256 MB を超える場合は、最適な転送サイズを 256 MB に設定します。

同期オフロード読み取りとオフロード書き込み SCSI コマンドにより、MPIO およびクラスターのフェールオーバーシナリオの複雑さが軽減されます。 Windows では、コピーマネージャーが同期オフロードの読み取り/書き込み SCSI コマンドを4秒以内に完了することを前提としています。

アプリケーションでは、FSCTL、DSM IOCTL、また\_は\_SCSI パススルー api を使用してストレージアレイと対話し、コピーオフロード操作を実行できます。 データの破損やシステムの不安定を避けるために、Windows では、最初にボリュームに排他的にアクセスすることなく、ファイルシステムによってマウントされたボリュームにアプリケーションが直接書き込まれることを制限しています。 これは、ボリュームへの書き込みがファイルシステムの書き込みと競合する可能性があるためです。 このような競合が発生した場合、ボリュームの内容が不整合な状態のままになることがあります。

### <a name="span-idoffloadreadoperationsspanspan-idoffloadreadoperationsspanspan-idoffloadreadoperationsspanoffload-read-operations"></a><span id="Offload_Read_Operations"></span><span id="offload_read_operations"></span><span id="OFFLOAD_READ_OPERATIONS"></span>読み取り操作のオフロード

アプリケーションのオフロード読み取り要求では、トークンの有効期間 (非アクティブなタイムアウト) を指定できます。 アプリケーションでトークンの有効期間をゼロに設定すると、既定の非アクティブタイマーがトークンの有効期間として使用されます。 ストレージアレイのコピーマネージャーは、非アクティブなタイムアウト値と資格情報に従ってトークンを保持し、検証します。 また、Windows ホストはファイルフラグメントの数を64に制限します。 オフロードの読み取り要求が64を超えるフラグメントで構成されている場合、Windows はコピーオフロード要求を失敗として、従来のコピー操作にフォールバックします。

オフロード読み取り要求を完了すると、コピーマネージャーは、receive offload read result コマンドに対してデータの表現 (ロッド) トークンを準備します。 [ロッド token] フィールドでは、ユーザーデータと保護情報の特定時点の表現を指定します。 このロッドは、[排他的に開く] または [共有で開く] の形式のユーザーデータにすることができます。 コピーマネージャーは、そのロッドのポリシー設定に従ってトークンを無効にすることができます。 ロッドがコピーオフロード操作専用に開いている場合、ロッドが変更または移動されると、ロッドトークンは無効になります。 ロッドが "共有で開く" 形式の場合、ロッドトークンは、ロッドが変更されたときに有効なままになります。

| サイズ (バイト単位) | トークンの内容 |
|---------------|----------------|
| 4             | ロッドトークン型 |
| 508           | ロッドトークン ID   |

 

この場合、ロッドトークンはストレージアレイによってのみ許可および使用されるため、その形式は不透明で一意で、高い安全性を備えています。 トークンが変更された場合、検証されていない場合、または有効期限が切れている場合、コピーマネージャーはオフロード書き込み操作中にトークンを無効にすることができます。 オフロード読み取り操作から返されたロッドトークンには、トークン使用法を使用した次の書き込みでトークンが有効であることをコピーマネージャーが保持する必要がある秒数を示す非アクティブなタイムアウト値があります。

### <a name="span-idoffloadwriteoperationsspanspan-idoffloadwriteoperationsspanspan-idoffloadwriteoperationsspanoffload-write-operations"></a><span id="Offload_Write_Operations"></span><span id="offload_write_operations"></span><span id="OFFLOAD_WRITE_OPERATIONS"></span>書き込み操作のオフロード

コピーマネージャーからロッドトークンを受け取った後、アプリケーションは、ロッドトークンを使用して、ストレージアレイのコピーマネージャーにオフロード書き込み要求を送信します。 同期オフロード書き込みコマンドがターゲットデバイスに送信されると、Windows はコピーマネージャーが4秒以内にコマンドを完了すると想定します。 コマンドタイムアウトまたはその他のエラー状態が原因でコマンドが終了した場合、Windows はコマンドを失敗させます。 アプリケーションは、返されたステータスコードに従って、従来のコピー操作にフォールバックします。

オフロード書き込み要求は、1つまたは複数の受信オフロード書き込み結果コマンドを使用して完了できます。 オフロード書き込みが部分的に完了した場合、コピーマネージャーは、推定遅延時間と、コピーの進行状況を示す転送数を返します。 転送数は、ソースからコピー先メディアへのエラーなしで書き込まれた連続する論理ブロックの数を指定します。 コピーマネージャーは、順次またはスキャッター/ギャザーパターンで書き込みのオフロードを実行できます。

書き込みエラーが発生すると、コピーの進行状況によって、最初の論理ブロックからエラーブロックまでの連続する論理ブロックがカウントされます。 クライアントアプリケーションまたはコピーエンジンは、書き込みエラーブロックからのオフロード書き込みを再開します。 オフロード書き込みが完了すると、コピーマネージャーは、[推定ステータス更新遅延] が0に設定され、データ転送回数が 100% である [受信ロッドトークン情報] コマンドを完了します。 受信オフロード書き込みの結果がデータ転送カウントと同じ進行状況を返した場合、Windows は4回の再試行の後にコピー操作をアプリケーションに戻します。

クライアントアプリケーションは、よく知られたロッドトークンを使用してオフロード書き込み操作を実行することもできます。 これは、既知のデータパターンとトークン形式を持つ定義済みのロッドトークンです。 1つの一般的な実装はゼロトークンと呼ばれます。 クライアントアプリケーションはゼロトークンを使用して、論理ブロックの1つ以上の範囲をゼロで埋めることができます。 既知のトークンがサポートされていないか認識できない場合、コピーマネージャーは "無効なトークン" を使用してオフロード書き込み要求を失敗させます。

| サイズ (バイト単位) | トークンの内容     |
|---------------|--------------------|
| 4             | ロッドトークン型     |
| 2             | よく知られているパターン |
| 506           | ロッドトークン ID       |

 

既知のロッドトークンを使用したオフロード書き込みでは、クライアントアプリケーションはオフロード読み取りを使用して、既知のトークンを要求することはできません。 コピーマネージャーは、独自のポリシーに従って既知のロッドトークンを検証し、管理します。

### <a name="span-idperformancetuningparametersofodximplementationspanspan-idperformancetuningparametersofodximplementationspanspan-idperformancetuningparametersofodximplementationspanperformance-tuning-parameters-of-odx-implementation"></a><span id="Performance_Tuning_Parameters_of_ODX_Implementation"></span><span id="performance_tuning_parameters_of_odx_implementation"></span><span id="PERFORMANCE_TUNING_PARAMETERS_OF_ODX_IMPLEMENTATION"></span>ODX 実装のパフォーマンスチューニングパラメーター

ODX のパフォーマンスは、サーバーと記憶域配列間のクライアント/サーバーネットワークまたは SAN のトランスポートリンク速度に依存しません。 データは、コピーマネージャーと記憶域配列のデバイスサーバーによって移動されます。

すべてのコピーオフロードが ODX テクノロジの恩恵をもたらすとは限りません。 たとえば、1ギガビット iSCSI ストレージアレイのコピーマネージャーは、10秒以内に 3 GB のファイルコピーを完了でき、データ転送速度は 300 MB/秒よりも大きくなります。 データ転送速度は、1ギガビットイーサネットインターフェイスの理論的な最大転送速度より既に向上しています。

すべてのファイルサイズのコピーオフロードによって、Windows ODX テクノロジのメリットが得られるわけではありません。 特定のサイズのファイルのコピーパフォーマンスが、ODX テクノロジの恩恵を受けない可能性があります。 パフォーマンスを最適化するために、ODX の使用は、ファイルの最小サイズと最大コピー長を許可するように制限できます。 ODX のパフォーマンスを調整するには、次のパラメーターを調整します。

コピーオフロード操作に最低限必要なファイルサイズを設定します。 現時点では、コピーオフロードの最小ファイルサイズは、コピーエンジンで 256 KB に設定されています。 ファイルが 256 KB 未満の場合、コピーエンジンは従来のコピープロセスにフォールバックします。

Windows ホストは、最大トークン転送サイズと最適な転送数を使用して、オフロード読み取りまたは書き込み SCSI コマンドの最適な転送サイズを準備します。 ブロック数の合計転送サイズは、最大トークン転送サイズを超えることはできません。 記憶域配列が最適な転送回数を報告しない場合、Windows では既定のカウントとして 64 MB が使用されます。

最適および最大転送長パラメーターでは、1つの範囲記述子に含まれる最大ブロック数を指定します。 コピーオフロードアプリケーションは、これらのパラメーターに準拠して、最適なファイル転送パフォーマンスを実現できます。

## <a name="span-idodxerrorhandlingandhighavailabilitysupportspanspan-idodxerrorhandlingandhighavailabilitysupportspanspan-idodxerrorhandlingandhighavailabilitysupportspanodx-error-handling-and-high-availability-support"></a><span id="ODX_Error_Handling_and_High_Availability_Support"></span><span id="odx_error_handling_and_high_availability_support"></span><span id="ODX_ERROR_HANDLING_AND_HIGH_AVAILABILITY_SUPPORT"></span>ODX のエラー処理と高可用性のサポート


ODX 操作でファイルコピー要求が失敗した場合、コピーエンジンと Windows ファイルシステム (NTFS) は従来のコピー操作にフォールバックします。 オフロード書き込み操作の途中でコピーオフロードが失敗した場合、コピーエンジンと NTFS は、オフロード書き込みの最初の障害点からの従来のコピー操作で再開されます。

次に示すのは、ODX を使用したコピーオフロード操作のアルゴリズムです。

### <a name="span-idodxerrorhandlingspanspan-idodxerrorhandlingspanspan-idodxerrorhandlingspanodx-error-handling"></a><span id="ODX_Error_Handling"></span><span id="odx_error_handling"></span><span id="ODX_ERROR_HANDLING"></span>ODX エラー処理

ODX は、記憶域配列の機能に従って、堅牢なエラー処理アルゴリズムを使用します。 ODX 対応パスでコピーオフロードが失敗した場合、Windows ホストはアプリケーションが従来のコピー操作にフォールバックすることを想定しています。 この時点で、Windows コピーエンジンは、"従来のコピーへのフォールバック" メカニズムを既に実装しています。 コピーオフロードエラーが発生すると、NTFS はソースとターゲットの LUN を ODX 対応ではなく3分間としてマークします。 この時間が経過すると、Windows コピーエンジンによって ODX 操作が再試行されます。 記憶域配列では、この機能を使用して、高度に負荷された状況で、一部のパスで ODX のサポートを一時的に無効にすることができます。

### <a name="span-idodxfailoverinmpioandclusterserverconfigurationsspanspan-idodxfailoverinmpioandclusterserverconfigurationsspanspan-idodxfailoverinmpioandclusterserverconfigurationsspanodx-failover-in-mpio-and-cluster-server-configurations"></a><span id="ODX_Failover_in_MPIO_and_Cluster_Server_Configurations"></span><span id="odx_failover_in_mpio_and_cluster_server_configurations"></span><span id="ODX_FAILOVER_IN_MPIO_AND_CLUSTER_SERVER_CONFIGURATIONS"></span>MPIO およびクラスターサーバー構成の ODX フェールオーバー

オフロードの読み取りと書き込みの操作は、同じストレージリンク (私\_は、"分散") から完了またはキャンセルする必要があります。

同期オフロードの読み取りまたは書き込み操作中に MPIO またはクラスターサーバーのフェールオーバーが発生すると、Windows は次のアルゴリズムを使用してフェールオーバーを処理します。

1.  同期オフロードの読み取り/書き込みコマンド。
2.  MPIO 構成の場合-Windows は、MPIO パスのフェールオーバー後に失敗したコマンドを再試行します。 コマンドが再度失敗した場合、Windows は次の処理を実行します。
    -   クラスターサーバーのフェールオーバーオプションを使用しない場合、Windows は LUN のリセットを記憶装置に発行し、i/o エラーの状態をアプリケーションに返します。
    -   クラスターサーバーのフェールオーバーオプションを使用すると、クラスターサーバーノードのフェールオーバーが開始されます。

3.  クラスターサーバー構成では、クラスター記憶域サービスは次に優先されるクラスターノードにフェールオーバーしてから、クラスター記憶域サービスを再開します。 クラスターストレージサービスのフェールオーバー後にオフロードの読み取り/書き込みコマンドを再試行できるようにするには、オフロードアプリケーションがクラスターに対応している必要があります。

MPIO パスとクラスターノードのフェールオーバー後にオフロードの読み取りまたは書き込みコマンドが失敗した場合は、フェールオーバー後に、Windows によってストレージデバイスに LUN のリセットが発行されます。 ストレージデバイスは、LUN で未処理のコマンドと保留中の操作をすべて終了します。

現在、Windows では、ストレージスタックからの非同期オフロードの読み取りまたは書き込みの SCSI コマンドは発行されません。

## <a name="span-idodxusagemodelsspanspan-idodxusagemodelsspanspan-idodxusagemodelsspanodx-usage-models"></a><span id="ODX_Usage_Models"></span><span id="odx_usage_models"></span><span id="ODX_USAGE_MODELS"></span>ODX の使用モデル


### <a name="span-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanspan-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanspan-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanodx-across-physical-disk-virtual-hard-disk-and-smb-shared-disk"></a><span id="ODX_across_Physical_Disk__Virtual_Hard_Disk_and_SMB_Shared_Disk"></span><span id="odx_across_physical_disk__virtual_hard_disk_and_smb_shared_disk"></span><span id="ODX_ACROSS_PHYSICAL_DISK__VIRTUAL_HARD_DISK_AND_SMB_SHARED_DISK"></span>物理ディスク、仮想ハードディスク、および SMB 共有ディスク全体の ODX

ODX 操作を実行するには、アプリケーションサーバーが、ソース LUN と宛先 LUN の両方に読み取り/書き込み特権でアクセスできる必要があります。 コピーオフロードアプリケーションは、ソース LUN にオフロード読み取り要求を発行し、ソース LUN のコピーマネージャーからトークンを受信します。 コピーオフロードアプリケーションでは、トークンを使用して、移行先 LUN にオフロード書き込み要求を発行します。 コピーマネージャーは、記憶域ネットワークを介して、ソース LUN からターゲット LUN にデータを移動します。

### <a name="span-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanodx-operation-with-one-server"></a><span id="ODX_Operation_with_One_Server"></span><span id="odx_operation_with_one_server"></span><span id="ODX_OPERATION_WITH_ONE_SERVER"></span>1台のサーバーでの ODX 操作

シングルサーバー構成では、コピーオフロードアプリケーションは、同じサーバーシステムからのオフロード読み取り要求と書き込み要求を発行します。

### <a name="span-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanodx-operation-with-one-server"></a><span id="ODX_Operation_with_One_Server"></span><span id="odx_operation_with_one_server"></span><span id="ODX_OPERATION_WITH_ONE_SERVER"></span>1台のサーバーでの ODX 操作

シングルサーバー構成では、コピーオフロードアプリケーションは、同じサーバーシステムからのオフロード読み取り要求と書き込み要求を発行します。

前の図では、Server1 または Virtual Machine1 は、ソース LUN (VHD1 または物理 Disk1) と宛先 LUN (VHD2 または物理 Disk2) の両方にアクセスできます。 コピーオフロードアプリケーションは、ソース LUN にオフロード読み取り要求を発行し、ソース LUN からトークンを受信します。次に、コピーオフロードアプリケーションは、トークンを使用して、移行先 LUN にオフロード書き込み要求を発行します。 コピーマネージャーは、同じ記憶域配列内のソース LUN からターゲット LUN にデータを移動します。

### <a name="span-idodxoperationwithtwoserversspanspan-idodxoperationwithtwoserversspanspan-idodxoperationwithtwoserversspanodx-operation-with-two-servers"></a><span id="ODX_Operation_with_Two_Servers"></span><span id="odx_operation_with_two_servers"></span><span id="ODX_OPERATION_WITH_TWO_SERVERS"></span>2台のサーバーを使用した ODX 操作

2台のサーバー構成では、2つのサーバーと複数の記憶域配列が同じコピーマネージャーによって管理されます。

-   Server1 または Virtual Machine1 はソース LUN のホストで、Server2 または Virtual Machine2 は宛先 LUN のホストです。 Server1 は、SMB プロトコル経由でソース LUN をアプリケーションクライアントと共有します。また、Server2 は、SMB プロトコル経由で宛先 LUN をアプリケーションクライアントと共有します。 アプリケーションクライアントは、ソース LUN とターゲット LUN の両方にアクセスできます。
-   移行元と移行先の記憶域配列は、SAN 構成で同じコピーマネージャーによって管理されます。
-   コピーオフロードアプリケーションは、アプリケーションクライアントシステムから、ソース LUN にオフロード読み取り要求を発行し、ソース LUN からトークンを受け取り、そのトークンを使用して移行先 LUN にオフロード書き込み要求を発行します。 コピーマネージャーは、2つの異なる場所にある2つの異なる記憶域配列の間で、ソース LUN からターゲット LUN にデータを移動します。

### <a name="span-idmassivedatamigrationspanspan-idmassivedatamigrationspanspan-idmassivedatamigrationspanmassive-data-migration"></a><span id="Massive_Data_Migration"></span><span id="massive_data_migration"></span><span id="MASSIVE_DATA_MIGRATION"></span>大量のデータの移行

大量のデータの移行とは、データベースレコード、スプレッドシート、テキストファイル、スキャンされたドキュメント、画像など、大量のデータを新しいシステムにインポートするプロセスのことです。 データの移行は、ストレージシステムのアップグレード、新しいデータベースエンジン、またはアプリケーションやビジネスプロセスにおける変更によって発生する可能性があります。 ODX を使用すると、新しい記憶域システムのコピーマネージャーでレガシ記憶域システムを管理できる場合に、レガシ記憶域システムから新しい記憶域システムにデータを移行することができます。

-   Server1 は、従来の記憶域システムのホストで、Server2 は新しい記憶域システムのホストです。 Server1 は、SMB プロトコルを使用してソース LUN をデータ移行アプリケーションクライアントとして共有し、Server2 は SMB プロトコルを使用して移行先 LUN をデータ移行アプリケーションクライアントとして共有します。 アプリケーションクライアントは、移行元と移行先の両方の LUN にアクセスできます。
-   従来のストレージシステムと新しい記憶域システムは、SAN 構成で同じコピーマネージャーによって管理されます。
-   データ移行アプリケーションクライアントシステムから、コピーオフロードアプリケーションは、ソース LUN にオフロード読み取り要求を発行し、ソース LUN からトークンを受信した後、そのトークンを使用して移行先 LUN にオフロード書き込み要求を発行します。 コピーマネージャーは、2つの異なる場所にある2つの異なるストレージシステム間で、ソース LUN からターゲット LUN にデータを移動します。
-   大規模なデータ移行は、同じ場所にある1つのサーバーでも運用できます。

### <a name="span-idhost-controlleddatatransferwithinatieredstoragedevicespanspan-idhost-controlleddatatransferwithinatieredstoragedevicespanspan-idhost-controlleddatatransferwithinatieredstoragedevicespanhost-controlled-data-transfer-within-a-tiered-storage-device"></a><span id="Host-Controlled_Data_Transfer_within_a_Tiered_Storage_Device"></span><span id="host-controlled_data_transfer_within_a_tiered_storage_device"></span><span id="HOST-CONTROLLED_DATA_TRANSFER_WITHIN_A_TIERED_STORAGE_DEVICE"></span>Tiered Storage デバイス内のホスト制御データ転送

階層型ストレージデバイスは、さまざまな種類の記憶域メディアにデータを分類して、コストを削減し、パフォーマンスを向上させ、容量の問題に対処します。 カテゴリは、必要な保護レベル、パフォーマンス要件、使用頻度、およびその他の考慮事項に基づいて作成できます。

データ移行戦略は、階層型ストレージ戦略の最終的な結果として重要な役割を果たします。 ODX を使用すると、階層化されたストレージデバイス内でホスト制御データを移行できます。 次の図は、階層化されたストレージデバイスの ODX の例を示しています。

-   サーバーは、階層化されたストレージシステムのホストです。 ソース LUN は Tier1 ストレージデバイスで、宛先 LUN は Tier2 ストレージデバイスです。
-   すべての階層型ストレージデバイスは、同じコピーマネージャーによって管理されます。
-   サーバーシステムから、データ移行アプリケーションは、ソース LUN にオフロード読み取り要求を発行し、ソース LUN からトークンを受信してから、そのトークンを使用して移行先 LUN にオフロード書き込み要求を発行します。 コピーマネージャーは、2つの異なる層ストレージデバイスでソース LUN から宛先 LUN にデータを移動します。
-   データ移行タスクが完了すると、アプリケーションは Tier1 ストレージデバイスからデータを削除し、記憶域スペースを解放します。

 

 




