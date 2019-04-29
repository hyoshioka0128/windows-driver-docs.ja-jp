---
title: オフロード データ転送
description: オフロード データ転送
ms.assetid: EDFA6AFB-7D14-44F8-A105-E74182D26398
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5ba3fad840820d8c772e645220f3d12fd0705be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389421"
---
# <a name="offloaded-data-transfer"></a>オフロード データ転送


## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要


オフロード データ転送 (ODX) では、記憶域デバイス上のデータ移動をトークン化された操作について説明します。 ソース ファイルとコピー先のファイルは、同じボリューム、同じコンピューター、ローカル ボリュームと SMB2 を使ってリモート ボリュームでホストされている 2 つの異なるボリュームまたは SMB2 を 2 つの異なるコンピューター上の 2 つのボリュームに配置できます。 オフロード データ転送は、Windows 8 で導入されました。

次は ODX を使用して、コピー オフロード操作プロセスです。

1.  コピーのオフロード アプリケーションでは、ソース ストレージ デバイスのコピー マネージャーに、オフロードの読み取り要求を送信します。
2.  アプリケーションでは、コピー マネージャーに受信オフロード結果の読み取り要求を送信し、トークンを返します。 トークンは、データのコピーを表したものです。
3.  アプリケーションでは、コピー マネージャー、変換先のストレージ デバイスに、トークンを使用してオフロード書き込み要求を送信します。
4.  アプリケーションでは、コピー マネージャーに受信オフロード書き込み結果の要求を送信します。 コピー マネージャーは、ソースからデータを送信先に移動し、アプリケーションをオフロード書き込みの結果を返します。

## <a name="span-ididentifyanodx-capablesourceanddestinationspanspan-ididentifyanodx-capablesourceanddestinationspanspan-ididentifyanodx-capablesourceanddestinationspanidentify-an-odx-capable-source-and-destination"></a><span id="Identify_an_ODX-Capable_Source_and_Destination"></span><span id="identify_an_odx-capable_source_and_destination"></span><span id="IDENTIFY_AN_ODX-CAPABLE_SOURCE_AND_DESTINATION"></span>ODX 対応のソースと変換先を識別します。


ODX をサポートするには、記憶域配列は、関連する T10 標準仕様を実装する必要があります。 識別されると、ODX 対応記憶域配列、オフロードが読み取りおよび書き込み操作、および既知のトークンと書き込みの負荷を軽減します。 LUN デバイスは、(システムのブートまたはプラグ アンド プレイ イベント) を列挙します。 Windows では、収集または、次の手順で記憶域ターゲット デバイスの ODX 機能の情報を更新します。

1.  クエリのコピーは、機能をオフロードします。
2.  コピーの必須パラメーターの操作と制限事項のオフロードを収集します。

既定では、Windows が ODX パス最初コピー操作の場合は、ソースとターゲット Lun の両方が ODX 対応。 Windows がソースとターゲット LUN の組み合わせをマークする記憶域デバイスには、ODX の最初の要求が失敗した場合、として、"しない ODX 対応"のパス。

## <a name="span-idodxreadwriteoperationsspanspan-idodxreadwriteoperationsspanspan-idodxreadwriteoperationsspanodx-readwrite-operations"></a><span id="ODX_Read_Write_Operations"></span><span id="odx_read_write_operations"></span><span id="ODX_READ_WRITE_OPERATIONS"></span>ODX の読み取り/書き込み操作


### <a name="span-idsynchronouscommandadoptionandapisspanspan-idsynchronouscommandadoptionandapisspanspan-idsynchronouscommandadoptionandapisspansynchronous-command-adoption-and-apis"></a><span id="Synchronous_Command_Adoption_and_APIs"></span><span id="synchronous_command_adoption_and_apis"></span><span id="SYNCHRONOUS_COMMAND_ADOPTION_AND_APIS"></span>同期コマンドの導入と Api

Windows 同期オフロードでは、読み取り、操作を書き込みます。 大規模なオフロード書き込み要求は、堅牢な同期オフロード書き込みを確実に、次のアルゴリズムを使用して分割されます。

-   ターゲット記憶域デバイスは、最適な転送サイズを提供していない場合は、64 MB で、最適な転送サイズを設定します。
-   最適な転送サイズの記憶域のターゲット デバイスで指定された、最適な転送サイズは 256 MB 未満の場合、0 より大きくします。
-   設定対象のデバイスで最適な転送サイズが 256 MB より大きい場合は、256 MB に最適な転送サイズを設定します。

