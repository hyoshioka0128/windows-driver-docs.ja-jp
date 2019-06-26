---
title: OID_GEN_RECEIVE_SCALE_PARAMETERS_V2
description: このトピックでは、OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 をについて説明します
ms.assetid: 3897A898-2B00-45DF-AC05-7EC719EB7353
keywords: OID_GEN_RECEIVE_SCALE_PARAMETERS_V2, OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 RSSv2
ms.date: 10/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 474e9a10ca974ca2aae0d3a1d898a1501ff93940
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355129"
---
[!include[RSSv2 Beta Prerelease](../rssv2-beta-prerelease.md)]

# <a name="oidgenreceivescaleparametersv2"></a>OID_GEN_RECEIVE_SCALE_PARAMETERS_V2

OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 OID に送信される[RSSv2](receive-side-scaling-version-2-rssv2-.md)-対応のミニポート ドライバーにスケーリングのエンティティに対する、間接指定テーブル以外の実行時パラメーターを設定します。 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 置換、 [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md) RSSv1 から OID、NDIS 6.80 する前に NDIS 光重みフィルター (LWFs) に表示されません。 この OID 正規の OID は、クエリまたは一連の要求として発行することができます。 これが IRQL で発行される PASSIVE_LEVEL = =。 特定 VPort をターゲットにできるときに、 *NDIS_OID_REQUEST_FLAGS_VPORT_ID_VALID* NIC スイッチの作成にフラグを設定します。 それ以外の場合、ネイティブ RSS ケース内の物理 NIC を対象とします。

クエリでは、NDIS および上にあるドライバーを使用して OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 クエリ NIC の RSS パラメーター NDIS を返します、 [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2) RSS の現在のパラメーターを定義する構造体。

この OID の目的は、セットとして、次の操作を実行するは。

- 最初に、スケーリングのエンティティ (RSS のネイティブ モードでミニポート アダプターまたは VMQ モードでの VPort) を構成します。
- 有効または RSS を無効にします。
- RSS モードの場合は、ハッシュ キー、ハッシュの種類とハッシュ関数の数のキュー、またはスケーリングのエンティティの間接指定テーブル エントリの数を変更するなどのタイミングが重要な管理機能を実行します。

## <a name="remarks"></a>注釈

RSS および RSS のパラメーターの設定を有効にするは、1 つの手順で実行できます. 上位のレイヤーをこの OID を使用して RSS を有効にすた後、スケーリングのエンティティの初期状態のとおりです。

- プライマリのプロセッサが*非アクティブな*します。
- 既定のプロセッサが*active*します。
- なるすべての ite 用*active*します。
- ミニポート ドライバーでは、すべてのパケットに対応する OOB の設定と間接のテーブルのエントリまたは既定のプロセッサ パラメーターで指定されたプロセッサにパケットを送信する RSS ハッシュの計算を開始します。

RSS を有効にすると、上位のレイヤーの問題、 [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) ite 用を別のプロセッサに移動する OID。 RSSv2 で、 **DefaultQueue**と**PrimaryProcessor** OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES を使用して別のプロセッサにも移動されます。

RSS を無効にする過程で、上位レイヤーはポイントすべて ite 用プライマリ プロセッサに RSS を無効にするには、この OID を呼び出す前にします。 その後、受信トラフィック、プライマリのプロセッサを対象とする必要があります。 ただし、ミニポート ドライバーでは、VPort の削除する前に RSS の無効化は限りません。 上位のレイヤーはことができますので、受信トラフィックが経由で流れていない、VPort を確保ゼロに VPort の受信フィルターを設定し、RSS を無効にしなくても、VPort の削除を続行します。

上位のレイヤーは管理機能を実行する前に重要な不変性が違反していないことを確認します。 例:

- キューの数を変更する前に間接指定テーブルを VPort 用に構成されたより多くのプロセッサを参照していないこと、上位のレイヤーが保証されます。
VMMQ によって制限されているアダプターの間接指定テーブル エントリの数を変更する前に、2 の累乗に間接指定テーブルの内容を正規化した上位のレイヤーが保証されます。

### <a name="error-conditions-and-status-codes"></a>エラー状況と状態コード

この OID では、エラーが発生したときに、次のステータス コードが返されます。

| 状態コード | エラー状況 |
| --- | --- |
| NDIS_STATUS_INVALID_LENGTH | OID が正しくありません。 |
| NDIS_STATUS_NO_QUEUES | RSS が有効になっているが、現在の間接指定テーブルが新しいキューの数よりもより多くのプロセッサを参照するときは、キューの数を変更するは。 |
| NDIS_STATUS_INVALID_DATA | <ul><li>間接指定テーブルは、サイズが縮小されているが、2 のべき乗の繰り返しパターンを含まない。</li><li>RSS 中に状態遷移 (に*で*または*オフ*)、プロセッサになるハンドル パラメーターから*active*はアダプターの RSS プロセッサ セットに属していません。 なお*非アクティブな*ハンドル パラメーターは、プロセッサへの追跡の書き込みのみ、適用されていません。 パラメーターになったら、RSS 状態遷移中に強制は行われます*active*します。</li></ul> |
| NDIS_STATUS_INVALID_PARAMETER | ヘッダーまたは OID 自体では、他のフィールドには、無効な値が含まれます。 |

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

- [Receive Side Scaling バージョン 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)

