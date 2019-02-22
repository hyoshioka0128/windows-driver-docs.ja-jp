---
title: WIA\_IPA\_FILENAME\_拡張機能
description: WIA\_IPA\_FILENAME\_拡張機能プロパティには、特定のファイル形式のファイル名拡張子が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 08abb3f2-73a2-42cd-ae69-1607eda63d1e
keywords:
- WIA_IPA_FILENAME_EXTENSION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_FILENAME_EXTENSION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d83166d781d5b70493106079ecf4d02eaf89b80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537940"
---
# <a name="wiaipafilenameextension"></a>WIA\_IPA\_FILENAME\_拡張機能


WIA\_IPA\_FILENAME\_拡張機能プロパティには、特定のファイル形式のファイル名拡張子が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipa_filename_extension_si"></span><span id="DDK_WIA_IPA_FILENAME_EXTENSION_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

ミニドライバー、更新、WIA\_IPA\_FILENAME\_拡張機能プロパティの現在の値を反映するように、 [ **WIA\_IPA\_形式**](wia-ipa-format.md)プロパティ。

たとえば場合、WIA\_IPA\_形式は WiaImgFmt\_JPEG、WIA\_IPA\_FILENAME\_拡張機能は、"jpg"をする必要があります。 場合 WIA\_IPA\_形式は WiaImgFmt\_BMP、WIA\_IPA\_FILENAME\_拡張機能は、"bmp"をする必要があります。 ファイル名拡張子にピリオドが含まれていないことに注意してください (".")。

WIA\_IPA\_FILENAME\_拡張機能プロパティを選択し、標準形式をサポートするドライバーをお勧めのカスタム定義の書式を実装するドライバーが必要です。 WIA\_IPA\_FILENAME\_形式のファイルをプライベートの転送中に使用する正しいファイル名拡張子のアプリケーション拡張機能が通知されます。 たとえば、A. Datum Corporation は、新しい形式でファイルを転送する WIA ドライバーを作成する場合、会社は"adc"の拡張機能を指定できます。 この拡張により、アプリケーションなどのファイル名を作成して、ファイルにその形式でデータを転送する*Myfile.adc*、これは、新しい拡張機能を理解している他のユーザーに有用です。

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


[**WIA\_IPA\_形式**](wia-ipa-format.md)

 

 