同期のオフロードの読み取りおよびオフロードは、SCSI コマンドは、MPIO のコンプリケーションを減らすし、クラスターのフェールオーバーのシナリオを記述します。 Windows では、4 秒以内に同期オフロード読み取り/書き込みの SCSI コマンドを完了するコピー マネージャーが必要です。

アプリケーションは、FSCTL、DSM の IOCTL または SCSI を使用できます\_渡す\_Api を介して記憶域配列を操作し、コピーを実行する操作の負荷を軽減します。 データの破損またはシステムが不安定になるを避けるためには、Windows は、ボリュームを取得する最初の排他アクセスなしのファイル システムでマウントされているボリュームに直接書き込むからアプリケーションを制限します。 これは、ボリュームへの書き込み、ファイル システム書き込みと競合する条件です。 このような競合が発生すると、ボリュームの内容が矛盾した状態で残る可能性が。

### <a name="span-idoffloadreadoperationsspanspan-idoffloadreadoperationsspanspan-idoffloadreadoperationsspanoffload-read-operations"></a><span id="Offload_Read_Operations"></span><span id="offload_read_operations"></span><span id="OFFLOAD_READ_OPERATIONS"></span>読み取り操作の負荷を軽減します。

オフロードの読み取り、アプリケーションの要求がトークンの有効期間 (アイドル タイムアウト) を指定できます。 アプリケーションでトークンの有効期間を 0 に設定すると、既定の非アクティブ タイマーがトークンの有効期間として使用されます。 記憶域配列のコピー マネージャーの管理し、アイドル タイムアウト値と資格情報に従ってトークンを検証します。 Windows ホストでは、64 ファイル フラグメントの数も制限されます。 場合は、オフロードでは、要求から成る 64 を超えるフラグメントを読み取り、Windows は、コピー オフロードが要求は失敗しは、従来のコピー操作に戻ります。

読み取り要求をオフロードの完了後、コピー マネージャーは receive オフロード読み取り結果コマンドのデータ (ROD) トークンの表現を準備します。 ROD トークン フィールドには、ユーザー データと保護情報の特定の時点の表現を指定します。 ROD には、「排他的開いている」または「共有で開く」の形式でユーザー データを指定できます。 コピー マネージャーは、その ROD のポリシー設定に従って、トークンが無効になることができます。 ROD が開いている場合は、専用のコピー操作をオフロード、ROD の変更や移動 ROD トークンを無効にすることができます。 ROD が「開いている共有を使用した」の形式である場合は、ROD トークンの値は、ROD が変更されたときに有効です。

| サイズ (バイト単位) | トークンの内容 |
|---------------|----------------|
| 4             | ROD トークンの種類 |
| 508           | ROD トークンの ID   |

 

ROD トークンを付与、記憶域配列でのみ使用されるため、その形式は、非透過、一意かつ高度なセキュリティが。 トークンは、変更、いない検証、または有効期限が切れて場合、コピー マネージャーは、オフロードの書き込み操作中に、トークンを無効にできます。 操作が、非アクティブ タイムアウト値をコピー マネージャー保つ必要があるトークン [次へ] を使用してトークンを書き込む使用量に対して有効な秒数を示すために、オフロードから返された ROD トークンの読み取り。

### <a name="span-idoffloadwriteoperationsspanspan-idoffloadwriteoperationsspanspan-idoffloadwriteoperationsspanoffload-write-operations"></a><span id="Offload_Write_Operations"></span><span id="offload_write_operations"></span><span id="OFFLOAD_WRITE_OPERATIONS"></span>書き込み操作の負荷を軽減します。

コピー マネージャーから ROD トークンを受信した後は、アプリケーションは、記憶域配列のコピー マネージャーに ROD トークンを使用してオフロード書き込み要求を送信します。 ターゲット デバイスに同期オフロード書き込みコマンドが送信されると、Windows は 4 秒間、コマンドの完了にコピー マネージャーが必要です。 コマンドのタイムアウトまたは他のエラー状態のため、コマンドを終了すると、Windows では、コマンドが失敗します。 アプリケーションは、返されるステータス コードに従ってレガシ コピー操作にフォールバックします。

