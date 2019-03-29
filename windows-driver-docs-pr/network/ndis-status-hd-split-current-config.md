---
title: NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG
description: ミニポート ドライバーでは、NDIS および上にあるドライバーに通知することがあったミニポート アダプターのヘッダー データの分割構成の変更を NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG 状態を示す値を使用します。
ms.assetid: 6605d888-bcbe-4898-aa25-4a4352fc50de
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 50b99e004bce1df1a5b2dff8eb1493adea8dd2e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573194"
---
# <a name="ndisstatushdsplitcurrentconfig"></a>NDIS\_状態\_HD\_分割\_現在\_構成


ミニポート ドライバーを使用して、NDIS\_状態\_HD\_分割\_現在\_ヘッダー データに変更されたが NDIS と関連付けたドライバーに通知する構成の状態の表示構成の分割ミニポート アダプター。

<a name="remarks"></a>コメント
-------

ミニポート ドライバーが受信すると、 [OID\_GEN\_HD\_分割\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569587)セットの要求、ドライバーの内容を使用する必要があります、 [ **NDIS\_HD\_分割\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565701)ミニポート アダプターの現在の構成を更新する構造体。 ミニポート ドライバー更新の後、NDIS での変更を報告する必要があります\_状態\_HD\_分割\_現在\_構成状態を示す値。 状態の表示により、新しい情報ですべての上にあるドライバーが更新されるようになります。

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造に含まれる、 [ **NDIS\_HD\_分割\_現在\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff565696)構造体。 この構造体には、ミニポート アダプターの現在のヘッダー データ分割構成を指定します。

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


[**NDIS\_HD\_分割\_現在\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff565696)

[**NDIS\_状態\_HD\_分割\_現在\_構成**](ndis-status-hd-split-current-config.md)

[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_GEN\_HD\_分割\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569587)

 

 




