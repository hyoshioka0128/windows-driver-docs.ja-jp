---
title: OID_GEN_VENDOR_ID
description: OID_GEN_VENDOR_ID OID として、クエリには、仕入先が特定の NIC を識別するために代入する 1 バイトの後に、3 バイト IEEE に登録されたベンダー コードを指定します
ms.assetid: dce0a2e4-5d34-417f-9764-85644fe2ce46
ms.date: 08/08/2017
keywords: -OID_GEN_VENDOR_ID ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 21524157a2a2cb38f8c8b5b84f734b5ed2db16c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387895"
---
# <a name="oidgenvendorid"></a>OID\_GEN\_ベンダー\_ID


クエリ、OID として\_GEN\_ベンダー\_ID OID を仕入先が特定の NIC を識別するために代入する 1 バイトの後に、3 バイト IEEE に登録されたベンダー コードを指定します

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
必須。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

IEEE コードは一意にベンダーを識別し、NIC のハードウェア アドレスの先頭に表示される 3 つのバイト数と同じです。

ベンダーは、IEEE 登録コードなしでは、値 0 xffffff を使用してください。

独立系ハードウェア ベンダーのフィルター ドライバーまたは中間ドライバーは、この OID をクエリがあります。

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

 

 




