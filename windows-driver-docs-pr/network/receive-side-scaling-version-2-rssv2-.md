---
title: Receive Side Scaling Version 2 (RSSv2)
description: このトピックでは、Receive Side Scaling バージョン 2 (RSSv2) について説明します。
ms.assetid: 192CAA41-0D17-4C06-8F13-68EA7C26D023
keywords: Receive Side Scaling Version 2、RSSv2、Receive Side Scaling Version 2 WDK、RSSv2 network drivers
ms.date: 10/12/2017
ms.localizationpriority: medium
ms.openlocfilehash: f87f7ff282891fead1912f8815a8692ddc72ccbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844859"
---
# <a name="receive-side-scaling-version-2-rssv2"></a>Receive Side Scaling Version 2 (RSSv2)

[!include[RSSv2 Beta Prerelease](../rssv2-beta-prerelease.md)]

[Receive Side Scaling](ndis-receive-side-scaling2.md)は、マルチプロセッサシステムでのネットワークデータの処理に関連するシステムパフォーマンスを向上させます。 NDIS 6.80 以降では、RSS バージョン 2 (RSSv2) がサポートされています。これは、キューの動的な VPort 分散を提供することで RSS を拡張します。

## <a name="overview"></a>概要

RSSv1 と比較すると、RSSv2 は CPU 負荷の測定と間接テーブルの更新の間の時間を短縮します。 これにより、トラフィックが多い状況での遅延が回避します。 これを実現するために、RSSv2 は、要求を処理するプロセッサコンテキストで、IRQL = DISPATCH_LEVEL でアクションを実行し、現在のプロセッサを指す間接テーブルエントリのサブセットでのみ動作します。 つまり、RSSv2 は、RSSv1 よりもはるかに多くの応答性を複数のプロセッサに動的に分散させることができます。

RSSv2 では、2つの Oid、 [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)と[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)が導入されており、適切な RSS 機能を設定し、間接テーブルを制御するためにミニポートドライバーを使用できます。 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 は通常の OID ですが、OID_GEN_RSS_SET_INDIRECTION_ENTRIES は NDIS_STATUS_PENDING を返すことができない同期 OID です。 これらの Oid の詳細については、個々の参照ページを参照してください。 同期 Oid の詳細については、「 [NDIS 6.80 の同期 oid 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)」を参照してください。

## <a name="rssv2-terminology"></a>RSSv2 の用語

このトピックでは、次の用語を使用します。

