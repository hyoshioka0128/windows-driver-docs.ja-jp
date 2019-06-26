---
title: OID_GEN_LAST_CHANGE
description: クエリとして OID_GEN_LAST_CHANGE OID を使用して、ネットワーク インターフェイス (RFC 2863 から ifLastChange) の最後の操作状態の変更の時刻を確認します。
ms.assetid: bd96d1ec-2fd0-491f-acb4-c1594ce6a084
ms.date: 08/08/2017
keywords: -OID_GEN_LAST_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 1b9385b9c8164c33a4a0b7232854ec6fe207fe1f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369094"
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

のみ[ネットワーク インターフェイスの NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダー、およびミニポート ドライバーではないまたはフィルター ドライバー、そのためには、OID 要求としてこの OID をサポートする必要があります。

この OID は、インターフェイスが現在の運用状態になったときに、最後のコンピューターの再起動から開始時間を返します。 操作の状態の詳細については、次を参照してください[ **NDIS\_状態\_工程\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-oper-status)と[OID\_GEN\_。OPERATIONAL\_状態](oid-gen-operational-status.md)します。 現在の時刻を取得するインターフェイスをプロバイダーが呼び出すことができます、 [ **NdisGetSystemUpTimeEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetsystemuptimeex)関数。

現在の操作状態は、インターフェイスの最後の再初期化する前に入力された、この値は 0 にする必要があります。 . インターフェイス プロバイダーを追跡しない場合は、動作状態を変更する時間、値は 0 を指定する必要があります。

インターフェイスのプロバイダーは、NDIS を返した場合\_状態\_成功すると、クエリの結果は、最後のコンピューターの再起動 (ミリ秒単位) の状態の変更時刻を指定する ULONG64 値。

<a name="requirements"></a>必要条件
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

[**NDIS\_状態\_工程\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-oper-status)

[**NdisGetSystemUpTimeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetsystemuptimeex)

[NDIS ネットワーク インターフェイスの Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




