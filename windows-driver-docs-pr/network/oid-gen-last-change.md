---
title: OID_GEN_LAST_CHANGE
description: クエリとして OID_GEN_LAST_CHANGE OID を使用して、ネットワーク インターフェイス (RFC 2863 から ifLastChange) の最後の操作状態の変更の時刻を確認します。
ms.assetid: bd96d1ec-2fd0-491f-acb4-c1594ce6a084
ms.date: 08/08/2017
keywords: -OID_GEN_LAST_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 40330e5150a2ef45be4c3057ec319fd971adbd66
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375696"
---
# <a name="oidgenlastchange"></a>OID\_GEN\_最後\_変更


クエリとして、OID を使用して、\_GEN\_最後\_ネットワーク インターフェイスの最後の操作状態の変更の時刻を確認する変更の OID (*ifLastChange*から[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)).

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

のみ[ネットワーク インターフェイスの NDIS](https://msdn.microsoft.com/library/windows/hardware/ff566527)プロバイダー、およびミニポート ドライバーではないまたはフィルター ドライバー、そのためには、OID 要求としてこの OID をサポートする必要があります。

この OID は、インターフェイスが現在の運用状態になったときに、最後のコンピューターの再起動から開始時間を返します。 操作の状態の詳細については、次を参照してください[ **NDIS\_状態\_工程\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567406)と[OID\_GEN\_。OPERATIONAL\_状態](oid-gen-operational-status.md)します。 現在の時刻を取得するインターフェイスをプロバイダーが呼び出すことができます、 [ **NdisGetSystemUpTimeEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562675)関数。

現在の操作状態は、インターフェイスの最後の再初期化する前に入力された、この値は 0 にする必要があります。 . インターフェイス プロバイダーを追跡しない場合は、動作状態を変更する時間、値は 0 を指定する必要があります。

インターフェイスのプロバイダーは、NDIS を返した場合\_状態\_成功すると、クエリの結果は、最後のコンピューターの再起動 (ミリ秒単位) の状態の変更時刻を指定する ULONG64 値。

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


[OID\_GEN\_OPERATIONAL\_状態](oid-gen-operational-status.md)

[**NDIS\_状態\_工程\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567406)

[**NdisGetSystemUpTimeEx**](https://msdn.microsoft.com/library/windows/hardware/ff562675)

[NDIS ネットワーク インターフェイスの Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