1 つまたは複数のオフロード書き込み結果が表示されるコマンドを使用してオフロードの書き込み要求を行うことができます。 オフロード書き込みが部分的に完了した場合は、コピー マネージャーが推定の遅延時間を返し、コピーの進行状況を示す転送の数をカウントします。 転送のカウント数は、変換先のメディアにエラーが発生せず、ソースから書き込まれた連続の論理ブロックの数を指定します。 コピー マネージャーには、順次のオフロード書き込みまたはスキャッター/ギャザー パターンを実行できます。

書き込みエラーが発生したときに、コピーの進行状況は、エラー ブロックに最初の論理ブロックからの連続した論理ブロックをカウントします。 クライアント アプリケーションまたはコピー エンジンには、書き込みエラーのブロックからオフロード書き込みが再開します。 オフロード書き込みが完了したら、コピー マネージャーは、0 に設定され、進行状況を 100% のデータ転送量の推定状態更新プログラムの遅延が ROD のトークン情報が表示されるコマンドを完了します。 場合は、受信の負荷を軽減書き込み結果が同じ進行状況のデータ転送の数を返します、Windows を 4 回の再試行後にアプリケーションにコピー操作は失敗します。

クライアント アプリケーションでは、よく知られている ROD トークンを使用してオフロード書き込み操作も実行できます。 これは、既知のデータのパターンとトークンの形式で定義済み ROD トークンです。 1 つの一般的な実装には、0 個のトークンは呼び出されます。 クライアント アプリケーションは、0 個のトークンを使用して、0 での論理ブロックの 1 つまたは複数の範囲を入力することができます。 場合は、よく知られているトークンがサポートされていないか、認識可能なコピー マネージャーが失敗した「トークンが無効です」で書き込み要求をオフロードします。

| サイズ (バイト単位) | トークンの内容     |
|---------------|--------------------|
| 4             | ROD トークンの種類     |
| 2             | 既知のパターン |
| 506           | ROD トークンの ID       |

 

よく知られている ROD トークンを使用してオフロードの書き込みをクライアント アプリケーションは、よく知られているトークンの要求を読み取り、オフロードを使用できません。 コピー マネージャーは、ことを確認し、独自のポリシーに従って、よく知られている ROD トークンを保持します。

### <a name="span-idperformancetuningparametersofodximplementationspanspan-idperformancetuningparametersofodximplementationspanspan-idperformancetuningparametersofodximplementationspanperformance-tuning-parameters-of-odx-implementation"></a><span id="Performance_Tuning_Parameters_of_ODX_Implementation"></span><span id="performance_tuning_parameters_of_odx_implementation"></span><span id="PERFORMANCE_TUNING_PARAMETERS_OF_ODX_IMPLEMENTATION"></span>パフォーマンス チューニングの ODX の実装のパラメーター

ODX のパフォーマンスは、クライアントとサーバー間のネットワークまたは SAN のサーバーと記憶域配列間のトランスポート リンクの速度に依存しません。 コピー マネージャーと記憶域配列のデバイスのサーバーでデータを移動します。

ODX のテクノロジからメリットをすべてコピーにオフロードします。 たとえば、1 ギガ ビット iSCSI ストレージ アレイのコピー マネージャーは 10 秒以内/3 GB のファイルのコピーを完了する可能性があり、データの転送速度は 1 秒あたり 300 MB より大きくなります。 データの転送速度は、1 ギガ ビット イーサネット インターフェイスの理論上の最大転送速度を既によりもします。

すべてのファイル サイズ コピー オフロードは、Windows ODX のテクノロジから利益を得ることが。 特定のサイズのファイルのコピーのパフォーマンスが ODX テクノロジを活用できないことことができます。 ODX を使用できるパフォーマンスを最適化する最小ファイル サイズとコピーの最大長を許容する制限します。 ODX のパフォーマンスをチューニングするには、次のパラメーターを調整します。

Windows では、オフロード操作用のファイルの最小サイズ要件を設定します。 現時点では、コピー エンジンで、256 KB に最小コピー オフロード ファイルのサイズを設定します。 ファイルが 256 KB 未満の場合、コピー エンジンのコピー (レガシ) プロセスにフォールバックします。

Windows ホストは、トークンの最大転送サイズを使用し、オフロードの最適な転送サイズを準備する最適な転送量は、読み取りまたは SCSI コマンドを記述します。 ブロックの数の合計の転送サイズは、トークンの最大転送サイズを超えない必要があります。 記憶域配列が、最適な転送の数を報告しない場合、Windows は、既定の数として 64 MB を使用します。

