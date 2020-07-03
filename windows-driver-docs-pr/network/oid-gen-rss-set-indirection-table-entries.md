---
title: OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES
description: このトピックでは、について説明し OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES
ms.assetid: F59D861C-B7DB-4C28-8842-4FDBAE1B95F1
keywords: OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES、OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES RSSv2
ms.date: 10/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e922335372512effda090610f7928c668e3d142
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916609"
---
# <a name="oid_gen_rss_set_indirection_table_entries"></a>OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES

[!include[RSSv2 Beta Prerelease](../includes/rssv2-beta-prerelease.md)]

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES OID は、個々の間接テーブルエントリの移動を実行するために[RSSv2](receive-side-scaling-version-2-rssv2-.md)対応ミニポートドライバーに送信されます。 この OID は[同期 oid](synchronous-oid-request-interface-in-ndis-6-80.md)であるため、NDIS_STATUS_PENDING を返すことはできません。 このメソッドは、IRQL = = DISPATCH_LEVEL でメソッド要求のみとして発行されます。 

この呼び出しでは、 *XxxSynchronousOidRequest*エントリポイントが使用されます。ここで、 *Xxx*は、要求を受信するドライバーの種類に応じて*ミニポート*または*フィルター*です。 このエントリポイントを指定すると、NDIS_STATUS_PENDING が返されます。

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES は、 [NDIS_RSS_SET_INDIRECTION_ENTRIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entries)構造を使用して、一連のアクションを同期的に実行するようにミニポートアダプターに指示します。各アクションは、指定された VPORT の RSS 間接テーブルの1つのエントリを、指定された CPU に移動します。

## <a name="remarks"></a>注釈

この OID は、それを発行したプロセッサコンテキストで実行され、完了する必要があります。 ミニポートドライバーは、NDIS_STATUS_SUCCESS を上位層に返すときに、この OID を完全に実行する必要があります。 これは、最初の移動が NDIS_STATUS_SUCCESS で終了した直後に新しいプロセッサで複数のデバイスを移動するために、バックツーバックの OID 要求を受信するようにミニポートドライバーで準備する必要があることを意味します。 

> [!TIP]
> この OID を完全に実行すると、予備を移動するための別の操作を正常に実行するために、ミニポートドライバーが準備されている必要があります。 転送中の受信トラフィックがキューの移動直後に示されます。これは、ソース CPU またはターゲット CPU 上に配置できます。

上層のプロトコルは、異なるプロセッサをポイントするように設定したり、プライマリおよび既定のプロセッサパラメーターを指定したりするために OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES を発行します。 

この OID は、アクティブまたは*非アクティブ**な*トラフィックステアリングパラメーターに対して発行できます。 パラメーターのステアリングの詳細については、「 [Receive side scaling version 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)」を参照してください。 *非アクティブ*状態のパラメーター/対象となる場合、ミニポートドライバーは、次の関連する RSS 状態の変更 (有効化または無効化) が行われるまで、ターゲットプロセッサを検証してキャッシュする必要があります。 その時点で、キャッシュされたプロセッサ番号が*アクティブ*になり、トラフィックを転送するために使用されます。 *アクティブな*パラメーター (検証も必要) への更新は、トラフィックを転送するために直ちに有効にする必要があります。

*NDIS_OID_REQUEST_FLAGS_VPORT_ID_VALID*フラグをオフにして、OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES をミニポートアダプターに発行する必要があります。 これは、さまざまな VPorts が配列内の異なる要素によって参照されている可能性があるためです。

この OID は、IRQL = = DISPATCH_LEVEL でのみ呼び出されます。

