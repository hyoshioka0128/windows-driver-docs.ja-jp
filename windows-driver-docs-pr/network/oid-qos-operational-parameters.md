---
title: OID_QOS_OPERATIONAL_PARAMETERS
description: 上にある、ドライバーは、ネットワーク アダプターの現在の NDIS サービスの品質 (QoS) 運用パラメーターを取得する OID_QOS_OPERATIONAL_PARAMETERS のオブジェクト識別子 (OID) のクエリ要求を発行します。
ms.assetid: 546EE7C6-BCED-4FF9-9B87-A36199B1B31C
ms.date: 08/08/2017
keywords: -OID_QOS_OPERATIONAL_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 07caef0308875b398f3ee917751fa418057809f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572967"
---
# <a name="oidqosoperationalparameters"></a>OID\_QOS\_OPERATIONAL\_パラメーター


上にある、ドライバーの OID オブジェクト識別子 (OID) のクエリ要求を発行する\_QOS\_OPERATIONAL\_ネットワーク アダプターの現在の NDIS サービスの品質 (QoS) 運用パラメーターを取得するパラメーター。 ミニポート ドライバーは、QoS パケットの転送を実行するために、運用上の NDIS QoS パラメーターを使用して、ネットワーク アダプターを構成します。

OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体。

**注**  IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスをサポートするミニポート ドライバーの NDIS がこの OID クエリ要求を処理します。

 

<a name="remarks"></a>コメント
-------

NDIS が OID の OID のクエリ要求を処理するときに\_QOS\_運用\_パラメーター、前のキャッシュした運用面の NDIS QoS パラメーターを返すことが正常に[ **NDIS\_ステータス\_QOS\_運用\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)ミニポート ドライバーで発行された状態を示す値。 ドライバーは、運用上の NDIS QoS パラメーターの初期セットをレポートするには、この状態表示を発行します。 ドライバーは、運用上の NDIS QoS パラメーターを変更するたびにもこの状態を示す値を発行します。

NDIS を返します、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)次のように初期化された構造体。

-   ミニポート ドライバーが既に発行されている場合、 [ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状態示す値、NDIS キャッシュ、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)データと OID クエリのこのデータを要求の OID を返します\_QOS\_。OPERATIONAL\_パラメーター。

-   ミニポート ドライバーを発行していない場合、 [ **NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状態示す値、NDIS を返します、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)すべてのメンバーを含む構造体 (例外として、**ヘッダー**メンバー) を 0 に設定します。

運用上の NDIS QoS パラメーターの詳細については、次を参照してください。 [NDIS QoS パラメーターの概要](https://msdn.microsoft.com/library/windows/hardware/hh440130)します。

### <a name="return-status-codes"></a>リターン状態コード

NDIS は、次のステータス コードのいずれかを返します。

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
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポート ドライバーでは、NDIS QoS インターフェイスはサポートしません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451640" data-raw-source="[&lt;strong&gt;NDIS_QOS_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451640)"><strong>NDIS_QOS_PARAMETERS</strong></a>)。 NDIS セット、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
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
[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_QOS\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)

[**NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)

[**NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)

[OID\_QOS\_パラメーター](oid-qos-parameters.md)

 

 




