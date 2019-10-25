---
title: OID_GEN_LAST_CHANGE
description: クエリとして、OID_GEN_LAST_CHANGE OID を使用して、ネットワークインターフェイス (RFC 2863 から ifLastChange) の操作状態の最終変更時刻を確認します。
ms.assetid: bd96d1ec-2fd0-491f-acb4-c1594ce6a084
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_LAST_CHANGE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: e5b1e7a4b5de1802ffb7c7c750f588f9e4885bc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844621"
---
# <a name="oid_gen_last_change"></a>OID\_GEN\_最終\_変更


クエリとして、OID\_GEN\_最後\_OID を使用して、ネットワークインターフェイスの操作状態が最後に変更された時刻 ( [RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)からの*ifLastChange* ) を確認します。

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
要求されていません。 NDIS インターフェイスプロバイダーのみ。

<a name="remarks"></a>注釈
-------

この OID を OID 要求としてサポートする必要があるのは、 [NDIS ネットワークインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)プロバイダーだけです。そのため、ミニポートドライバーやフィルタードライバーはサポートされません。

この OID は、最後にコンピューターを再起動したときから、インターフェイスが現在の動作状態に戻ったときからの時間を返します。 動作状態の詳細については、「 [**NDIS\_status\_OPER\_status**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-oper-status) 」および「 [OID\_GEN\_operational\_STATUS](oid-gen-operational-status.md)」を参照してください。 現在の時刻を取得するために、インターフェイスプロバイダーは[**NdisGetSystemUpTimeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetsystemuptimeex)関数を呼び出すことができます。

現在の操作状態が、インターフェイスの最後の再初期化の前に入力された場合、この値は0にする必要があります。 の順に移動します。 インターフェイスプロバイダーが動作状態の変更時刻を追跡しない場合、値は0にする必要があります。

インターフェイスプロバイダーが NDIS\_STATUS\_SUCCESS を返した場合、クエリの結果は、最後のコンピューターが再起動してからの状態変更時間 (ミリ秒単位) を指定する ULONG64 値になります。

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


[OID\_GEN\_操作\_の状態](oid-gen-operational-status.md)

[**NDIS\_STATUS\_OPER\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-oper-status)

[**NdisGetSystemUpTimeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetsystemuptimeex)

[NDIS ネットワークインターフェイス Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




