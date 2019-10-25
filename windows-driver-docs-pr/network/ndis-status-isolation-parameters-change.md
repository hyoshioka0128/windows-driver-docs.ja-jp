---
title: NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE
description: VM ネットワークアダプターのミニポートドライバーは、ネットワークアダプターのポートでルーティングドメインの構成が更新されるたびに、NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE ステータスを生成します。
ms.assetid: 4F3916B6-F52D-4B99-8F1C-A4A5BA9B307B
ms.date: 08/08/2017
keywords: -Windows Vista 以降の NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 3fc7b46042a1d66b2fa4af28095f0cf378bbc8ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844210"
---
# <a name="ndis_status_isolation_parameters_change"></a>NDIS\_ステータス\_分離\_パラメーター\_変更


VM ネットワークアダプターのミニポートドライバーは、ネットワークアダプターのポートでルーティングドメインの構成が更新されるたびに、 **\_の\_\_パラメーターの\_の NDIS**を生成し、変更の状態を示します。 これにより、TCP 層がトリガーされ、 [oid\_GEN\_分離\_パラメーター](oid-gen-isolation-parameters.md) oid が発行され、マルチテナント構成が再クエリされます。 この状態の表示には、ステータスバッファーがありません。

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
<td><p>NDIS 6.40 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_GEN\_分離\_パラメーター](oid-gen-isolation-parameters.md)

 

 




