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
ms.openlocfilehash: 3c182cb446cf0ea2d4517ac3a939b91ea7e7f2df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582532"
---
# <a name="kscategorysynthesizer"></a>KSCATEGORY_SYNTHESIZER


KSCATEGORY_SYNTHESIZER[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)MIDI データ wave オーディオ サンプルまたは、出力をアナログ信号に変換する (KS) 機能のカテゴリ。

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

シンセサイザーの詳細については、次を参照してください。 [MIDI と DirectMusic フィルター](https://msdn.microsoft.com/library/windows/hardware/ff537520)します。

オーディオのアダプターのインターフェイス クラスのデバイスについては、次を参照してください。[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff536813)します。

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

 

 





