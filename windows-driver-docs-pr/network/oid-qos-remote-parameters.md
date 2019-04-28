---
title: OID_QOS_REMOTE_PARAMETERS
description: 上にある、ドライバーは、リモート ピアの NDIS サービスの品質 (QoS) パラメーターを取得する OID_QOS_REMOTE_PARAMETERS のオブジェクト識別子 (OID) のクエリ要求を発行します。
ms.assetid: F9DA87FF-577F-4E06-929B-4AD65105B2F0
ms.date: 08/08/2017
keywords: -OID_QOS_REMOTE_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b19d4b026d2c9acd98f25dc368876bb6aef8cda3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364106"
---
# <a name="oidqosremoteparameters"></a>OID\_QOS\_リモート\_パラメーター


上にある、ドライバーの OID オブジェクト識別子 (OID) のクエリ要求を発行する\_QOS\_リモート\_リモート ピアの NDIS サービスの品質 (QoS) パラメーターを取得するパラメーター。 ミニポート ドライバーでは、これらリモート QoS パラメーターを使用して、その運用上の NDIS QoS パラメーターを解決します。 ドライバーは、QoS パケットの転送を実行するために、オペレーションのパラメーターを使用して、ネットワーク アダプターを構成します。

OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体。

**注**  この OID クエリ要求は、IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスをサポートするミニポート ドライバーでのみ有効です。

 

<a name="remarks"></a>注釈
-------

NDIS が OID の OID 要求を処理するときに\_QOS\_リモート\_パラメーター、前のキャッシュしたリモートの NDIS QoS パラメーターを返すことが正常に[ **NDIS\_ステータス\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)ミニポート ドライバーで発行された状態を示す値。 ドライバーは、リモートの NDIS QoS パラメーターの初期セットをレポートするには、この状態表示を発行します。 ドライバーは、リモートの NDIS QoS パラメーターを変更するたびにもこの状態を示す値を発行します。

NDIS を返します、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)次のように初期化された構造体。

-   ミニポート ドライバーが既に発行されている場合、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態示す値、NDIS キャッシュ、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)データと OID クエリのこのデータを要求の OID を返します\_QOS\_。リモート\_パラメーター。

-   ミニポート ドライバーを発行していない場合、 [ **NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状態の表示NDIS を返します、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)すべてのメンバーを含む構造体 (例外として、**ヘッダー**メンバー) は、0 に設定します。

リモートの NDIS QoS パラメーターの詳細については、次を参照してください。 [NDIS QoS パラメーターの概要](https://msdn.microsoft.com/library/windows/hardware/hh440130)します。

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
[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_QOS\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)

[**NDIS\_状態\_QOS\_運用\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439810)

[**NDIS\_状態\_QOS\_リモート\_パラメーター\_変更**](https://msdn.microsoft.com/library/windows/hardware/hh439812)

[OID\_QOS\_パラメーター](oid-qos-parameters.md)

 

 




