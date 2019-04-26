---
title: Receive Side Scaling Version 2 (RSSv2)
description: このトピックでは、受信側のスケーリングのバージョン 2 (RSSv2) を説明します。
ms.assetid: 192CAA41-0D17-4C06-8F13-68EA7C26D023
keywords: 受信側のスケーリングのバージョン 2、RSSv2、受信側のスケーリングのバージョン 2 WDK、RSSv2 ネットワーク ドライバー
ms.date: 10/12/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7dad30280a68c572c982e119b16bbce0b8293d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353211"
---
# <a name="receive-side-scaling-version-2-rssv2"></a>Receive Side Scaling Version 2 (RSSv2)

[!include[RSSv2 Beta Prerelease](../rssv2-beta-prerelease.md)]

[Receive Side Scaling](ndis-receive-side-scaling2.md)マルチプロセッサ システムのネットワーク データの処理に関連するシステムのパフォーマンスが向上します。 NDIS 6.80 以降では、RSS バージョン 2 (RSSv2) を提供する動的、VPort あたり分散させることでキューの RSS を拡張するものをサポートします。

## <a name="overview"></a>概要

RSSv2 は、RSSv1 と比較して、CPU 負荷の測定と間接指定テーブルを更新するまでの時間が短縮されます。 高トラフィックの状況時に速度の低下を回避できます。 これを実現する RSSv2 は IRQL でそのアクションを実行、要求を処理のプロセッサ コンテキスト = DISPATCH_LEVEL とを現在のプロセッサを指す間接指定テーブル エントリのサブセットについてだけ動作します。 つまり RSSv2 が動的に分散させることは、RSSv1 よりもはるかに使えるレスポンシブ複数のプロセッサにキューを受信します。

2 つの Oid [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)と[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)、適切な RSS 機能とコントロールを設定する、ミニポート ドライバー RSSv2 に導入されました。間接指定は、それぞれ表。 にします。 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 は正規の OID、OID_GEN_RSS_SET_INDIRECTION_ENTRIES は同期の OID を NDIS_STATUS_PENDING を返すことはできません。 これらの Oid の詳細については、その個々 のリファレンス ページを参照してください。 同期の Oid の詳細については、次を参照してください。 [NDIS 6.80 で同期 OID 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)します。

## <a name="rssv2-terminology"></a>RSSv2 用語集

このトピックでは、次の用語を使用します。

| 項目 | 定義 |
| --- | --- |
| RSSv1 | 第 1 世代は受信側のスケーリング メカニズムです。 使用して[OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)します。 |
| RSSv2 | 第 2 世代は受信側のスケーリング メカニズムは、Windows 10、バージョン 1803 でサポートされているし、後で、このトピックで説明です。 |
| エンティティのスケーリング| ミニポート アダプター自体ネイティブ RSS モード、または、VPort RSSv2 モードにします。 |
| ITE | スケーリングの特定のエンティティの間接指定テーブル エントリ (項目)。 Ite 用 VPort ごとの合計数を超えることはできません**NumberOfIndirectionTableEntriesPerNonDefaultPFVPort**または**NumberOfIndirectionTableEntriesForDefaultVPort** VMQ モードまたはネイティブ RSS に 128大文字にします。 **NumberOfIndirectionTableEntriesPerNonDefaultPFVPort**と**NumberOfIndirectionTableEntriesForDefaultVPort**のメンバーである、 [NDIS_NIC_SWITCH_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff566583)構造体。 |
| スケーリング モード | 実行時にその ite 用の処理方法を制御する VPort あたり vmswitch ポリシー。 これには、静的 (負荷の変化により ITE 移動がありません) または動的 (拡張および現在のトラフィックの負荷に応じて結合) を指定できます。 |
| キュー | 基になるハードウェア オブジェクト (キュー)、項目をバックアップします。 構成キューは、ハードウェアと間接指定テーブルによって、ite 用の複数をバックアップする可能性があります。 既定のキューで使用される 1 つ以上のキューの合計数は、通常、管理者によって設定された構成済みの制限を超えることはできません。 |
| 既定のプロセッサ | ハッシュを計算できませんパケットを受信するプロセッサ。 各 VPort では、既定のプロセッサを搭載します。
| プライマリのプロセッサ | として指定したプロセッサ、 **ProcessorAffinity**のメンバー、 [NDIS_NIC_SWITCH_VPORT_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/hh451597) VPort の作成中に構造体。 このプロセッサは、実行時に更新して、VMQ トラフィックの誘導先を指定します。 |
| ソースの CPU | 項目が現在マップされているプロセッサ。 |
| ターゲット CPU | 項目が再マップされる (RSSv2 を使用して) プロセッサ。 |
| アクターの CPU | 要求が行われる中でどの RSSv2 プロセッサ。 |

