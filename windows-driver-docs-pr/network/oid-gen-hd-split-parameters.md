---
title: OID_GEN_HD_SPLIT_PARAMETERS
description: セットとして、NDIS およびそれ以降のドライバーまたはユーザーモードアプリケーションは OID_GEN_HD_SPLIT_PARAMETERS OID を使用して、ミニポートアダプターの現在のヘッダーデータ分割設定を設定します。
ms.assetid: 1b33c601-4302-4f63-8265-b75889b42d42
ms.date: 08/08/2017
keywords: -Windows Vista 以降のネットワークドライバーの OID_GEN_HD_SPLIT_PARAMETERS
ms.localizationpriority: medium
ms.openlocfilehash: a9d9387232d4ce872a64517758121a4691a46bf0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843019"
---
# <a name="oid_gen_hd_split_parameters"></a>OID\_GEN\_HD\_SPLIT\_パラメーターの分割


セットとして、NDIS およびそれ以降のドライバーまたはユーザーモードアプリケーションでは、OID\_GEN\_HD\_分割\_パラメーター OID を使用して、ミニポートアダプターの現在のヘッダーデータ分割設定を設定します。 ヘッダーデータ分割サービスが提供する NDIS 6.1 およびそれ以降のミニポートドライバーは、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

<a name="remarks"></a>注釈
-------

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_HD\_SPLIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)構造体が含まれています。

Ndis では、NDIS 5 の場合、OID\_GEN\_HD\_SPLIT\_PARAMETERS OID が設定されることがあります。*x*プロトコルドライバーは NDIS 6.1 ミニポートにバインドされます。 NDIS は、この OID をミニポートドライバーに渡す前に処理し、必要に応じて、ミニポートアダプターの **\*HeaderDataSplit**標準化されたキーワードを更新します。 ヘッダーデータの分割が無効になっている場合、NDIS はこの OID をミニポートアダプターに送信しません。

Ndis は、ヘッダーデータの分割が ndis\_HD\_\_SPLIT で有効になっている場合にのみ、この OID をミニポートドライバーに送信します。この場合、ミニポートの初期化時に、 [**ndis\_hd\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes) split\_の分割フラグが\_有効になります。\_\_

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


[**NDIS\_HD\_SPLIT\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)

[**NDIS\_HD\_SPLIT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)

[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




