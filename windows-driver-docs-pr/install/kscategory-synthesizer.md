---
title: KSCATEGORY_SYNTHESIZER
description: KSCATEGORY_SYNTHESIZER
ms.assetid: 07713c80-adff-4c3d-a9df-2c2865ef78d9
keywords:
- KSCATEGORY_SYNTHESIZER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_SYNTHESIZER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d4e0ef43b9d42bcbf5ff6d9b242c104c2f67338b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366695"
---
# <a name="kscategorysynthesizer"></a>KSCATEGORY_SYNTHESIZER


KSCATEGORY_SYNTHESIZER[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)MIDI データ wave オーディオ サンプルまたは、出力をアナログ信号に変換する (KS) 機能のカテゴリ。

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
<td align="left"><p>KSCATEGORY_SYNTHESIZER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{DFF220F3-F70F-11D0-B917-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

KS オーディオ アダプター デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_SYNTHESIZER 機能カテゴリをサポートすることを示す KSCATEGORY_SYNTHESIZER のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法の例は、次を参照してください、 *Ddksynth.inf* INF ファイルでのソフトウェアのシンセサイザー サンプルに含まれている、 *src\\オーディオ\\ddksynth。* WDK のディレクトリ。

シンセサイザーの詳細については、次を参照してください。 [MIDI と DirectMusic フィルター](https://docs.microsoft.com/windows-hardware/drivers/audio/midi-and-directmusic-filters)します。

オーディオのアダプターのインターフェイス クラスのデバイスについては、次を参照してください。[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://docs.microsoft.com/windows-hardware/drivers/audio/installing-device-interfaces-for-an-audio-adapter)します。

<a name="requirements"></a>必要条件
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

 

 





