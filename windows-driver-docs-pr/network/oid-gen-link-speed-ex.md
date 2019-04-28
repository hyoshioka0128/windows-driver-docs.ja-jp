---
title: OID_GEN_LINK_SPEED_EX
description: クエリとして OID_GEN_LINK_SPEED_EX OID は提供、送信とインターフェイスのリンク速度を受信します。 バージョン情報の Windows Vista と laterSupported します。 NDIS 6.0 とそれ以降のミニポート driversNot が要求されました。 NDIS インターフェイス プロバイダーのみです。
ms.assetid: 86cc281b-3898-484c-9418-4408a45ebe71
ms.date: 08/08/2017
keywords: -OID_GEN_LINK_SPEED_EX ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: a24c28d3dccef45e726e29d0c68212effbb33963
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375688"
---
# <a name="oidgenlinkspeedex"></a>OID\_GEN\_リンク\_速度\_例


クエリ、OID として\_GEN\_リンク\_速度\_EX OID はリンク速度インターフェイスの受信、送信します。

**バージョン情報**

<a href="" id="windows-vista-and-later"></a>Windows Vista 以降  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。 NDIS インターフェイス プロバイダーのみです。

<a name="remarks"></a>注釈
-------

NDIS はこの OID を使用してクエリのリンク速度を[ネットワーク インターフェイスの NDIS](https://msdn.microsoft.com/library/windows/hardware/ff566527)プロバイダー。 のみ NDIS インターフェイス プロバイダー、およびしたがってミニポート ドライバーではないまたはフィルター ドライバー、する必要がありますサポートこの OID OID 要求として。

この OID でリンク速度を返します、 [ **NDIS\_リンク\_速度**](https://msdn.microsoft.com/library/windows/hardware/ff565864)構造体。

ミニポート ドライバーでは、初期化中に、リンク速度を指定し、更新されたリンク速度を状態インジケーターに提供します。

ミニポート ドライバーでは、リンク速度を指定するには、設定、 **XmitLinkSpeed**と**RcvLinkSpeed**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)ミニポート ドライバーに渡します構造、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。

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


[**NDIS\_リンク\_速度**](https://msdn.microsoft.com/library/windows/hardware/ff565864)

[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)

[NDIS ネットワーク インターフェイスの Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




