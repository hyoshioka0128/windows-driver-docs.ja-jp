---
title: OID_GEN_DISCONTINUITY_TIME
description: クエリとして、OID_GEN_DISCONTINUITY_TIME OID を使用して、ネットワークインターフェイス (RFC 2863 から ifCounterDiscontinuityTime) の不連続時間を決定します。
ms.assetid: 3eac6818-c346-47f6-b812-f98b808dc36a
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_DISCONTINUITY_TIME ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: c6cf543aaf140cf97d63d7891ee30c3e395f6aed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837985"
---
# <a name="oid_gen_discontinuity_time"></a>OID\_GEN\_不連続\_時間


クエリとして、OID\_GEN\_不連続\_時間 OID を使用して、ネットワークインターフェイス ( [RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)からの*ifCounterDiscontinuityTime* ) の不連続時間を決定します。

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 NDIS インターフェイスプロバイダーのみ。

<a name="remarks"></a>注釈
-------

この OID を OID 要求としてサポートする必要があるのは、 [NDIS ネットワークインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダーだけです。そのため、ミニポートドライバーやフィルタードライバーはサポートされません。

この OID は、前回のコンピューターの再起動からの時間を返します。これは、インターフェイスが統計カウンターを維持する際に不連続性を持っていた場合に発生します。 たとえば、インターフェイスが無効になっていたか、関連付けられているアダプターがコンピューターから削除されたため、不連続性が発生しました。 統計カウンターの詳細については、「 [OID\_GEN\_statistics](oid-gen-statistics.md)」を参照してください。 現在の時刻を取得するために、インターフェイスプロバイダーは[**NdisGetSystemUpTimeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetsystemuptimeex)関数を呼び出すことができます。

インターフェイスの前回の再初期化以降にこのような不連続性が発生しなかった場合は、この値を0にする必要があります。 インターフェイスプロバイダーで不連続性時間が追跡されない場合、この値は0にする必要があります。

インターフェイスプロバイダーが NDIS\_STATUS\_SUCCESS を返した場合、クエリの結果は、最後のコンピューターが再起動してからの、ULONG64 の時間をミリ秒単位で指定する値になります。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[NDIS ネットワークインターフェイス Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