## <a name="advertising-rssv2-capability-in-a-miniport-driver"></a>ミニポート ドライバーで RSSv2 機能を提供

ミニポート ドライバーを設定して RSSv2 サポートを提供する、 **CapabilitiesFlags**のメンバー、 [NDIS_RECEIVE_SCALE_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff567220)構造体、 *NDIS_RSS_CAPS_SUPPORTS_INDEPENDENT_ENTRY_MOVE*フラグ。 この機能は RSSv2 の CPU の負荷分散と共に機能を有効にするために必要、 *NDIS_RECEIVE_FILTER_DYNAMIC_PROCESSOR_AFFINITY_CHANGE_SUPPORTED* RSSv1 動的既定以外の拡張 (の分散を可能にするフラグVMQs)。

> [!NOTE]
> 上位層プロトコルでは、RSSv2 ミニポート ドライバーの既定 VPort のプライマリのプロセッサを移動できることを前提としています。

ミニポート アダプターが RSSv2 機能をアドバタイズしていない場合場合でも、これらの拡張が動的に分散させることを実行する要求された静的な展開モードで VMQ が有効なすべての拡張を維持します。 RSS のパラメーターの構成の RSSv1 OID [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)、静的な展開モード中のこれらの拡張のために使用します。

ミニポート ドライバーのみ、-RSSv1 または RSSv2 のいずれか、1 つの RSS 制御メカニズムを実装する必要があります。 場合は、ドライバーは RSSv2 サポートをアドバタイズ RSSv2 Oid に構成する VPort ごとの展開に必要であれば NDIS に RSSv1 Oid が変換されます。 ミニポート ドライバーは、2 つの Oid が新たにサポートされ、RSSv1 OID_GEN_RECEIVE_SCALE_PARAMETERS OID の動作を次のように変更する必要があります。

- [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md) RSSv2 でクエリの要求に対してのみ、RSS パラメーターを設定しないに使用されます。
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)はクエリであり、ite 用、RSS の有効化/無効化の数のキューの数などのスケーリングのエンティティのパラメーターを構成するために使用される設定の OID とキーの更新をハッシュします。
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)メソッド OID 間接指定テーブル エントリの変更の実行に使用します。

## <a name="handling-rssv2-oids"></a>RSSv2 Oid の処理

[OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)は、特定のスケーリングのエンティティの現在の RSS パラメーターをクエリにのみ使用します。 RSSv1 はこの OID を使用してパラメーターを設定します。 RSSv2 対応のミニポート ドライバーでは、NDIS は自動的にドライバーをこのロールの変換を実行し、代わりにパラメーターを設定する次の 2 つの Oid を発行します。

[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)正規の OID は、RSSv1 で OID_GEN_RECEIVE_SCALE_PARAMETERS OID が処理済みとして同じ処理されます。 この OID では、NDIS 6.80 より前の NDIS 軽量フィルター ドライバー (LWFs) に表示されません。

[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)、ただしは、[同期 OID](synchronous-oid-request-interface-in-ndis-6-80.md) NDIS_STATUS_PENDING を返すことはできません。 この OID は実行され、OID の発生元プロセッサ コンテキスト内に完了する必要があります。 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 なども表示されていない NDIS LWFs NDIS 6.80 より前にします。 以降では、NDIS 6.80 LWFs はこの OID を遅延または別のプロセッサに移動は許可されていません。 そのペイロードには、スケーリングのエンティティの 1 つの項目を別のターゲット CPU に移動するためのコマンドを含む単純な「項目を移動する」のアクションでは、配列が含まれています。 配列の要素には、異なるスケーリング エンティティ (拡張) を参照できます。