| 用語 | 定義 |
| --- | --- |
| RSSv1 | 最初のジェネレーション受信側のスケーリング機構。 [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)を使用します。 |
| RSSv2 | このトピックで説明している Windows 10 バージョン1803以降でサポートされている第2世代の receive side scaling のメカニズム。 |
| エンティティのスケーリング| ミニポートアダプター自体がネイティブ RSS モードの場合は、RSSv2 モードの場合は VPort です。 |
| I) | 指定されたスケーリングエンティティの間接テーブルエントリ (ITE)。 VPort あたりの総接続数は、VMQ モードの場合は number **Ofindirection tableの**値を、ネイティブの RSS の場合は 128**以下にする**ことはできません。 数値**Ofindirection Table個 Pernondefaultpfvport**と**番号 Ofindirection Tableare fordefaultvport**は[NDIS_NIC_SWITCH_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体のメンバーです。 |
| スケーリングモード | 実行時にどのように処理されるかを制御する、VPort の vmswitch ポリシー。 これは、静的な場合もあります (負荷の変更による ITE の移動はありません)。または、現在のトラフィック負荷に応じた拡張と合体です。 |
| キュー | ITE をバックする基になるハードウェアオブジェクト (キュー)。 ハードウェアと間接参照テーブルによっては、構成キューが複数の場合があります。 キューの総数 (既定のキューによって使用されるキューを含む) は、通常、管理者によって設定される構成済みの制限を超えることはできません。 |
| 既定のプロセッサ | ハッシュを計算できないパケットを受信するプロセッサ。 各 VPort には既定のプロセッサがあります。
| プライマリプロセッサ | VPort の作成時に[NDIS_NIC_SWITCH_VPORT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)構造体の**processoraffinity**メンバーとして指定されたプロセッサ。 このプロセッサは実行時に更新でき、VMQ トラフィックの送信先を指定します。 |
| ソース CPU | ITE が現在マップされているプロセッサ。 |
| ターゲット CPU | RSSv2 を使用して、ITE を再マップする対象のプロセッサ。 |
| アクター CPU | RSSv2 要求が行われているプロセッサ。 |

## <a name="advertising-rssv2-capability-in-a-miniport-driver"></a>ミニポートドライバーで RSSv2 機能をアドバタイズする

ミニポートドライバーは、 [NDIS_RECEIVE_SCALE_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)構造体の**CapabilitiesFlags**メンバーに*NDIS_RSS_CAPS_SUPPORTS_INDEPENDENT_ENTRY_MOVE*フラグを設定して、RSSv2 サポートをアドバタイズします。 この機能は、RSSv2's CPU 負荷分散機能を有効にするために必要です。これは、既定以外の VPorts (VMQs) に対して RSSv1 動的分散を有効にする*NDIS_RECEIVE_FILTER_DYNAMIC_PROCESSOR_AFFINITY_CHANGE_SUPPORTED*フラグと共に使用します。

> [!NOTE]
> 上層プロトコルは、既定の VPort のプライマリプロセッサを RSSv2 ミニポートドライバー用に移動できることを前提としています。

ミニポートアダプターで RSSv2 機能をアドバタイズしない場合、これらの VPorts が動的拡散を実行するように要求されていても、すべての VMQ が有効な VPorts が静的拡散モードのままになります。 RSS パラメーター [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)を構成するための RSSv1 OID は、これらの vports が静的拡散モードのままで使用されます。

ミニポートドライバーは、RSSv1 または RSSv2 のいずれか1つの RSS 制御機構を実装するだけでかまいません。 ドライバーが RSSv2 サポートをアドバタイズした場合、NDIS は RSSv1 Oid を RSSv2 Oid に変換します (必要な場合)。 VPort 拡散が scale になります。 ミニポートドライバーは、2つの新しい Oid をサポートし、次のように RSSv1 OID_GEN_RECEIVE_SCALE_PARAMETERS OID の動作を変更する必要があります。

- [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)は、RSS パラメーターの設定ではなく、RSSv2 のクエリ要求に対してのみ使用されます。
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)は、キューの数、無効化の数、RSS 有効化/、ハッシュキーの更新など、スケーリングエンティティのパラメーターを構成するために使用されるクエリとセット OID です。
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)は、間接テーブルエントリの変更を実行するために使用されるメソッド OID です。

## <a name="handling-rssv2-oids"></a>RSSv2 Oid の処理

[OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)は、指定されたスケーリングエンティティの現在の RSS パラメーターに対してのみクエリを実行するために使用されます。 RSSv1 では、この OID を使用してパラメーターを設定します。 RSSv2 対応ミニポートドライバーの場合、NDIS はドライバーに対してこの役割変換を自動的に実行し、次の2つの Oid を発行してパラメーターを設定します。

[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)は通常の oid で、Oid が RSSv1 で処理された OID_GEN_RECEIVE_SCALE_PARAMETERS と同じように処理されます。 この OID は、NDIS 6.80 より前では、NDIS ウェイトウェイトフィルタードライバー (LWFs) には表示されません。

ただし[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)は、NDIS_STATUS_PENDING を返すことができない[同期 OID](synchronous-oid-request-interface-in-ndis-6-80.md)です。 Oid を生成したプロセッサコンテキストで、この OID を実行して完了する必要があります。 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 と同様に、NDIS 6.80 より前の NDIS LWFs にも表示されません。 NDIS 6.80 以降の LWFs では、この OID の遅延または別のプロセッサへの移動は許可されていません。 このペイロードには単純な "move ITE" アクションの配列が含まれています。各アクションには、スケーリングエンティティの単一の ITE を別のターゲット CPU に移動するためのコマンドが含まれています。 配列の要素は、さまざまなスケーリングエンティティ (VPorts) を参照できます。

