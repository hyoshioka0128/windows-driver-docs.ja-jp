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
ms.openlocfilehash: c1acf61ef1314849a6ed90fb76c4fc80ccf07b62
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366715"
---
# <a name="kscategoryaudio"></a>KSCATEGORY_AUDIO


KSCATEGORY_AUDIO[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS)、オーディオ デバイスの機能のカテゴリ。

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

オーディオのアダプターのインターフェイス クラスのデバイスについては、次を参照してください。[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://docs.microsoft.com/windows-hardware/drivers/audio/installing-device-interfaces-for-an-audio-adapter)します。

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

 

 





