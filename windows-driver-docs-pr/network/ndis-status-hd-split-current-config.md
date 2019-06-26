---
title: NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG
description: ミニポート ドライバーでは、NDIS および上にあるドライバーに通知することがあったミニポート アダプターのヘッダー データの分割構成の変更を NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG 状態を示す値を使用します。
ms.assetid: 6605d888-bcbe-4898-aa25-4a4352fc50de
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: b22e475563ab4a6ec4325d66e02655707cbc54bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368589"
---
# <a name="ndisstatushdsplitcurrentconfig"></a>NDIS\_状態\_HD\_分割\_現在\_構成


ミニポート ドライバーを使用して、NDIS\_状態\_HD\_分割\_現在\_ヘッダー データに変更されたが NDIS と関連付けたドライバーに通知する構成の状態の表示構成の分割ミニポート アダプター。

<a name="remarks"></a>注釈
-------

ミニポート ドライバーが受信すると、 [OID\_GEN\_HD\_分割\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)セットの要求、ドライバーの内容を使用する必要があります、 [ **NDIS\_HD\_分割\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)ミニポート アダプターの現在の構成を更新する構造体。 ミニポート ドライバー更新の後、NDIS での変更を報告する必要があります\_状態\_HD\_分割\_現在\_構成状態を示す値。 状態の表示により、新しい情報ですべての上にあるドライバーが更新されるようになります。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造に含まれる、 [ **NDIS\_HD\_分割\_現在\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)構造体。 この構造体には、ミニポート アダプターの現在のヘッダー データ分割構成を指定します。

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
<td><p>NDIS 6.1 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_HD\_分割\_現在\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)

[**NDIS\_状態\_HD\_分割\_現在\_構成**](ndis-status-hd-split-current-config.md)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_GEN\_HD\_分割\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)

 

 




