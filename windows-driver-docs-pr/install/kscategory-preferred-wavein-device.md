---
title: KSCATEGORY_PREFERRED_WAVEIN_DEVICE
description: KSCATEGORY_PREFERRED_WAVEIN_DEVICE
ms.assetid: d5f20f18-396a-4cb7-b653-038310ce8e42
keywords:
- KSCATEGORY_PREFERRED_WAVEIN_DEVICE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_PREFERRED_WAVEIN_DEVICE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d27182bb6bb4bf463046235084dd38a0f22428e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529923"
---
# <a name="kscategorypreferredwaveindevice"></a>KSCATEGORY_PREFERRED_WAVEIN_DEVICE


KSCATEGORY_PREFERRED_WAVEIN_DEVICE[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)優先 wave 入力デバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_PREFERRED_WAVEIN_DEVICE</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{D6C50671-72C1-11D2-9755-0000F8004788}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ユーザーは、マルチ メディアのプロパティ ページ、コントロール パネルで、優先 wave 入力デバイスを選択します。

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

 

 