各種類の NDIS ドライバー、ミニポート、フィルター、およびプロトコルには、同期 OID 要求インターフェイスをサポートするためのエントリポイントがあります。

| NDIS ドライバーの種類 | 同期 OID ハンドラー | 同期 Oid を生成する関数 |
| --- | --- | --- |
| ミニ | [*MiniportSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-miniport_synchronous_oid_request) | 該当なし |
| フィルター | <ul><li>[*FilterSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request)</li><li>[*FilterSynchronousOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request_complete)</li></ul> | [**NdisFSynchronousOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsynchronousoidrequest) |
| プロトコル | 該当なし | [**NdisSynchronousOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissynchronousoidrequest) |

## <a name="rss-state-transitions-ite-updates-and-primarydefault-processors"></a>RSS 状態遷移、ITE 更新、およびプライマリ/既定のプロセッサ

### <a name="steering-parameters"></a>ステアリングパラメーター

RSSv2 では、RSS の状態 (有効または無効) に応じて、さまざまなパラメーターを使用して、適切な CPU へのトラフィックを調整します。 RSS を無効にすると、プライマリプロセッサのみがトラフィックを転送するために使用されます。 RSS を有効にすると、既定のプロセッサとすべてのの両方がトラフィックを転送するために使用されます。 これらの*ステアリングパラメーター*は、次の表に示すように、"アクティブ" または "非アクティブ" として labele です。

| ステアリングパラメーター | RSS の無効化 | RSS の有効化 |
| --- | --- | --- |
| プライマリプロセッサ | Active | Inactive |
| 既定のプロセッサ | Inactive | Active |
| ITE [0.. N] | Inactive | Active |

ステアリングパラメーターが*アクティブな*状態にある場合は、トラフィックを送信します。 パラメーターを*非アクティブ*にする RSS 状態遷移の時点では、逆方向の切り替えによってパラメーターが再びアクティブ化されるまで、ミニポートドライバーでパラメーターへの変更を追跡する必要があります。 つまり、ミニポートドライバーは、既定のプロセッサと間接テーブルのエントリに対するすべての更新を追跡する必要がありますが、そのスケーリングエンティティでは RSS は無効になっています。 RSS を有効にすると、既定のプロセッサテーブルと間接間接テーブルの現在の追跡状態が有効になります。

たとえば、ソフトウェア vRSS が既に有効になっている場合のシナリオを考えてみます。 この場合、間接テーブルは、上位層プロトコルに既に存在し、上位層のソフトウェア拡散コードによって積極的に使用されます。 ハードウェア RSS の有効化中に、すべてのエントリがプライマリプロセッサを指している場合は、間接テーブルエントリの*移動*を行う更新がハードウェアによって発行され、ハードウェアによって実行される前に、プライマリプロセッサで短時間が発生する可能性があります。 ミニポートドライバーによって既定のプロセッサおよび ITE 情報が追跡されている場合は、上位層によって既に予想されている場所にトラフィックを転送できます。

ミニポートドライバーは、非アクティブなステアリングパラメーターに対するすべての更新を追跡する必要がありますが、RSS 状態の変更によってこれらのパラメーターが*アクティブ*になるまで、これらのパラメーターの検証を遅らせる必要があることに注意してください。 たとえば、ハードウェア RSS が無効になっている間にソフトウェアが拡散している場合は、上位層プロトコルで任意のプロセッサを使用できます (アダプターの RSS セットの外部を含む)。 上位層では、RSS 状態の移行の時点で、すべての*非アクティブ*なパラメーターが新しい rss 状態に対して有効であることを確認します。 ただし、ミニポートの dirver は、追跡されている*非アクティブ*なステアリングパラメーターが無効であることを検出した場合でも、パラメーターを検証し、RSS 状態の移行を失敗させる必要があります。

### <a name="initial-state-and-updates-to-steering-parameters"></a>最初の状態とステアリングパラメーターの更新

次の表では、作成後のスケーリングエンティティの初期状態 (たとえば、VPort の作成後) と、パラメーターを更新する方法について説明します。

