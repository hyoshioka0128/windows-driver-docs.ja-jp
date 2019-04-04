---
title: KSCATEGORY_AUDIO
description: KSCATEGORY_AUDIO
ms.assetid: 5acdca77-ed90-4f20-bdcc-5f51312c9dd7
keywords:
- KSCATEGORY_AUDIO デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_AUDIO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 711c81d0e78b01ca3198556dbc8f086b66cf6ada
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552402"
---
# <a name="kscategoryaudio"></a>KSCATEGORY_AUDIO


KSCATEGORY_AUDIO[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS)、オーディオ デバイスの機能のカテゴリ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>KSCATEGORY_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{6994AD04-93EF-11D0-A3CC-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS オーディオ デバイス用のドライバーは、デバイスが KSCATEGORY_AUDIO 機能カテゴリをサポートするオペレーティング システムに示すためにこのデバイスのインターフェイス クラスのインスタンスを登録します。

オーディオのアダプターのインターフェイス クラスのデバイスについては、[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff536813)を参照してください。

INF ファイルでこの機能のカテゴリを登録する方法については、ヘルプ ファイルを参照してください*INFViewer.html*と*ac97smpl.inf*、付属している、 [AC'97 サンプル ドライバー。](https://go.microsoft.com/fwlink/p/?linkid=256075) WDK に含まれています。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