NDIS ドライバー、ミニポート、フィルター、およびプロトコルの種類ごとには、同期 OID 要求インターフェイスをサポートするエントリ ポイントがあります。

| NDIS ドライバーの種類 | 同期の OID 負います | 同期の Oid を発信関数 |
| --- | --- | --- |
| ミニポート | [*MiniportSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-miniport_synchronous_oid_request) | N/A |
| フィルター | <ul><li>[*FilterSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-filter_synchronous_oid_request)</li><li>[*FilterSynchronousOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-filter_synchronous_oid_request_complete)</li></ul> | [**NdisFSynchronousOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsynchronousoidrequest) |
| プロトコル | N/A | [**NdisSynchronousOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissynchronousoidrequest) |

## <a name="rss-state-transitions-ite-updates-and-primarydefault-processors"></a>RSS は状態遷移、項目の更新プログラム、およびプライマリ/既定のプロセッサ

### <a name="steering-parameters"></a>ハンドルのパラメーター

RSSv2 でさまざまなパラメーターは、RSS の状態 (有効または無効になっている) に応じて、適切な CPU へのトラフィックを進めるために使用されます。 RSS を無効にすると、トラフィックを転送するため、プライマリのプロセッサのみが使用されます。 RSS を有効にすると、トラフィックを転送するため、既定のプロセッサとすべて ite 用の両方を使用します。 これら*ハンドル パラメーター* "active"または「非アクティブ」として labele は、次の表にまとめます。

| ハンドルのパラメーター | RSS を無効になっています | RSS を有効になっています。 |
| --- | --- | --- |
| プライマリのプロセッサ | Active | Inactive |
| 既定のプロセッサ | Inactive | Active |
| 項目 [0..N] | Inactive | Active |

ハンドル パラメーターの場合、 *active*状態では、これは、トラフィックを送信します。 RSS の時点から状態パラメーターは、遷移*非アクティブな*、ミニポート ドライバーは、逆遷移アクティブ化してもう一度までに、パラメーターの変更を追跡する必要があります。 これは、ミニポート ドライバーがそのスケーリングのエンティティの RSS を無効にして、既定のプロセッサと間接指定テーブル エントリをすべての更新プログラムを追跡する必要があることを意味します。 RSS が有効にすると、既定のプロセッサと間接指定テーブルの現在の追跡対象の状態が反映する必要があります。

たとえば、ソフトウェア vRSS が既に有効にするとシナリオを検討します。 この場合は、間接指定テーブルは既に上層のプロトコルに存在して、上位層のソフトウェアのコードを分散させることで使用中です。 かどうか、ハードウェア RSS の有効化中にすべてのエントリは開始を更新する前に、プライマリのプロセッサを指す*移動*間接指定テーブルのエントリに発行され、ハードウェアで実行される、プライマリのプロセッサが発生する可能性があります、短いが詰まっています。 ミニポート ドライバーには、既定のプロセッサと項目の情報を追跡が場合に、上位のレイヤーで想定される既ににトラフィックを転送します。

注ことミニポート ドライバーでは、非アクティブなハンドル パラメーターにすべての更新プログラムを追跡する必要があります、中がこれらのパラメーターの検証に達するまで遅らせます RSS 状態は、これらのパラメーターを実行する試行を変更*active*します。 たとえば、RSS が無効になっているハードウェアの中に分散させること、ソフトウェアの場合上位層プロトコルことができますを使用して、いずれかのプロセッサ (外部アダプターの RSS のセットを含む) の展開のため。 上位の層はいることを確認、状態遷移を RSS の時点ですべて*非アクティブな*パラメーターは、新しい RSS 状態に対して無効です。 ただし、ミニポート dirver する必要がありますもパラメーターを検証し、追跡されていることが検出された場合は、RSS の状態遷移を失敗*非アクティブな*ハンドル パラメーターが無効です。

### <a name="initial-state-and-updates-to-steering-parameters"></a>初期状態とステアリング パラメーターへの更新

次の表には、パラメーターを更新する方法と (たとえば、VPort の作成) 後の作成後に、スケーリングのエンティティの初期状態がについて説明します。

