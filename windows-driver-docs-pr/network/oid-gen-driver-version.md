---
title: OID_GEN_DRIVER_VERSION
description: クエリとしては、OID_GEN_DRIVER_VERSION OID は、使用中、ミニポート ドライバーで NDIS バージョンを指定します。
ms.assetid: 8c3ac2ab-a83a-44d2-88bc-bd1468a0a59b
ms.date: 08/08/2017
keywords: -OID_GEN_DRIVER_VERSION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6ec8884119840a4f8af74f42663abb5368f54ff9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381354"
---
# <a name="oidgendriverversion"></a>OID\_GEN\_ドライバー\_バージョン


クエリ、OID として\_GEN\_ドライバー\_バージョン OID ミニポート ドライバーによって使用中で NDIS バージョンを指定します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
要求されません。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
必須。

<a name="remarks"></a>注釈
-------

NDIS は、NDIS 6.0 とそれ以降のミニポート ドライバーのこの OID を処理します。

上位バイトはメジャー バージョン番号です。下位バイトは、マイナー バージョン番号です。

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

 

 




