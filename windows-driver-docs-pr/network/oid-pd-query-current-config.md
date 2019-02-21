---
title: OID_PD_QUERY_CURRENT_CONFIG
description: NDIS プロトコルまたはフィルター ドライバーは、PD 状態と機能を取得する PD 対応ミニポート ドライバーに OID_PD_QUERY_CURRENT_CONFIG のオブジェクト識別子 (OID) メソッド要求を送信します。 PD 対応のすべてのミニポート ドライバーでは、この OID 要求を処理する必要があります。
ms.assetid: 1BF09EAE-9D03-4655-98CD-D3A10BF48A48
ms.date: 08/08/2017
keywords: -OID_PD_QUERY_CURRENT_CONFIG ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1c35c2c408bd89f804ebaafb2c80fa933dc3ded9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532134"
---
# <a name="oidpdquerycurrentconfig"></a>OID\_PD\_クエリ\_現在\_構成


OID のオブジェクト識別子 (OID) メソッド要求を送信する NDIS プロトコルまたはフィルター ドライバー\_PD\_クエリ\_現在\_PD 状態と機能を取得する PD 対応ミニポート ドライバーを構成します。 PD 対応のすべてのミニポート ドライバーでは、この OID 要求を処理する必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には、バッファーへのポインターが含まれています。 このバッファーには、次のデータが含まれています。

-   [ **NDIS\_PD\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/dn931835)構造体

<a name="remarks"></a>注釈
-------

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)

[**NDIS\_PD\_構成**](https://msdn.microsoft.com/library/windows/hardware/dn931835)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

 

 