| パラメーター | 説明 |
| --- | --- |
| プライマリプロセッサ | <ul><li>VPort の作成時に指定された**アフィニティ**プロセッサを使用して初期化されます。</li><li>**NDIS_RSS_SET_INDIRECTION_ENTRY_FLAG_PRIMARY_PROCESSOR**フラグが設定された[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID を使用して更新できます。</li><li>**NDIS_NIC_SWITCH_VPORT_PARAMS_PROCESSOR_AFFINITY_CHANGED**フラグが設定された[OID_NIC_SWITCH_VPORT_PARAMETERS](oid-nic-switch-vport-parameters.md) OID を使用して更新できます (これは既存のコマンドレットの互換性パスです)。</li><li>**NDIS_NIC_SWITCH_VPORT_PARAMS_PROCESSOR_AFFINITY_CHANGED**フラグを使用して[OID_NIC_SWITCH_VPORT_PARAMETERS](oid-nic-switch-vport-parameters.md) OID を使用して読み取ることができます (これは既存のコマンドレットの互換性パスです)。</li><li>プライマリプロセッサの初期化後の移動は、既定のプロセッサまたは間接テーブルの内容には影響しません。</li></ul> |
| 既定のプロセッサ | <ul><li>VPort の作成時に指定された**アフィニティ**プロセッサを使用して初期化されます。</li><li>**NDIS_RSS_SET_INDIRECTION_ENTRY_FLAG_DEFAULT_PROCESSOR**フラグが設定された[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID を使用して更新できます。</li></ul> |
| 間接テーブル | <ul><li>数値**Ofindirection Tableentries**が**1**に設定されています。</li><li>唯一のエントリは、VPort 作成時に指定された**アフィニティ**プロセッサを使用して初期化されます。</li><li>[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID を使用して更新できます。</li></ul> |

(OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES を使用した) プロセッサとプライマリ/既定のプロセッサに対する更新は、対応するエントリが現在指しているプロセッサから呼び出されます。 特定の VPort については、上の層によって、次のような状況で、プライマリ/既定のプロセッサを移動または設定するための OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES Oid がないことが保証されます。

1. [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)が進行中です。
2. VPort の削除シーケンスが開始された後。 たとえば、上位レイヤーは、移動する最後の OID が完了した後にのみ、set フィルター OID を発行します。

### <a name="rss-disablement"></a>RSS 無効化

RSS 無効化中に、上層のプロトコルは、すべての参加をプライマリプロセッサに示すか、OID を発行して RSS を無効にするか、または間接テーブルをそのままにして RSS を無効にするかを選択することができます。 どちらの場合も、受信トラフィックはプライマリプロセッサを対象とする必要があります。

RSSv2 は、最初に RSS を無効にすることなく、上層のプロトコルが VPort を削除できるようにする RSSv1 の要件を維持します。 上位レイヤーでは、VPort の受信フィルターをゼロに設定して、受信トラフィックが VPort を通過しないようにし、RSS を無効にせずに VPort の削除を続行することができます。 上位層は、VPort の削除中またはその後に OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES Oid が発行されないことを保証します。

RSS 無効化と VPort の両方の削除中に、以前のキューの移動によって存在する可能性がある保留中の内部操作をミニポートドライバーで処理する必要があります。

### <a name="rssv2-invariants"></a>RSSv2 インバリアント

上位層プロトコルを使うと、管理機能や ITE の移動を実行する前に、重要な不変条件に違反しないようにすることができます。 次に、例を示します。

1. キューの数を減らす前に、上位層によって、間接テーブルが、VPort の新しいキュー数よりも多くのプロセッサを参照しないようにします。
2. 上位レイヤーでは、現在構成されている VPort のキュー数に違反する間接テーブルの更新を要求することはできません。 ミニポートドライバーはこれを強制し、エラーを返します。
3. VMMQ アダプターの間接参照テーブルのエントリ数を変更する前に、上位層によって、間接テーブルの内容が2の累乗に正規化されます。

## <a name="related-links"></a>関連リンク

[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)

[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)

[NDIS 6.80 の同期 OID 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)
