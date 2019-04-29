---
title: NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE
description: VM ネットワーク アダプターのミニポート ドライバーは、ルーティング ドメインの構成は、ネットワーク アダプターのポートで更新されるたびに、NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE 状態を示す値を生成します。
ms.assetid: 4F3916B6-F52D-4B99-8F1C-A4A5BA9B307B
ms.date: 08/08/2017
keywords: -NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2f8b713befb209af4db83f786f1a564263b63471
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323446"
---
# <a name="ndisstatusisolationparameterschange"></a>NDIS\_状態\_分離\_パラメーター\_変更


VM ネットワーク アダプターのミニポート ドライバーが生成されます、 **NDIS\_状態\_分離\_パラメーター\_変更**状態表示のときに、ルーティング ドメインの構成ネットワーク アダプターのポートで更新されます。 これは、場合、トリガーに対して発行することによって、マルチ テナント機能の構成を再クエリする TCP レイヤー、 [OID\_GEN\_分離\_パラメーター](oid-gen-isolation-parameters.md) OID。 この状態表示の状態のバッファーではありません。

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
<td><p>NDIS 6.40 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_状態\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_GEN\_分離\_パラメーター](oid-gen-isolation-parameters.md)

 

 