ミニポートドライバーは、 [NDIS_NIC_SWITCH_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造でアドバタイズされるときに、少なくとも1個の間接テーブルエントリの移動アクションを処理するように準備する必要があります。 これは、その構造体の数値**Ofindirection Table個 Pernondefaultvport**メンバーまたは**Number ofindirection table個**、またはネイティブ RSS モードの**128**で定義されています。

ミニポートドライバーは、可能な限り多くのエントリを実行し、各[NDIS_RSS_SET_INDIRECTION_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entry)の**entrystatus**メンバーを操作の結果で更新しようとします。

### <a name="oid-handler-for-oid_gen_rss_set_indirection_table_entries"></a>OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES の OID ハンドラー

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES の OID ハンドラーは、次のように動作することが想定されています。

- OID の同期呼び出しの種類により、NDIS_STATUS_PENDING の戻り値は許可されません。
- 現在の CPU (以前はリモートプロセッサで開始されたもの) に対して送信されたすべての受信 ITE の移動を最終処理します。 
- パラメーターの完全な検証パスを実行するには、ミニポートドライバーを使用することを強くお勧めします。 可能でない場合は、1回だけの配列エントリの検証と実行を実行します。 ミニポートドライバーは、参照されているすべてのオブジェクトが有効かどうかを具体的に確認する必要があります。
    - ITE の**Entrystatus**フィールドに NDIS_STATUS_PENDING を返すことは許可されていません。
    - ミニポートアダプターが存在し、良好な状態です。 それ以外の場合は、エントリの**Entrystatus**フィールドを NDIS_STATUS_ADAPTER_NOT_FOUND、NDIS_STATUS_ADAPTER_NOT_READY などに設定します。
    - 各 VPort は存在し、良好な状態です。 それ以外の場合は、エントリの**Entrystatus**フィールドを NDIS_STATUS_INVALID_PORT、NDIS_STATUS_INVALID_PORT_STATE などに設定します。
    - 各間接テーブルのエントリインデックスは、構成された範囲内にあります。 この範囲は0xFFFF であるか、または[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md) OID によって設定された [0... Number Ofindirection tableentries-1] の範囲にあります。 0xFFFF と0xFFFE エントリのインデックスには特別な意味があります。0xFFFF は既定のプロセッサを定義し、0xFFFE はプライマリプロセッサを定義します。 エラーが発生した場合、ハンドラーはエントリの**Entrystatus**フィールドを NDIS_STATUS_INVALID_PARAMETER に設定します。
    - 上位層とミニポートドライバーは、移動前に、ITE が現在のプロセッサ (アクター CPU) を指していることを想定しています。 つまり、ITE をリモートでリダイレクトすることはできません。 この値が true でない場合は、エントリの**Entrystatus**フィールドを NDIS_STATUS_NOT_ACCEPTED に設定します。
    - すべてのターゲットプロセッサは有効で、ミニポートアダプターの RSS セットに含まれています。 それ以外の場合は、エントリの**Entrystatus**フィールドを NDIS_STATUS_INVALID_DATA に設定します。
- その後、またはパラメーターの検証パスの一部として、リソースの状況を検証します。 完全バッチ移動 (退避) の後に使用されるキューの数が、 [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)要求中に[NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)構造に設定されている**numberofqueues**を超えないことを確認します。 それ以外の場合は NDIS_STATUS_NO_QUEUES が返されます。 構成されたキュー数の違反を表すすべての条件に対して NDIS_STATUS_NO_QUEUES を使用する必要があります。 NDIS_STATUS_RESOURCES は、一時的なメモリ不足状態を指定するためにのみ使用する必要があります。
- リソースチェックの一部として、各スケーリングエンティティ (VPort など) に対して、currrent CPU をポイントするすべてのデバイスが移動されると、ミニポートドライバーは条件を処理する必要があります。「」を参照してください。

上記のすべてのチェックに合格すると、ミニポートドライバーは新しい構成を無条件に適用できる必要があり、各エントリの**Entrystatus**フィールドを NDIS_STATUS_SUCCESS に設定する必要があります。

一般に、この OID のハンドラーは非常に軽量である必要があります。 スピンロックや[**NdisMConfigMSIXTableEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismconfigmsixtableentry)のような同期操作では、以外の NDIS またはオペレーティングシステムサービスを呼び出さないでください。

ミニポートドライバーは、状態または PnP イベントを示すために、NDIS を呼び出すことはできません。

また、ミニポートドライバーは、この OID ハンドラーのコンテキストで、受信/送信の完全な表示を使用しないようにする必要があります。これにより、再帰が発生します。 上位層は、受信または送信の表示コンテキストからこの OID を呼び出すことができます。

### <a name="moving-all-indirection-table-entries"></a>すべての間接テーブルエントリの移動

ミニポートドライバーは、すべての間接テーブルエントリを現在の CPU から離れた場所に移動する特別な要求を認識して処理する必要があります。 RSSv2 は個別の ITE 移動で動作するため、ミニポートドライバーは操作全体の原子性を保証する必要があります。 Move コマンドの対応する配列の処理中にバッチの途中でエラーが発生した場合、ミニポートドライバーは、既に実行されているすべてのコマンドを元に戻し、すべてのコマンドを "失敗" として "コマンドごとの**エントリの状態**" フィールドにマークする必要があります。 上位層プロトコルでは、常に "すべて移動" バッチに "succeeded" とマークされているすべてのコマンド、または "failed" とマークされたすべてのコマンドが含まれていることを前提としています。また、トラフィックが結果の状態 (移動の前または後) であると想定しています。 上位レイヤーに "failed" とマークされたエントリがある場合は、システムを確認し、その原因としてミニポートドライバーをポイントします。

ミニポートドライバーによる "すべて移動" コマンドの処理を支援し、デッドロックを回避するために、上層のプロトコルグループは、次のように**Switchid + VPortId**フィールドのペアでバッチ内のコマンドを移動します。

- "すべて移動" コマンドの一部として、上位層が一緒に実行されるコマンドは、バッチ全体に連続して配置されます。
- ミニポートドライバーは、"すべて移動" の方法で、さまざまな VPorts をターゲットにすることがあるコマンドバッチ全体を実行しようとすることはできません。 同じ VPort (同じ**Switchid + VPortId** pair でタグ付けされたもの) を対象とするコマンドのグループのみ、"すべて移動" セマンティクスに準拠して実行する必要があります。
- 上位層が "すべて移動" セマンティクスを考慮しない場合、コマンドが異なる VPort に対してコマンドを使用して同じ VPort にインターリーブされる可能性があります。 この場合、"キューの数" 違反が原因で同じ VPort に対する2番目のコマンドグループを実行できない場合、ミニポートドライバーは、対応するステータスコード (NDIS_STATUS_NO_QUEUES) を持つグループをマークし、上位層が復旧に責任を持ちます。

たとえば、上層のプロトコルが次のような一連のコマンドを実行しているとします。

- `VPort=1 ITE[0,1]`
- `VPort=2 ITE[0]`
- `VPort=1 ITE[2]`

ミニポートドライバーでは、4つの move コマンドすべて、または () の3つの move コマンドすべてをアトミックに実行する必要はありません `VPort=1` `ITE[0,1,2]` 。 グループを実行する必要があるのは、 `VPort=1 ITE[0,1]` "すべて移動" の方法だけです。その後、グループを実行する必要があり `VPort=2 ITE[0]` `VPort=1 ITE[2]` ます。 3つのコマンドグループはすべて、結果が異なる場合があります。 たとえば、とのグループは `VPort=1 ITE[0,1]` `VPort=2 ITE[0]` 成功する可能性があり、グループは失敗する可能性があり `VPort=1 ITE[2]` ます。 結果は、各コマンド構造の対応する**Entrystatus**メンバーに反映される必要があります。 このように、ミニポートドライバーは、バッチ全体を安全に実行するための対策を講じる必要はありません (たとえば、アダプター全体をロックするなど)。 特定の VPort を対象とするコマンドのみをシリアル化し、より詳細な VPort ロックを使用することができます。また、特定のデッドロックが回避されます。

> [!NOTE]
> コマンドエントリのグループ全体を同じエントリ状態でマークする必要があります。

### <a name="error-conditions-and-status-codes"></a>エラー状態と状態コード

この OID は、エラーが発生したときに次の状態コードを返します。

| 状態コード | エラー状態 |
| --- | --- |
| NDIS_STATUS_INVALID_LENGTH | OID の形式が正しくありません。 |
| NDIS_STATUS_INVALID_PARAMETER | ヘッダーまたは OID 自体に含まれるその他のフィールド (個々のコマンドエントリではありません) には、無効な値が含まれています。 |

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1709**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

- [Receive Side Scaling Version 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)
- [NDIS_RSS_SET_INDIRECTION_ENTRIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entries)
- [NDIS_RSS_SET_INDIRECTION_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entry)
- [NDIS_NIC_SWITCH_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)