転送の最適なと最大長のパラメーターは、1 つの範囲の記述子で最適かつ最大ブロック数を指定します。 コピー オフロード アプリケーションは、最適なファイル転送のパフォーマンスを実現するためにこれらのパラメーターに準拠できます。

## <a name="span-idodxerrorhandlingandhighavailabilitysupportspanspan-idodxerrorhandlingandhighavailabilitysupportspanspan-idodxerrorhandlingandhighavailabilitysupportspanodx-error-handling-and-high-availability-support"></a><span id="ODX_Error_Handling_and_High_Availability_Support"></span><span id="odx_error_handling_and_high_availability_support"></span><span id="ODX_ERROR_HANDLING_AND_HIGH_AVAILABILITY_SUPPORT"></span>ODX のエラー処理と高可用性のサポート


ODX 操作には、ファイル コピーの要求が失敗した場合、コピー エンジンと Windows ファイル システム (NTFS) フォールバックはレガシ コピー操作にします。 コピーは、オフロードの書き込み操作の途中で失敗をオフロード、コピー エンジンと NTFS がオフロード書き込みでは、最初の障害点からレガシ コピー操作を再開します。

ODX を使用して、コピー オフロード操作のアルゴリズムを次に示します。

### <a name="span-idodxerrorhandlingspanspan-idodxerrorhandlingspanspan-idodxerrorhandlingspanodx-error-handling"></a><span id="ODX_Error_Handling"></span><span id="odx_error_handling"></span><span id="ODX_ERROR_HANDLING"></span>ODX のエラー処理

ODX は、堅牢なエラー処理のアルゴリズムに従って、記憶域配列の機能を使用します。 場合は、コピー オフロード、ODX 対応のパスでエラーと、Windows ホストは、従来のコピー操作にフォールバックするアプリケーションが必要です。 この時点では、Windows のコピー エンジンが、「従来のコピーにへの切り替え」メカニズムを実装済みです。 後、コピーは、障害をオフロード、NTFS、ソースとターゲット LUN としてマーク ODX に対応していない 3 分間します。 この期間が経過した後、Windows は ODX 操作エンジンの再試行をコピーします。 記憶域配列は、この機能を使用して、ストレスを感じ状況の中にいくつかのパスで ODX サポートを一時的に無効にできます。

### <a name="span-idodxfailoverinmpioandclusterserverconfigurationsspanspan-idodxfailoverinmpioandclusterserverconfigurationsspanspan-idodxfailoverinmpioandclusterserverconfigurationsspanodx-failover-in-mpio-and-cluster-server-configurations"></a><span id="ODX_Failover_in_MPIO_and_Cluster_Server_Configurations"></span><span id="odx_failover_in_mpio_and_cluster_server_configurations"></span><span id="ODX_FAILOVER_IN_MPIO_AND_CLUSTER_SERVER_CONFIGURATIONS"></span>ODX のフェールオーバーでは、MPIO と、クラスター サーバーの構成

読み取りの負荷を軽減し、書き込み操作の完了または同じストレージのリンクからキャンセルする必要があります (は\_T nexus)。

同期オフロード中に、MPIO またはクラスターにサーバーのフェールオーバーが発生する場合は、読み取りまたは書き込み操作では、Windows は、次のアルゴリズムを使用してフェールオーバーを処理します。

1.  同期のオフロードの読み取り/書き込みコマンド。
2.  MPIO の構成で、Windows は、MPIO パスのフェールオーバー後に失敗したコマンドを再試行します。 コマンドが再度失敗した場合は、次の Windows。
    -   クラスター サーバーのフェールオーバー オプション – なしは、Windows は、リセット記憶装置に LUN を発行し、アプリケーションに、I/O エラーの状態を返します。
    -   クラスター サーバーのフェールオーバー オプション – では、Windows は、クラスターのサーバー ノードのフェールオーバーを開始します。

3.  クラスター サーバーの構成-クラスターの記憶域サービスが次の推奨するクラスター ノードにフェールオーバーとクラスターのストレージ サービスを再開します。 オフロード アプリケーションは、クラスターに対応するクラスター記憶域サービスのフェールオーバー後に、オフロード読み取り/書き込みコマンドを再試行することである必要があります。

