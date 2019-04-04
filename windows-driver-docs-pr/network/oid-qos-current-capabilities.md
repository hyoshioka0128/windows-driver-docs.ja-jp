---
title: OID_QOS_CURRENT_CAPABILITIES
description: 上にある、ドライバーは、ネットワーク アダプターの現在有効になっている NDIS サービスの品質 (QoS) のハードウェア機能を取得する OID_QOS_CURRENT_CAPABILITIES のオブジェクト識別子 (OID) のクエリ要求を発行します。
ms.assetid: E9013EB2-5EDB-4BCB-BC1D-17345B85D1C4
ms.date: 08/08/2017
keywords: -OID_QOS_CURRENT_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d876cd65e16c950b0aa64742c94d686d542478b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569695"
---
# <a name="oidqoscurrentcapabilities"></a>OID\_QOS\_現在\_機能


上にある、ドライバーの OID オブジェクト識別子 (OID) のクエリ要求を発行する\_QOS\_現在\_ネットワーク アダプターの現在有効になっている NDIS サービスの品質 (QoS) のハードウェア機能を取得する機能。

OID のクエリ要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_QOS\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)構造体。

**注**  IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスをサポートするミニポート ドライバーの NDIS がこの OID クエリ要求を処理します。

 

<a name="remarks"></a>コメント
-------

ミニポート ドライバー、ネットワーク アダプターの現在有効になっている NDIS QoS ハードウェア機能を登録するときにその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数が呼び出されます。 ドライバーは、次の手順に従って、これらの機能を登録します。

1.  ドライバーの初期化、 [ **NDIS\_QOS\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451629) QoS ハードウェアの機能を有効になっているを含む構造体。

2.  ドライバーのセット、 **CurrentQosCapabilities**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体へのポインターを[ **NDIS\_QOS\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)構造体。

3.  ミニポート ドライバーを呼び出して、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数とセット、 *MiniportAttributes*パラメーターへのポインターを[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体。

**注**  NDIS が現在有効になっている NDIS QoS のハードウェア機能、ネットワーク アダプターにバインド中にプロトコルとフィルター ドライバーを関連するレポートまたはアタッチ操作していません。

 

NDIS QoS 機能を登録する方法の詳細については、[NDIS QoS 機能の登録](https://msdn.microsoft.com/library/windows/hardware/hh440188)を参照してください。

### <a name="return-status-codes"></a>リターン状態コード

OID の OID のクエリ要求を処理する NDIS\_QOS\_現在\_機能要求のミニポート ドライバー、および次のステータス コードの 1 つを返します。

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
<td><p>情報バッファーの長さが sizeof より小さい (<a href="https://msdn.microsoft.com/library/windows/hardware/hh451629" data-raw-source="[&lt;strong&gt;NDIS_QOS_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451629)"><strong>NDIS_QOS_CAPABILITIES</strong></a>)。 NDIS セット、<strong>データ。QUERY_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
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
[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

[**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_QOS\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451629)

 

 




