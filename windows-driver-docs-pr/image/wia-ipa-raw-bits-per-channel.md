---
title: WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル
description: WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル プロパティには、各カラー チャネルのビット数が含まれています。
ms.assetid: 541d5409-b095-4bf0-bdc7-cc56d416ed43
keywords:
- WIA_IPA_RAW_BITS_PER_CHANNEL イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_RAW_BITS_PER_CHANNEL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e56a74db4ed907929088e64602f3d8de5f04e146
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535953"
---
# <a name="wiaiparawbitsperchannel"></a>WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル


WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル プロパティには、各カラー チャネルのビット数が含まれています。

## <span id="ddk_wia_ipa_raw_bits_per_channel_si"></span><span id="DDK_WIA_IPA_RAW_BITS_PER_CHANNEL_SI"></span>


プロパティの種類:VT\_UI1 |VT\_ベクター

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

WIA\_IPA\_RAW\_ビット\_1 秒あたり\_ベクターがあるため、多くのバイト値を含むチャネル、最初のバイトがビット数に対応する場所として、チャネル プロパティを報告する必要があります最初のチャネルでは、2 番目のチャネルでのビット数を 2 番目のバイト。 ベクターとして数のエントリを含める必要があります、 [ **WIA\_IPA\_チャネル\_1 秒あたり\_ピクセル**](wia-ipa-channels-per-pixel.md)チャンネルがプロパティを報告します。 ドライバー設定 WIA\_IPA\_チャネルあたり\_ピクセル、アプリケーションを設定すると[ **WIA\_IPA\_形式**](wia-ipa-format.md) WiaImgFmtに\_生です。

WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネルと似ています、 [ **WIA\_IPA\_ビット\_1 秒あたり\_チャネル**](wia-ipa-bits-per-channel.md)プロパティ (これは RAW 以外の形式の使用)。

次の表に、必要な WIA 内のエントリ数\_IPA\_RAW\_ビット\_1 秒あたり\_wia が定義されているチャネル\_IPA\_データ型の値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WIA_IPA_DATATYPE 値</th>
<th>必要な WIA_IPA_RAW_BITS_PER_CHANNEL 内のエントリ数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DATA_DITHER</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_GRAYSCALE</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_BGR</p></td>
<td><p>3</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_CMY</p></td>
<td><p>3</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_CMYK</p></td>
<td><p>4</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_RGB</p></td>
<td><p>3</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_YUV</p></td>
<td><p>3</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_YUVK</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_THRESHOLD</p></td>
<td><p>1</p></td>
</tr>
</tbody>
</table>

 

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
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_チャネル\_1 秒あたり\_ピクセル**](wia-ipa-channels-per-pixel.md)

[**WIA\_IPA\_データ型**](wia-ipa-datatype.md)

[**WIA\_IPA\_形式**](wia-ipa-format.md)

 

 






