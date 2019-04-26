---
title: OID_GEN_LINK_STATE
description: クエリとして NDIS および上にあるドライバーはミニポート アダプターの現在のリンクの状態を判断するのに OID_GEN_LINK_STATE OID を使用します。
ms.assetid: 75a30054-8700-4b79-902c-c8382a25c0a2
ms.date: 08/08/2017
keywords: -OID_GEN_LINK_STATE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7b37225cde129644fba488a88aa4d51d480fa511
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358888"
---
# <a name="oidgenlinkstate"></a>OID\_GEN\_リンク\_状態


クエリ、NDIS と関連付けたドライバーを使用、OID\_GEN\_リンク\_状態 OID ミニポート アダプターの現在のリンクの状態を確認します。 ミニポート ドライバーで、リンクの状態の受信、 [ **NDIS\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh205390)構造体。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 (「解説」を参照してください セクション)

<a name="remarks"></a>注釈
-------

ミニポート ドライバーでは、初期化中に、リンクの状態を指定し、状態インジケーターの更新プログラムを提供します。

リンクの状態を指定するには、設定、 **MediaConnectState**、 **MediaDuplexState**、 **XmitLinkSpeed**、 **RcvLinkSpeed**、 **PauseFunctions**、および**AutoNegotiationFlags**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_[全般]\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)ミニポート ドライバーに渡します構造、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。

ミニポート ドライバーがこの OID をサポートしていない場合、ドライバーは NDIS を返す必要があります\_状態\_いない\_サポートされています。 ミニポート ドライバーは、この OID をサポートしている場合は、接続状態、双方向の状態を返します内のリンクが高速化、 [ **NDIS\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh205390)構造体。

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


[**NDIS\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh205390)

[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NDIS\_オブジェクト\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff566588)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[OID\_GEN\_メディア\_CONNECT\_状態\_例](oid-gen-media-connect-status-ex.md)

[OID\_GEN\_メディア\_双方向\_状態](oid-gen-media-duplex-state.md)

 

 




