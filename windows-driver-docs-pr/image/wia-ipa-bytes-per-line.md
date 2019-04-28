---
title: WIA\_IPA\_バイト\_1 秒あたり\_行
description: WIA\_IPA\_バイト\_1 秒あたり\_ライン プロパティには、イメージの 1 つのスキャン ラインのバイト数が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: f746ce05-5dfe-47fe-857a-967a6144de16
keywords:
- WIA_IPA_BYTES_PER_LINE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_BYTES_PER_LINE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e79195687a1199ec7bffd9336dd651e63127a6e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369558"
---
# <a name="wiaipabytesperline"></a>WIA\_IPA\_バイト\_1 秒あたり\_行


WIA\_IPA\_バイト\_1 秒あたり\_ライン プロパティには、イメージの 1 つのスキャン ラインのバイト数が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipa_bytes_per_line_si"></span><span id="DDK_WIA_IPA_BYTES_PER_LINE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

WIA\_IPA\_バイト\_1 秒あたり\_行プロパティは転送が有効なすべての項目の Windows Vista のドライバーのオプションです。 場合このプロパティは、と共に、 [ **WIA\_IPA\_数\_の\_行**](wia-ipa-number-of-lines.md)と[ **WIA\_IPA\_ピクセル\_1 秒あたり\_行**](wia-ipa-pixels-per-line.md)アプリケーションが Windows Server 2003、Windows XP、Windows の以前のバージョン用に設計を見積もることができるプロパティは、それぞれの行、各スキャン ラインに必要なバイト数、および画像のスキャン ラインの合計数のピクセルの数。 イメージ処理のフィルターがこれらのプロパティが表す実際の値を変更するため、これらの値は正確ではありません。

Windows Vista ドライバーがこれらのプロパティを指定しない場合、WIA サービスで互換レイヤーはこれらのプロパティを追加します。 使用して更新されます、WIA サービスがこれらのプロパティを追加するとき、 [ **WIA\_IPA\_深さ**](wia-ipa-depth.md)、 [ **WIA\_のipアドレス\_XEXTENT**](wia-ips-xextent.md)、および[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)プロパティ。

Windows Vista アプリケーションのイメージのより正確な情報を取得するイメージ ヘッダー データを常に解析する必要があり、これらのプロパティから利用可能です。

<a name="requirements"></a>必要条件
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


[**WIA\_IPA\_深さ**](wia-ipa-depth.md)

[**WIA\_IPA\_数\_の\_行**](wia-ipa-number-of-lines.md)

[**WIA\_IPA\_ピクセル\_1 秒あたり\_行**](wia-ipa-pixels-per-line.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

 

 






