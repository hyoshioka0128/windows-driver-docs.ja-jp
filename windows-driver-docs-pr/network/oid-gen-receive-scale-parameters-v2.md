---
title: OID_GEN_RECEIVE_SCALE_PARAMETERS_V2
description: このトピックでは、について説明し OID_GEN_RECEIVE_SCALE_PARAMETERS_V2
ms.assetid: 3897A898-2B00-45DF-AC05-7EC719EB7353
keywords: OID_GEN_RECEIVE_SCALE_PARAMETERS_V2、OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 RSSv2
ms.date: 10/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 311829906f8ce32b51fd76e3cbd2681454db6e4c
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235349"
---
# <a name="oid_gen_receive_scale_parameters_v2"></a>OID_GEN_RECEIVE_SCALE_PARAMETERS_V2

[!include[RSSv2 Beta Prerelease](../includes/rssv2-beta-prerelease.md)]

OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 OID は、スケーリングエンティティに対して間接テーブル以外の実行時パラメーターを設定するために[RSSv2](receive-side-scaling-version-2-rssv2-.md)対応ミニポートドライバーに送信されます。 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 は、 [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md) OID を RSSv1 から置き換えます。 ndis 6.80 の前に、Ndis ライトウェイトフィルター (LWFs) には表示されません。 この OID は通常の OID であり、クエリまたは設定要求として発行できます。 これは、IRQL = = PASSIVE_LEVEL で発行されます。 *NDIS_OID_REQUEST_FLAGS_VPORT_ID_VALID*フラグが NIC スイッチの作成時に設定されている場合、特定の vport をターゲットにすることができます。 それ以外の場合は、ネイティブの RSS ケースで物理 NIC を対象とします。

NDIS およびそれ以降のドライバーは、クエリとして OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 を使用して、NIC の RSS パラメーターを照会できます。 NDIS は、現在の RSS パラメーターを定義する[NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)構造体を返します。

セットとして、この OID の目的は次のアクションを実行することです。

- スケーリングエンティティ (ネイティブ RSS モードの場合はミニポートアダプター、VMQ モードでは VPort) を最初に構成します。
- RSS を有効または無効にします。
- RSS モードでは、スケールエンティティのハッシュキー、ハッシュの種類とハッシュ関数、キューの数、間接テーブルエントリの数など、タイミングが重要ではない管理機能を実行します。

## <a name="remarks"></a>解説

RSS の有効化と RSS パラメーターの設定は、1回の手順で実行できます。 この OID を使用して、上位レイヤーで RSS を有効にした後、スケーリングエンティティの初期状態は次のようになります。

- プライマリプロセッサが*非アクティブ*になります。
- 既定のプロセッサが*アクティブ*になります。
- すべてのが*アクティブ*になります。
- ミニポートドライバーは、RSS ハッシュの計算を開始し、対応するすべてのパケットの OOB を設定し、間接テーブルエントリまたは既定のプロセッサパラメーターで指定されたプロセッサにパケットを転送します。

RSS を有効にすると、 [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID が異なるプロセッサに移動するようになります。 RSSv2 では、 **Defaultqueue**と**primaryprocessor**も OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES を使用して別のプロセッサに移動されます。

RSS を無効にするプロセスでは、この OID を呼び出して RSS を無効にする前に、上位層がすべてのがプライマリプロセッサをポイントします。 この時点以降、受信トラフィックはプライマリプロセッサを対象とする必要があります。 ただし、ミニポートドライバーでは、VPort を削除する前に RSS を無効にする必要はありません。 上位レイヤーでは、VPort の受信フィルターをゼロに設定して、受信トラフィックが VPort を通過しないようにしてから、RSS を無効にせずに VPort の削除に進みます。

上位層は、管理機能を実行する前に、重要な不変条件に違反しないようにします。 たとえば、次のように入力します。

- キューの数を変更する前に、上位層では、間接テーブルが、VPort 用に構成されているよりも多くのプロセッサを参照していないことを確認します。
VMMQ アダプターの間接参照テーブルのエントリ数を変更する前に、上位層によって、間接テーブルの内容が2の累乗に正規化されます。

### <a name="error-conditions-and-status-codes"></a>エラー状態と状態コード

この OID は、エラーが発生したときに次の状態コードを返します。

| status code | エラー状態 |
| --- | --- |
| NDIS_STATUS_INVALID_LENGTH | OID の形式が正しくありません。 |
| NDIS_STATUS_NO_QUEUES | RSS が有効になっているときにキューの数が変更されていますが、現在の間接テーブルでは、新しいキューの数より多くのプロセッサが参照されています。 |
| NDIS_STATUS_INVALID_DATA | <ul><li>間接テーブルのサイズが縮小されていますが、2回の繰り返しパターンが含まれていません。</li><li>RSS 状態遷移 ( *on*または*off*) 中に、*アクティブ*になるステアリングパラメーターのプロセッサは、アダプターの RSS プロセッサセットに属していません。 *非アクティブ*なステアリングパラメーターはプロセッサへの書き込みを追跡するだけであり、強制されないことに注意してください。 適用は、パラメーターが*アクティブ*になったときに RSS 状態の移行中に行われます。</li></ul> |
| NDIS_STATUS_INVALID_PARAMETER | ヘッダーまたは OID 自体にある他のフィールドには、無効な値が含まれています。 |

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

- [Receive Side Scaling Version 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)