場合は、オフロードの読み取りまたは書き込みコマンドは、MPIO パスとクラスター ノードのフェールオーバー後に失敗しました、Windows は、フェールオーバー後に、記憶域デバイスをリセット LUN を発行します。 記憶装置に未処理のすべてのコマンドが終了して、保留中の LUN の下の操作。

現時点では、Windows オフロードの非同期読み取りを発行したりしない記憶域スタックから SCSI コマンドの記述。

## <a name="span-idodxusagemodelsspanspan-idodxusagemodelsspanspan-idodxusagemodelsspanodx-usage-models"></a><span id="ODX_Usage_Models"></span><span id="odx_usage_models"></span><span id="ODX_USAGE_MODELS"></span>ODX の使用モデル


### <a name="span-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanspan-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanspan-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanodx-across-physical-disk-virtual-hard-disk-and-smb-shared-disk"></a><span id="ODX_across_Physical_Disk__Virtual_Hard_Disk_and_SMB_Shared_Disk"></span><span id="odx_across_physical_disk__virtual_hard_disk_and_smb_shared_disk"></span><span id="ODX_ACROSS_PHYSICAL_DISK__VIRTUAL_HARD_DISK_AND_SMB_SHARED_DISK"></span>ODX の物理ディスク、仮想ハード ディスクと SMB の間で共有ディスク

ODX 操作を実行するには、アプリケーション サーバーは、両方のソース LUN と読み取り/書き込み権限を持つターゲット LUN へのアクセスが必要です。 コピーのオフロード アプリケーションでは、ソース LUN への要求を読み取り、オフロードを発行し、ソース LUN のコピー マネージャーからトークンを受け取ります。 コピーは、ターゲット LUN にオフロードの書き込み要求を発行するトークンをアプリケーションの使用にオフロードします。 コピー マネージャーはし、記憶域ネットワークを通じてターゲット LUN に、ソース LUN からデータを移動します。

### <a name="span-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanodx-operation-with-one-server"></a><span id="ODX_Operation_with_One_Server"></span><span id="odx_operation_with_one_server"></span><span id="ODX_OPERATION_WITH_ONE_SERVER"></span>1 つのサーバーで ODX 操作

1 台サーバー構成では、コピーは、アプリケーションのオフロードは、読み取りし、書き込み要求を同じサーバー システムの問題をオフロードします。

### <a name="span-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanodx-operation-with-one-server"></a><span id="ODX_Operation_with_One_Server"></span><span id="odx_operation_with_one_server"></span><span id="ODX_OPERATION_WITH_ONE_SERVER"></span>1 つのサーバーで ODX 操作

1 台サーバー構成では、コピーは、アプリケーションのオフロードは、読み取りし、書き込み要求を同じサーバー システムの問題をオフロードします。

前の図に Server1 または仮想マシン 1 がへのアクセス両方のソース LUN (VHD1 または物理ディスク 1) とターゲット LUN (VHD2 または物理ディスク 2)。 コピー オフロード オフロード読み取りをソース LUN を要求し、LUN、ソースからのトークンを受け取るアプリケーションの問題とし、コピー オフロードをアプリケーションで使用するターゲット LUN にオフロードの書き込み要求を発行するトークン。 コピー マネージャーは、同じ記憶域配列内のターゲット LUN に LUN のソースからデータを移動します。

### <a name="span-idodxoperationwithtwoserversspanspan-idodxoperationwithtwoserversspanspan-idodxoperationwithtwoserversspanodx-operation-with-two-servers"></a><span id="ODX_Operation_with_Two_Servers"></span><span id="odx_operation_with_two_servers"></span><span id="ODX_OPERATION_WITH_TWO_SERVERS"></span>2 つのサーバーで ODX 操作

2 台のサーバー構成では、2 つのサーバーと同じコピー マネージャーによって管理される複数の記憶域配列があります。

-   Server1 または仮想マシン 1 は、ソース LUN のホストと Server2 または仮想マシン 2 はターゲット LUN のホスト。 Server1 では、SMB プロトコルを使用してクライアント アプリケーションとソース LUN を共有し、Server2 は、SMB プロトコルを使用して、アプリケーション クライアントとターゲット LUN を共有することもできます。 アプリケーションのクライアントには、LUN をソースとターゲット LUN へのアクセスがあります。
-   ソースと宛先のストレージ アレイは、SAN の構成で同じコピー マネージャーによって管理されます。
-   アプリケーションのクライアント システムからは、コピーは、アプリケーションのオフロード読み取りを要求ソース LUN に LUN をソースからのトークンを受け取るし、トークンを使用してターゲット LUN にオフロードの書き込み要求を発行の問題をオフロードします。 コピー マネージャーは、2 つの異なる場所に 2 つの異なる記憶域配列間でのターゲット LUN に LUN のソースからデータを移動します。

