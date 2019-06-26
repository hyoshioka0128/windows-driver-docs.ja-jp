---
title: OID_SWITCH_FEATURE_STATUS_QUERY
description: オブジェクト識別子 (OID) のメソッドが拡張可能スイッチに関する拡張機能からカスタム状態情報を取得する要求 OID_SWITCH_FEATURE_STATUS_QUERY の HYPER-V 拡張可能スイッチに関する問題のプロトコルのエッジ。
ms.assetid: 580EFBD0-7798-4C56-99C5-84EADB8F8E82
ms.date: 08/08/2017
keywords: -OID_SWITCH_FEATURE_STATUS_QUERY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 18af7aabc7d558b63db4ba53b22a78a8862ea3d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362878"
---
# <a name="oidswitchfeaturestatusquery"></a>OID\_スイッチ\_機能\_状態\_クエリ


HYPER-V 拡張可能スイッチのプロトコルのエッジの OID オブジェクト識別子 (OID) メソッド要求を発行する\_切り替える\_機能\_状態\_拡張機能からのカスタム状態情報を取得するクエリ、拡張可能スイッチ。 この情報と呼ばれる*機能の状態*情報。 この情報の形式は、独立系ソフトウェア ベンダー (ISV) によって定義されます。

この OID メソッド要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_スイッチ\_機能\_状態\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)機能の状態の種類のパラメーターを指定する構造体返される情報。

-   [ **NDIS\_切り替える\_機能\_状態\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom)拡張可能スイッチの機能の状態情報を含む構造体。

<a name="remarks"></a>注釈
-------

OID を処理する方法に関するガイドラインの OID 要求のセットの\_スイッチ\_機能\_状態\_クエリを参照してください[カスタム スイッチの機能の状態情報を管理する](https://docs.microsoft.com/windows-hardware/drivers/network/managing-custom-switch-feature-status-information)します。

### <a name="return-status-codes"></a>リターン状態コード

拡張機能は、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_スイッチ\_機能\_状態\_クエリ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが小さすぎる機能の状態情報を返すだけでなく<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_FEATURE_STATUS_CUSTOM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom)"> <strong>NDIS_SWITCH_FEATURE_STATUS_CUSTOM</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_FEATURE_STATUS_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)"> <strong>NDIS_SWITCH_FEATURE_STATUS_PARAMETERS</strong> </a>構造体。 拡張可能スイッチのセットの基になるミニポート edge、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_プロパティ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_switch_property_type)

[**NDIS\_スイッチ\_機能\_状態\_カスタム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_feature_status_custom)

[**NDIS\_スイッチ\_機能\_状態\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_feature_status_parameters)

 

 




