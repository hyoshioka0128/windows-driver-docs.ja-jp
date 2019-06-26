---
title: KSCATEGORY_PREFERRED_WAVEOUT_DEVICE
description: KSCATEGORY_PREFERRED_WAVEOUT_DEVICE
ms.assetid: bba79780-e89c-4b19-98e0-84bfdb5bbf25
keywords:
- KSCATEGORY_PREFERRED_WAVEOUT_DEVICE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_PREFERRED_WAVEOUT_DEVICE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 540281cb3a638a5fc05a58e3ca4ec6c70888e1a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353384"
---
# <a name="kscategorypreferredwaveoutdevice"></a>KSCATEGORY_PREFERRED_WAVEOUT_DEVICE


KSCATEGORY_PREFERRED_WAVEIN_DEVICE[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)優先 wave 入力デバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>{D6C5066E-72C1-11D2-9755-0000F8004788}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ユーザーは、マルチ メディアのプロパティ ページ、コントロール パネルで、優先 wave 入力デバイスを選択します。

この機能のカテゴリは、システムが提供して排他的に使用用に予約された[WDM オーディオ コンポーネント](https://docs.microsoft.com/windows-hardware/drivers/audio/wdm-audio-components)します。

<a name="requirements"></a>必要条件
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

 

 





