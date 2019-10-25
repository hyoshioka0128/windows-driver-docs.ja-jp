---
title: NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG
description: ミニポートドライバーは、NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG 状態表示を使用して、ミニポートアダプターのヘッダーデータ分割構成が変更されたことを NDIS およびそれ以降のドライバーに通知します。
ms.assetid: 6605d888-bcbe-4898-aa25-4a4352fc50de
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: e4a0b127ad71a6fe1d3928f7e7d779574b1bc077
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833741"
---
# <a name="ndis_status_hd_split_current_config"></a>NDIS\_状態\_HD\_分割\_現在の\_構成


ミニポートドライバーは、NDIS\_の状態\_HD\_SPLIT\_現在の\_構成の状態の表示を使用して、ミニポートアダプターのヘッダーデータ分割構成が変更されたことを NDIS およびそれ以降のドライバーに通知します。

<a name="remarks"></a>注釈
-------

ミニポートドライバーが[\_GEN\_hd\_split\_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters) set request の分類を受け取ると、ドライバーは、 [**NDIS\_HD\_split\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)構造の内容を使用して現在のを更新する必要があります。ミニポートアダプターの構成。 更新後に、ミニポートドライバーは、NDIS\_状態\_HD\_SPLIT\_現在の\_構成状態の表示で変更を報告する必要があります。 状態の表示によって、すべてのドライバーが新しい情報で更新されます。

[**Ndis\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーには、[**現在の\_構成構造\_分割された ndis\_HD\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)が含まれています。 この構造体は、ミニポートアダプターの現在のヘッダーデータの分割構成を指定します。

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
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_HD\_分割\_現在の\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)

[**NDIS\_状態\_HD\_分割\_現在の\_構成**](ndis-status-hd-split-current-config.md)

[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_GEN\_HD\_SPLIT\_パラメーターの分割](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)

 

 




