---
title: OID_GEN_HD_SPLIT_CURRENT_CONFIG
description: クエリとして、それ以降のドライバーや管理ユーティリティでは、OID_GEN_HD_SPLIT_CURRENT_CONFIG OID を使用して、ミニポートアダプターの現在のヘッダーデータ分割構成を確認できます。
ms.assetid: fc363227-1040-45bc-8c76-2ac61606d777
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_HD_SPLIT_CURRENT_CONFIG ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: f9b0fac8398f0f6d05023b94b97e4c0cd0a88384
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843022"
---
# <a name="oid_gen_hd_split_current_config"></a>OID\_GEN\_HD\_分割\_現在の\_構成


クエリとして、それ以降のドライバーや管理ユーティリティでは、OID\_GEN\_HD\_分割\_現在の\_CONFIG OID を使用して、ミニポートアダプターの現在のヘッダーデータの分割構成を確認できます。 システム管理者は、WMI インターフェイスを使用して、この OID に関連付けられている GUID を使用できます。

<a name="remarks"></a>注釈
-------

NDIS は、ミニポートドライバーに代わってこの OID を処理します。 現在のヘッダーデータの分割構成情報は、ミニポートドライバーの初期化属性と[**ndis\_ステータス\_HD\_分割\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)の状態の表示に基づいて、ndis によって保持されます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、[**現在の\_構成構造\_分割される ndis\_HD\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)が含まれています。

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
<td><p>NDIS 6.1 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_HD\_分割\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_状態\_HD\_分割\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)

 

 




