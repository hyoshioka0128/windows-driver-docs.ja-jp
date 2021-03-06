---
title: OID_GEN_DISCONTINUITY_TIME
description: クエリとして OID_GEN_DISCONTINUITY_TIME OID を使用して、(RFC 2863 から ifCounterDiscontinuityTime) のネットワーク インターフェイスの以降の不連続性の時間を決定します。
ms.assetid: 3eac6818-c346-47f6-b812-f98b808dc36a
ms.date: 08/08/2017
keywords: -OID_GEN_DISCONTINUITY_TIME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 26b11a4694eac734ce093c0863188676dc3c02ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369118"
---
# <a name="oidgendiscontinuitytime"></a>OID\_GEN\_以降の不連続性\_時間


クエリとして、OID を使用して、\_GEN\_以降の不連続性\_ネットワーク インターフェイスの以降の不連続性の時間を確認する時間の OID (*ifCounterDiscontinuityTime*から[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)).

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

のみ[ネットワーク インターフェイスの NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダー、およびミニポート ドライバーではないまたはフィルター ドライバー、そのためには、OID 要求としてこの OID をサポートする必要があります。

この OID は、インターフェイスがある、統計カウンターを維持する上で連続していない場合に、最後のコンピューターの再起動から開始時間を返します。 インターフェイスが無効になっているか、関連付けられているアダプターがコンピューターから削除されたため、以降の不連続性がありましたなど。 統計カウンターの詳細については、次を参照してください。 [OID\_GEN\_統計](oid-gen-statistics.md)します。 現在の時刻を取得するインターフェイスをプロバイダーが呼び出すことができます、 [ **NdisGetSystemUpTimeEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetsystemuptimeex)関数。

インターフェイスの最後の再初期化後にこのような不連続性が発生していない場合は、この値は 0 にする必要があります。 インターフェイス プロバイダーは、以降の不連続性の時間を追跡していない、この値は 0 にする必要があります。

インターフェイスのプロバイダーは、NDIS を返した場合\_状態\_成功すると、クエリの結果は、以降の不連続性の時間を最後のコンピューターの再起動 (ミリ秒単位) を指定する ULONG64 値。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[NDIS ネットワーク インターフェイスの Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




