---
title: OID_GEN_DRIVER_VERSION
description: クエリとしては、OID_GEN_DRIVER_VERSION OID は、使用中、ミニポート ドライバーで NDIS バージョンを指定します。
ms.assetid: 8c3ac2ab-a83a-44d2-88bc-bd1468a0a59b
ms.date: 08/08/2017
keywords: -OID_GEN_DRIVER_VERSION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6ec8884119840a4f8af74f42663abb5368f54ff9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580712"
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

<a name="remarks"></a>コメント
-------

NDIS は、NDIS 6.0 とそれ以降のミニポート ドライバーのこの OID を処理します。

上位バイトはメジャー バージョン番号です。下位バイトは、マイナー バージョン番号です。

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

 

 




