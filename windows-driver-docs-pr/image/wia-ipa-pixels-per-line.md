---
title: WIA\_IPA\_ピクセル\_1 秒あたり\_行
description: WIA\_IPA\_ピクセル\_1 秒あたり\_ライン プロパティにイメージ (つまり、イメージには、ピクセルの幅) の行ごとのピクセル数が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: ec845e34-d883-4960-a1cd-39b99e2f5941
keywords:
- WIA_IPA_PIXELS_PER_LINE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_PIXELS_PER_LINE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d45ebcc5ee4cb8889881843afe37c095e88c8d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384649"
---
# <a name="wiaipapixelsperline"></a>WIA\_IPA\_ピクセル\_1 秒あたり\_行


WIA\_IPA\_ピクセル\_1 秒あたり\_ライン プロパティにイメージ (つまり、イメージには、ピクセルの幅) の行ごとのピクセル数が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipa_pixels_per_line_si"></span><span id="DDK_WIA_IPA_PIXELS_PER_LINE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

WIA\_IPA\_ピクセル\_1 秒あたり\_行プロパティは転送が有効なすべての項目の Windows Vista のドライバーのオプションです。 場合 WIA\_IPA\_ピクセル\_1 秒あたり\_行、 [ **WIA\_IPA\_バイト\_1 秒あたり\_行**](wia-ipa-bytes-per-line.md)、および[ **WIA\_IPA\_数\_の\_行**](wia-ipa-number-of-lines.md)実装は、Windows Server 2003 用に記述されたアプリケーションWindows XP、および Windows の以前のバージョンは、行、各スキャン ラインに必要なバイト数、および画像のスキャン ラインの合計数ごとのピクセルの数を見積もることができます。 これらの値は、イメージ処理フィルターは、実際の値では、どの WIA を変更可能性がありますので、正確な\_IPA\_ピクセル\_1 秒あたり\_行、WIA\_IPA\_バイト\_あたり\_線、および WIA\_IPA\_数\_の\_線を表します。

Windows Vista ドライバーがこれらのプロパティを指定しない場合、WIA サービスで互換レイヤーはこれらのプロパティを追加します。 使用して更新されます、WIA サービスがこれらのプロパティを追加するとき、 [ **WIA\_IPA\_深さ**](wia-ipa-depth.md)、 [ **WIA\_のipアドレス\_XEXTENT**](wia-ips-xextent.md)、および[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)プロパティ。

Windows Vista アプリケーションでは、以上に示したプロパティから使用できる情報よりも正確であるイメージに関する情報を取得するイメージ ヘッダー データを常に解析する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>すべての転送が有効な項目の Windows Vista のドライバーの省略可能。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_バイト\_1 秒あたり\_行**](wia-ipa-bytes-per-line.md)

[**WIA\_IPA\_深さ**](wia-ipa-depth.md)

[**WIA\_IPA\_数\_の\_行**](wia-ipa-number-of-lines.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

 

 






