---
title: OID_GEN_RECEIVE_HASH
description: クエリとして NDIS および上にあるドライバーはミニポート アダプターの現在の受信ハッシュ計算の設定を取得するのに OID_GEN_RECEIVE_HASH OID を使用します。
ms.assetid: be120dab-c98d-418f-8777-e2fb37b774a1
ms.date: 08/08/2017
keywords: -OID_GEN_RECEIVE_HASH ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1f847bd4537a77cf6a72aa07a103f049fc40185b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353315"
---
# <a name="oidgenreceivehash"></a>OID\_GEN\_受信\_ハッシュ


クエリ、NDIS と関連付けたドライバーを使用、OID\_GEN\_受信\_ミニポート アダプターのハッシュの計算の設定を取得するには、現在の受信にハッシュの OID。 NDIS を返します、 [ **NDIS\_受信\_ハッシュ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)現在受信ハッシュの設定を含む構造体。

セットとして NDIS と関連付けたドライバー使用 OID\_GEN\_受信\_ハッシュ OID ミニポート アダプターで受信ハッシュ計算を構成します。 ミニポート ドライバーが受信、NDIS\_受信\_ハッシュ\_パラメーター構造体。

<a name="remarks"></a>注釈
-------

NDIS ミニポート ドライバーでは、クエリは要求されません。

この OID セットは、RSS をサポートするものも含め、ミニポート ドライバー オプションをサポートします。

上にある、ドライバーは OID を使用できる\_GEN\_受信\_ハッシュ OID を有効にし、ハッシュ計算を構成するのには、RSS を有効にしなくてもフレームを受信します。

**注**  プロトコル ドライバーを無効にする必要がありますが、RSS が有効にする前に、ハッシュ計算を受信します。 RSS が有効になっている場合、プロトコル ドライバー無効 RSS が有効にする前に、ハッシュ計算を受け取ります。 ミニポート ドライバーのセットの要求が失敗する**NDIS\_状態\_無効な\_OID**または**NDIS\_状態\_いない\_サポートされています。** 有効にする場合は、ハッシュ計算を受信[OID\_GEN\_受信\_スケール\_パラメーター](oid-gen-receive-scale-parameters.md)が現在有効です。

 

**注**  の後に、秘密キーを追加、 [ **NDIS\_受信\_ハッシュ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)メンバー構造体します。

 

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
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_受信\_ハッシュ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)

 

 




