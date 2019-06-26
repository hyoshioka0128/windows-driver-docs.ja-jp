---
title: KSCATEGORY_CAPTURE
description: KSCATEGORY_CAPTURE
ms.assetid: b33e9a04-00f2-4cfa-911e-55461ce5aae7
keywords:
- KSCATEGORY_CAPTURE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_CAPTURE
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 05370a49f25847204c1b9648ea5b44ddb3a6ae58
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384253"
---
# <a name="kscategorycapture"></a>KSCATEGORY_CAPTURE


KSCATEGORY_CAPTURE[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)wave または MIDI データ ストリームをキャプチャする (KS) 機能のカテゴリ。

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
<td align="left"><p>KSCATEGORY_CAPTURE</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{65E8773D-8F56-11D0-A3B9-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、デバイスが KSCATEGORY_CAPTURE 機能カテゴリをサポートすることを示す KSCATEGORY_CAPTURE のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法については、次を参照してください。、 *Ac97smpl.inf* INF ファイルに含まれている、 [AC'97 サンプル ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256075) WDK で提供されています。

オーディオのアダプターのインターフェイス クラスのデバイスについては、次を参照してください。[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://docs.microsoft.com/windows-hardware/drivers/audio/installing-device-interfaces-for-an-audio-adapter)します。

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
<td align="left">Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

 

 





