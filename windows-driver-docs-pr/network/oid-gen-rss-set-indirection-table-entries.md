---
title: OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES
description: このトピックでは、OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES をについて説明します
ms.assetid: F59D861C-B7DB-4C28-8842-4FDBAE1B95F1
keywords: OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES、OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES RSSv2
ms.date: 10/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b90bc6a0728d5b257fb1b5fe638d62ecb748b21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581041"
---
[!include[RSSv2 Beta Prerelease](../rssv2-beta-prerelease.md)]

# <a name="oidgenrsssetindirectiontableentries"></a>OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES OID に送信される[RSSv2](receive-side-scaling-version-2-rssv2-.md)-テーブルのエントリを対応のミニポート ドライバーに個々 の間接参照の移動を実行します。 この OID は、[同期 OID](synchronous-oid-request-interface-in-ndis-6-80.md)、つまり NDIS_STATUS_PENDING を返すことはできません。 これが発行される irql = DISPATCH_LEVEL メソッド要求のみと。 

この呼び出しで使用して、 *XxxSynchronousOidRequest*エントリ ポイントで、 *Xxx*か*ミニポート*または*フィルター*の種類に応じてドライバーが要求を受信します。 このエントリ ポイントは、状態を返す、NDIS_STATUS_PENDING を認識した場合に、システムのバグ チェックを実行します。

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES を使用して、 [NDIS_RSS_SET_INDIRECTION_ENTRIES](https://msdn.microsoft.com/library/windows/hardware/9AB69EC6-FE78-4242-89C7-D36AA16676BF)ミニポート アダプタを各アクションが、RSS の 1 つのエントリを移動アクションのセットを同期的に実行するように指示する構造体ターゲットに指定された VPort の間接指定テーブルでは、CPU を指定します。

## <a name="remarks"></a>コメント

この OID は、実行し、それを発行するプロセッサのコンテキスト内に完了する必要があります。 ミニポート ドライバーでは、NDIS_STATUS_SUCCESS を上位の層に戻ったときにこの OID に完全に実行する必要があります。 つまり、NDIS_STATUS_SUCCESS で最初の移動が終了した直後に、新しいプロセッサで複数 ite 用を移動するバックツー バック OID 要求を受信するミニポート ドライバーを準備する必要があります。 

> [!TIP]
> この OID を完全に実行すると、正常に、項目を移動する別のアクションを試行する準備ができて、ミニポート ドライバーである必要がありますを意味します。 実行中は規定はない受信トラフィックは、キューを移動するかできるソースの CPU またはターゲット CPU の直後に示されます。

上位層プロトコルは、OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES ite 用や、プライマリに設定し、既定の異なるプロセッサをポイントするプロセッサのパラメーターを発行します。 

この OID は、いずれかに対して発行できます*active*または*非アクティブな*トラフィックの制御パラメーター。 ハンドル パラメーターの詳細については、[受信側のバージョン 2 (RSSv2) スケーリング](receive-side-scaling-version-2-rssv2-.md)を参照してください。 Ite 用のパラメーターの*非アクティブな*状態では、ミニポート ドライバーの検証および関連する次の RSS 状態 (有効化または無効化) を変更するまでの間に、ターゲットのプロセッサをキャッシュする必要があります。 その時点では、プロセッサの数になるキャッシュされた*active*され、トラフィックを転送するために使用されます。 更新*active*パラメーター (これも検証する必要があります) する必要がありますを直ちに有効に、トラフィックを転送します。

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES をミニポート アダプターに発行する必要があります、 *NDIS_OID_REQUEST_FLAGS_VPORT_ID_VALID*フラグをクリアします。 これは、配列内のさまざまな要素によって参照されている別の拡張の可能性があります。

IRQL でのみこの OID が呼び出される DISPATCH_LEVEL の = =。

ミニポート ドライバーは、テーブル エントリ ・移動の数以上の間接参照操作で情報を提供するように処理するために準備する必要があります、 [NDIS_NIC_SWITCH_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff566583)構造体。 これで定義されている、 **NumberOfIndirectionTableEntriesPerNonDefaultVPort**または**NumberOfIndirectionTableEntriesForDefaultVPort** 、その構造体のメンバーまたは**128**RSS のネイティブ モードでします。

でき、更新数のエントリを実行するミニポート ドライバーを試みる必要がある、 **EntryStatus**のそれぞれに所属[NDIS_RSS_SET_INDIRECTION_ENTRY](https://msdn.microsoft.com/library/windows/hardware/4430E19F-C603-4C52-8FC8-C36197FD2996)操作の結果とします。

### <a name="oid-handler-for-oidgenrsssetindirectiontableentries"></a>OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES の OID ハンドラー

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES の OID ハンドラーは次のように動作するが必要です。

- OID の同期呼び出しの種類により NDIS_STATUS_PENDING の戻り値は許可されていません。
- (以前はリモートのプロセッサで開始された) 現在の CPU が送信先と受信の ITE 移動を確定します。 
- 完全なパラメーターの検証パスを実行するミニポート ドライバーを強くお勧めします。 、できない場合は、配列エントリの 1 つずつ検証および実行を実行します。 ミニポート ドライバーでは、すべての参照先オブジェクトが有効なかどうかは確認する必要があります具体的には。
    - NDIS_STATUS_PENDING を返す、 **EntryStatus**フィールドは、項目は許可されていません。
    - ミニポート アダプターが存在し、正常な状態にします。 それ以外の場合、設定、 **EntryStatus** NDIS_STATUS_ADAPTER_NOT_FOUND、NDIS_STATUS_ADAPTER_NOT_READY などするエントリのフィールド。
    - 各 VPort が存在し、良好な状態にします。 それ以外の場合、設定、 **EntryStatus** NDIS_STATUS_INVALID_PORT、NDIS_STATUS_INVALID_PORT_STATE などするエントリのフィールド。
    - 各間接指定テーブル エントリのインデックスでは、構成済みの範囲です。 この範囲は、0 xffff されているか、[0... NumberOfIndirectionTableEntries - 1] の範囲の設定、 [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md) OID。 0 xffff および 0 xfffe エントリのインデックスは、特別な意味を持ちます。0 xffff は、0 xfffe、プライマリのプロセッサを定義するときに、既定のプロセッサを定義します。 エラーの場合、ハンドラーの設定、 **EntryStatus** NDIS_STATUS_INVALID_PARAMETER するエントリのフィールド。
    - 上位のレイヤーとミニポート ドライバー、項目を移動する前に、現在のプロセッサ (CPU のアクター) を指していることを期待しています。 つまり、リモートで、項目をリダイレクトできません。 これが true でない場合は、設定、 **EntryStatus** NDIS_STATUS_NOT_ACCEPTED するエントリのフィールド。
    - ターゲットのすべてのプロセッサは有効では、ミニポート アダプターの RSS のセットの一部です。 それ以外の場合、設定、 **EntryStatus** NDIS_STATUS_INVALID_DATA するエントリのフィールド。
- その後、またはパラメーターの検証パスの一部として、リソースの状況を検証します。 完全なバッチ (退避) の移動後に使用するキューの数を超えないことを検証、 **NumberOfQueues**設定、 [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://msdn.microsoft.com/library/windows/hardware/96EAB6EE-BF9A-46AD-8DED-5D9BD2B6F219)中に構造体、 [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)要求。 それ以外の場合、NDIS_STATUS_NO_QUEUES が返されます。 NDIS_STATUS_NO_QUEUES をキューの構成済みの数の違反を表すすべての条件に使用する必要があります。 NDIS_STATUS_RESOURCES は、一時的なメモリ不足の条件を指定する場合にのみ使用する必要があります。
- スケーリングのエンティティ (たとえば、VPort) ごとのリソースのチェックの一部として現在の CPU は他の場所に移動するポイントをすべて ite 用とミニポート ドライバーが条件を処理する必要があります.

ミニポート ドライバーが無条件に新しい構成を適用できる必要があり、設定する必要があります、上記のチェックのすべてを渡す場合、 **EntryStatus** NDIS_STATUS_SUCCESS を各エントリのフィールド。

一般に、この OID のハンドラーでは、非常に軽量必要があります。 NDIS は呼び出さないでくださいまたはスピンロックなどの考えられる同期操作のオペレーティング システムがサービス以外の場合と[ **NdisMConfigMSIXTableEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismconfigmsixtableentry)します。

ミニポート ドライバーは、状態または PnP イベントを示す NDIS を呼び出さないでください。

ミニポート ドライバーも使用しないで受信/送信の完了がないこの OID ハンドラーのコンテキストで実行のためには再帰潜在顧客として。 上位のレイヤーでは、受信のコンテキストからこの OID を起動したり、インジケーターを送信することができます。

### <a name="moving-all-indirection-table-entries"></a>すべての間接指定テーブル エントリの移動

ミニポート ドライバーが認識し、現在の CPU からのすべての間接指定テーブル エントリを移動する特別な要求を処理する必要があります。 RSSv2 で操作を行いますので、個々 の項目を移動、ミニポート ドライバーは、全体的な操作の原子性を保証する必要があります。 ミニポート ドライバーが既に実行されたすべてのコマンドを元に戻す必要があり、- コマンドでは、「失敗」として、すべてのコマンドをマークの移動コマンドの対応する配列の処理中に、バッチの途中でエラーが発生した場合**EntryStatus**フィールド。 上層のプロトコルが常に「成功」としてマークされているすべてのコマンドまたは「失敗」としてマークされているすべてのコマンドのいずれかを格納する「ite 用のすべての移動」バッチを要求して、(前に、または後の移行)、トラフィックが、結果の状態を従うこと見なされます。 これはバグの上位レイヤーには、「失敗」としてマークされているいくつかのエントリのみが表示される場合、システムを確認し、原因として、ミニポート ドライバー をポイントします。

「Ite 用のすべての移動」コマンドの処理のミニポート ドライバーを支援するために、デッドロックを回避するには、上層のプロトコルのペアで、バッチ内のグループの移動コマンド**SwitchId + VPortId**フィールド、ように。

- 上位のレイヤーが同じ VPort に「すべてを移動」コマンドの一部としてまとめて実行する必要があるコマンドは、全体的なバッチ内で連続して配置されます。
- ミニポート ドライバーは、全体を実行しようとはしないでくださいコマンドのバッチは、「すべてを移動」の形式でのさまざまな拡張がターゲット可能性があります。 同じ VPort を対象とするコマンドのグループのみ (同じでタグ付け**SwitchId + VPortId**ペア) を実行する必要があります「すべてを移動」セマンティクスに準拠しています。
- 上位のレイヤーでは、この「すべてを移動」のセマンティクスが考慮しません、ときに異なる VPort(s) にコマンドを使用して同じ VPort にコマンドをインターリーブに可能性があります。 この場合、「キューの数」違反のために同じ VPort コマンドの 2 つ目のグループは実行できない場合、ミニポート ドライバーが、対応する状態コード (NDIS_STATUS_NO_QUEUES) では、そのグループをマークし、上位のレイヤーが担当回復します。

たとえば、プロトコル レイヤーの上にある場合は、一連のこのようなコマンドを 2 等分します。

- `VPort=1 ITE[0,1]`
- `VPort=2 ITE[0]`
- `VPort=1 ITE[2]`

ミニポート ドライバーがアトミックに、すべての 4 つの移動コマンドを実行しようとする必要がないか、3 つすべてのコマンドを移動する`VPort=1`(`ITE[0,1,2]`)。 のみを実行する必要があります、 `VPort=1 ITE[0,1]` 「すべてを移動」に、グループ、`VPort=2 ITE[0]`グループ化し、`VPort=1 ITE[2]`します。 異なる結果を次の 3 つのコマンドのすべてのグループがあります。 グループなど、`VPort=1 ITE[0,1]`と`VPort=2 ITE[0]`が成功したと`VPort=1 ITE[2]`グループが失敗する可能性があります。 対応する結果を反映する必要があります**EntryStatus**各コマンドの構造体のメンバー。 これにより、ミニポート ドライバーは、全体的なバッチ (たとえば、ロック、全体のアダプター) の安全な実行の予防措置には必要ありません。 コマンドのみを特定 VPort のターゲットがシリアル化する必要があります、細かい単位あたりの VPort のロックは使用できますが、および特定のデッドロックを回避します。

> [!NOTE]
> 同じエントリ状態では、コマンドのエントリのグループ全体をマークする必要があります。

### <a name="error-conditions-and-status-codes"></a>エラー状況と状態コード

この OID では、エラーが発生したときに、次のステータス コードが返されます。

| 状態コード | エラー状況 |
| --- | --- |
| NDIS_STATUS_INVALID_LENGTH | OID が正しくありません。 |
| NDIS_STATUS_INVALID_PARAMETER | 無効な値を含むヘッダーまたは OID 自体で (ただし個々 のコマンドのエントリではなく) どちらか、他のフィールド。 |

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

- [Receive Side Scaling バージョン 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)
- [NDIS_RSS_SET_INDIRECTION_ENTRIES](https://msdn.microsoft.com/library/windows/hardware/9AB69EC6-FE78-4242-89C7-D36AA16676BF)
- [NDIS_RSS_SET_INDIRECTION_ENTRY](https://msdn.microsoft.com/library/windows/hardware/4430E19F-C603-4C52-8FC8-C36197FD2996)
- [NDIS_NIC_SWITCH_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff566583)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://msdn.microsoft.com/library/windows/hardware/96EAB6EE-BF9A-46AD-8DED-5D9BD2B6F219)

