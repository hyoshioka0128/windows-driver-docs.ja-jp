---
title: GetGlobalAttribute の使用
description: GetGlobalAttribute の使用
ms.assetid: 0e23ecba-7d89-44f5-b6a7-7d6be9a56765
keywords:
- GetGlobalAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 271bf32129c906728387a0ded92e641ebe4e2cda
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362729"
---
# <a name="using-getglobalattribute"></a>GetGlobalAttribute の使用





キーワード名が定義されているすべてのグローバル属性名が同じ*PostScript プリンター説明ファイル形式の仕様、v4.3*します。 自分のセマンティクスのためには、この仕様を参照してください。 (このリソースできない場合がありますのいくつかの言語および国。)

次の表に、 *pdwDataType*パラメーターの値には、 [ **EATTRIBUTE\_DATATYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/ne-printoem-_eattribute_datatype)列挙型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>グローバル属性</th>
<th>出力パラメーター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CenterRegistered</strong></p></td>
<td><p><em>pdwDataType: kADT_BOOL</p>
<p><em></em>pbData</em>:<strong>TRUE</strong>または<strong>FALSE</strong></p>
<p><em><em>pcbNeeded</em>: <strong>sizeof</strong>(BOOL)</p></td>
</tr>
<tr class="even">
<td><p><strong>ColorDevice</strong></p></td>
<td><p></em>pdwDataType: kADT_BOOL</p>
<p><em><em>pbData</em>:<strong>TRUE</strong>または<strong>FALSE</strong></p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(BOOL)</p></td>
</tr>
<tr class="odd">
<td><p><strong>拡張機能</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:ASCII 文字列 (レジストリ形式) で登録されている値を含む extensionOption のプリンターをサポートします。</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (最後の null 文字を含む)</p>
<p>注:"<em>ファイル システム。True"を扱われる場合と<strong></em>拡張</strong>"FileSystem"オプションがありました。 "FileSystem:False"を扱われるよう<em>拡張機能では"FileSystem"オプションがありませんでした。</p></td>
</tr>
<tr class="even">
<td><p><strong>FileVersion</strong></p></td>
<td><p><em></em>pdwDataType</em>: kADT_DWORD</p>
<p><em><em>pbData</em>: DWORD の上位ワードには、メジャー バージョン番号が含まれていますとの下位ワードにマイナー バージョン番号が含まれています。</p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>FreeVM</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p><em></em>pbData</em>: の値<em>FreeVM</p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><strong>LandscapeOrientation</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:NULL で終わる"Plus90"または"Minus90"のいずれかの文字列を ASCII です。</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (最後の null 文字を含む)</p>
<p>注:PPD が含まれている場合にのみ、"Minus90"が返される"<em>LandscapeOrientation:Minus90"。 その他のすべてのケースでは、"Plus90"が返されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LanguageEncoding</strong></p></td>
<td><p><em></em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:NULL で終わる ASCII 文字列 encodingOption 値は次のいずれかを含む:</p>
<p>"ISOLatin1"</p>
<p>"Unicode"</p>
<p>"JIS83-RKSJ"</p>
<p>"None"</p>
<p><em><em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (最後の null 文字を含む)</p>
<p>メモ</p>
<p>"WindowsANSI"を扱わ"ISOLatin1"と同じです。 その他の encodingOption 値がサポートされていません。</p>
<p>場合 * LanguageEncoding が存在しない場合は、* LanguageVersion の戻り値を推定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><strong>LanguageLevel</strong></p></td>
<td><p><em></em>pdwDataType</em>: kADT_DWORD</p>
<p><em><em>pbData</em>:プリンターでサポートされている、postScript 言語レベル</p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>ニックネーム</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_UNICODE</p>
<p><em>pbData</em>:Ppd の NULL で終わる Unicode 文字列 * ShortNickName の場合は値 * ShortNickName が存在する、または * 場合に値をニックネーム * ShortNickName が存在しません。</p>
<p><em></em>pcbNeeded</em>: Unicode 文字列のバイト数が指す<em>pbData</em> (最後の null 文字を含む)</p></td>
</tr>
<tr class="even">
<td><p><strong>PPD Adobe</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p><em></em>pbData</em>: DWORD の上位ワードには、メジャー バージョン番号が含まれていますとの下位ワードにマイナー バージョン番号が含まれています。</p>
<p><em><em>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>PrintPSErrors</strong></p></td>
<td><p></em>pdwDataType: kADT_BOOL</p>
<p><em><em>pbData</em>:<strong>TRUE</strong>または<strong>FALSE</strong></p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(BOOL)</p>
<p>注:場合<em>PrintPSErrors が存在しない場合は、あると見なされます<strong>TRUE</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>Product</strong></p></td>
<td><p><em></em>pdwDataType</em>: kADT_BINARY</p>
<p><em>pbData</em>:<em>製品値</p>
<p><em></em>pcbNeeded</em>: 出力バイナリ データのバイト数</p>
<p>注: 最初のメッセージだけ<em>製品エントリが返されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>プロトコル</strong></p></td>
<td><p><em></em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:ASCII 文字列 (レジストリ形式) で登録されている値を含む protocolOption のプリンターをサポートします。</p>
<p><em><em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (最後の null 文字を含む)</p></td>
</tr>
<tr class="even">
<td><p><strong>PSVersion</strong></p></td>
<td><p><em></em>pdwDataType</em>: kADT_BINARY</p>
<p><em>pbData</em>: <em>PSVersion の値</p>
<p><em></em>pcbNeeded</em>: 出力バイナリ データのバイト数</p>
<p>注: 最初のメッセージだけ<em>PSVersion エントリが返されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SuggestedJobTimeout</strong></p></td>
<td><p><em></em>pdwDataType</em>: kADT_DWORD</p>
<p><em><em>pbData</em>: * SuggestedJobTimeout 値。 それが存在しない場合、PPD から既定で 0 が返されます。</p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><strong>SuggestedWaitTimeout</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p><em></em>pbData</em>: <em>SuggestedWaitTimeout 値。 PPD にない場合は、既定で 300 を返します。</p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>スループット</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p><em></em>pbData</em>:<em>スループット値。 PPD にない場合は、既定で 0 を返します。</p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><strong>TTRasterizer</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: rasterizerOption 値を次のいずれかを含む NULL で終わる ASCII 文字列。</p>
<p>"None"</p>
<p>"Accept68K"</p>
<p>"Type42"</p>
<p>"TrueImage"</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (最後の null 文字を含む)</p>
<p>注: 場合は、* TTRasterizer エントリが存在しない場合、"None"が返されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




