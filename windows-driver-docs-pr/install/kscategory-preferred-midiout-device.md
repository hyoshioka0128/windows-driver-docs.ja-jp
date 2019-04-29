---
title: KSCATEGORY_PREFERRED_MIDIOUT_DEVICE
description: KSCATEGORY_PREFERRED_MIDIOUT_DEVICE
ms.assetid: b3d93d21-d4f8-4f00-9947-034790f3f7b1
keywords:
- KSCATEGORY_PREFERRED_MIDIOUT_DEVICE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_PREFERRED_MIDIOUT_DEVICE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf5f52954b2c6ab4238743ecda60728b98a5def3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390746"
---
# <a name="kscategorypreferredmidioutdevice"></a>KSCATEGORY_PREFERRED_MIDIOUT_DEVICE


KSCATEGORY_PREFERRED_MIDIOUT_DEVICE[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)優先 MIDI の機能のカテゴリ (KS) は、デバイスを出力します。

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
<td align="left"><p>KSCATEGORY_PREFERRED_WAVEOUT_DEVICE</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{D6C50674-72C1-11D2-9755-0000F8004788}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ユーザーは、マルチ メディアのプロパティ ページ、コントロール パネルで、優先する MIDI 出力デバイスを選択します。

この機能のカテゴリは、システムが提供して排他的に使用用に予約された[WDM オーディオ コンポーネント](https://msdn.microsoft.com/library/windows/hardware/ff538905)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Server 2003、Windows XP、Windows 2000 および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





