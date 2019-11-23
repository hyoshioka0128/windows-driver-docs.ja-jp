---
title: OID_GEN_RECEIVE_HASH
description: クエリとして、NDIS およびそれ以降のドライバーは、OID_GEN_RECEIVE_HASH OID を使用して、ミニポートアダプターの現在の受信ハッシュ計算の設定を取得します。
ms.assetid: be120dab-c98d-418f-8777-e2fb37b774a1
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_RECEIVE_HASH
ms.localizationpriority: medium
ms.openlocfilehash: c2d5d3c6fc63a37d3fcd552855d81e243e392158
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840473"
---
# <a name="oid_gen_receive_hash"></a>OID\_GEN\_RECEIVE\_HASH


クエリとして、NDIS およびそれ以降のドライバーは、\_ハッシュ OID を受け取る OID\_GEN\_使用して、ミニポートアダプターの現在の受信ハッシュ計算の設定を取得します。 NDIS は、現在の受信ハッシュ設定を含む[**ndis\_receive\_HASH\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)構造体を返します。

セットとして、NDIS およびそれ以降のドライバーは、\_ハッシュ OID を受信\_OID\_GEN を使用して、ミニポートアダプターでの受信ハッシュ計算を構成します。 ミニポートドライバーは、NDIS\_RECEIVE\_HASH\_PARAMETERS 構造体を受け取ります。

<a name="remarks"></a>注釈
-------

NDIS ミニポートドライバーの場合、クエリは要求されません。

この OID セットのサポートは、ミニポートドライバー (RSS をサポートするものを含む) では省略可能です。

後のドライバーでは、OID\_GEN\_使用して\_ハッシュ OID を受け取ることができます。これにより、RSS を有効にしなくても、受信したフレームでハッシュ計算を有効化および構成できます。

**注**  プロトコルドライバーでは、RSS を有効にする前に、受信ハッシュ計算を無効にする必要があります。 RSS が有効になっている場合、受信ハッシュ計算を有効にする前に、プロトコルドライバーが RSS を無効にします。 ミニポートドライバーは、 **NDIS\_状態\_無効\_oid**または NDIS\_の状態を使用して要求を失敗させる[必要があり](oid-gen-receive-scale-parameters.md)ます。この\_サポートされ**ていません**。\_\_\_\_\_

 

[**NDIS\_\_ハッシュ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)構造体のメンバーを受け取ると、秘密キーが追加**さ  ます**。

 

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
<td><p>NDIS 6.0 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_\_ハッシュ\_パラメーターを受け取る**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_hash_parameters)

 

 