| パラメーター | 説明 |
| --- | --- |
| プライマリのプロセッサ | <ul><li>初期化された、**アフィニティ**プロセッサ VPort の作成時に指定します。</li><li>使用して更新できる、 [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)と OID、 **NDIS_RSS_SET_INDIRECTION_ENTRY_FLAG_PRIMARY_PROCESSOR**フラグを設定します。</li><li>使用して更新できる、 [OID_NIC_SWITCH_VPORT_PARAMETERS](oid-nic-switch-vport-parameters.md)と OID、 **NDIS_NIC_SWITCH_VPORT_PARAMS_PROCESSOR_AFFINITY_CHANGED**フラグを設定 (これは、既存のコマンドレットの互換性のパス).</li><li>使用して読み取ることができます、 [OID_NIC_SWITCH_VPORT_PARAMETERS](oid-nic-switch-vport-parameters.md)と OID、 **NDIS_NIC_SWITCH_VPORT_PARAMS_PROCESSOR_AFFINITY_CHANGED**フラグ (これは既存のコマンドレットの互換性のパスです)。</li><li>プライマリのプロセッサの初期化後の移動は、既定のプロセッサまたは間接参照テーブルの内容には影響しません。</li></ul> |
| 既定のプロセッサ | <ul><li>初期化された、**アフィニティ**プロセッサ VPort の作成時に指定します。</li><li>使用して更新できる、 [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)と OID、 **NDIS_RSS_SET_INDIRECTION_ENTRY_FLAG_DEFAULT_PROCESSOR**フラグを設定します。</li></ul> |
| 間接指定テーブル | <ul><li>**NumberOfIndirectionTableEntries**に設定されている**1**します。</li><li>唯一のエントリが初期化されて、**アフィニティ**プロセッサ VPort の作成時に指定します。</li><li>使用して更新できる、 [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID。</li></ul> |

Ite 用と (OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES を使用して) プライマリ/既定のプロセッサの更新プログラムは、対応するエントリが現在指しているプロセッサから呼び出されます。 特定の VPort の上位レイヤーにより ite 用またはこのような場合、プライマリ/既定のプロセッサが発行されますセットに移動するには、ない OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES Oid:

1. 中に[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)が進行中です。
2. 後、VPort の削除のシーケンスが開始されます。 たとえば、上位レイヤーは、ite 用に移動する最後の OID が完了した後にのみ、OID のフィルターの設定を発行します。

### <a name="rss-disablement"></a>RSS の無効化

RSS の無効化中にプライマリのプロセッサをすべての ite 用をポイントし、RSS を無効にする OID を発行するか、上層のプロトコルを選択または間接参照テーブルとしてのままにすることもできますが、RSS を無効にするには、します。 いずれの場合も、受信トラフィック、プライマリのプロセッサを対象とする必要があります。

RSSv2 は、RSSv1 上層のプロトコルを無効にする最初の RSS を使わないの VPort の削除を許可する要件を維持します。 上位のレイヤーは、ので、VPort を通じていない受信トラフィックのフローを確保する 0 に VPort に受信フィルターを設定し、RSS を無効にしなくても VPort の削除を実行します。 ある OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES Oid は発行されません中または VPort の削除後に上位のレイヤーが保証されます。

RSS の無効化、およびその VPort の削除、ミニポート ドライバーが前のキューの移動のために存在する内部操作保留中の注意が必要です。

### <a name="rssv2-invariants"></a>RSSv2 不変性

上層のプロトコルは、重要な不変性が管理機能を実行する前に違反していないまたは項目に移動できるようにします。 例:

1. キューの数を小さく前に、上位層により、間接指定テーブルを VPort の新しいキューの数よりもより多くのプロセッサが含まれていないこと。
2. 上位のレイヤーを VPort のキューの現在構成されている数に違反する間接参照テーブルの更新を要求しないでください。 ミニポート ドライバーは、これが適用され、エラーを返す必要があります。
3. VMMQ によって制限されているアダプターの間接指定テーブル エントリの数を変更する前に上位のレイヤーにより、間接指定テーブルの内容は、2 の累乗に正規化されます。

## <a name="related-links"></a>関連リンク

[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)

[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)

[NDIS 6.80 で同期の OID 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)