### <a name="span-idmassivedatamigrationspanspan-idmassivedatamigrationspanspan-idmassivedatamigrationspanmassive-data-migration"></a><span id="Massive_Data_Migration"></span><span id="massive_data_migration"></span><span id="MASSIVE_DATA_MIGRATION"></span>大量のデータの移行

大量のデータの移行は、新しいシステムに大量のデータベース レコード、スプレッドシート、テキスト ファイル、スキャンしたドキュメント、画像などのデータをインポートするプロセスです。 ストレージ システムのアップグレードや、データベース エンジンに新しいアプリケーションまたはビジネス プロセスの変更では、データの移行が考えられます。 新しい記憶域システムのコピー マネージャーによって、従来の記憶域システムを管理することができる場合、新しい記憶域システム、従来の記憶域システムからデータを移行する ODX を使用できます。

-   Server1 は、従来の記憶域システムのホストと Server2 は、新しい記憶域システムをホストします。 Server1 は SMB プロトコルを使用してデータ移行アプリケーション クライアントとしてソース LUN を共有し、Server2 は、SMB プロトコルを使用してデータ移行アプリケーション クライアントとしてターゲット LUN を共有します。 アプリケーションのクライアントには、ソースとターゲット LUN へのアクセスがあります。
-   従来の記憶域システムと新しい記憶域システムは、SAN の構成で同じコピー マネージャーによって管理されます。
-   データ移行アプリケーションのクライアント システムからは、コピーは、アプリケーションのオフロード読み取りを要求ソース LUN に LUN をソースからのトークンを受け取るし、トークンを使用してターゲット LUN にオフロードの書き込み要求を発行の問題をオフロードします。 コピー マネージャーは、2 つの異なる場所にある 2 つの別のストレージ システムにターゲット LUN に LUN のソースからデータを移動します。
-   大量のデータの移行は、同じ場所にある 1 つのサーバーでも運用する可能性があります。

### <a name="span-idhost-controlleddatatransferwithinatieredstoragedevicespanspan-idhost-controlleddatatransferwithinatieredstoragedevicespanspan-idhost-controlleddatatransferwithinatieredstoragedevicespanhost-controlled-data-transfer-within-a-tiered-storage-device"></a><span id="Host-Controlled_Data_Transfer_within_a_Tiered_Storage_Device"></span><span id="host-controlled_data_transfer_within_a_tiered_storage_device"></span><span id="HOST-CONTROLLED_DATA_TRANSFER_WITHIN_A_TIERED_STORAGE_DEVICE"></span>階層型記憶域デバイスで、ホストの管理対象のデータ転送します。

階層型記憶域デバイスは、コストの削減、パフォーマンスを向上させるし、容量の問題に対処するストレージ メディアの種類ごとにデータを分類します。 カテゴリは、必要な保護のレベル、パフォーマンス要件、使用量の頻度およびその他の考慮事項に基づいて作成できます。

データ移行の戦略は、階層型記憶域の戦略の最終的な結果で重要な役割を果たします。 ODX は、階層型記憶域デバイス内のホストの管理対象データ移行できます。 階層型記憶域デバイスで ODX の例を次の図に示します

-   サーバーは、階層型記憶域システムのホストです。 ソース LUN は、レベル 1 の記憶装置とターゲット LUN がレベル 2 の記憶域デバイス。
-   すべての階層型記憶域デバイスは、同じコピー マネージャーによって管理されます。
-   サーバーのシステムからは、データ移行のアプリケーションはソース LUN への要求を読み取り、オフロードの問題、LUN、ソースからのトークンを受け取るし、トークンを使用してターゲット LUN にオフロードの書き込み要求を発行します。 コピー マネージャーは、2 つの異なる層ストレージ デバイス間でのターゲット LUN に LUN のソースからデータを移動します。
-   データ移行タスクが完了したら、アプリケーションは、レベル 1 のストレージ デバイスからデータを削除し、記憶域スペースを解放します。

 

 




