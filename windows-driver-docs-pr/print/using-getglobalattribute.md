---
title: GetGlobalAttribute の使用
description: GetGlobalAttribute の使用
ms.assetid: 0e23ecba-7d89-44f5-b6a7-7d6be9a56765
keywords:
- GetGlobalAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19a960a52b2b6221492a4280eb1f6b04004d45dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843615"
---
# <a name="using-getglobalattribute"></a>GetGlobalAttribute の使用





グローバル属性のすべての名前は、 *PostScript プリンターの説明ファイル形式の仕様である version 4.3*で定義されているキーワード名と同じです。 これらのセマンティクスについては、この仕様を参照してください。 (このリソースは、一部の言語および国では使用できません。)

次の表では、 *pdwDataType*パラメーターは、 [**EATTRIBUTE\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ne-printoem-_eattribute_datatype)列挙型の値を受け取ります。

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
<td><p><strong>センター登録済み</strong></p></td>
<td><p><em>pdwDataType: kADT_BOOL</p>
<p>pbData</em>: <strong>TRUE</strong>または<strong>FALSE</strong></p>
<p><em><em>Pcbneeded 必要</em>: <strong>sizeof</strong>(BOOL)</p></td>
</tr>
<tr class="even">
<td><p><strong>ColorDevice</strong></p></td>
<td><p></em>pdwDataType: kADT_BOOL</p>
<p><em><em>Pbdata</em>: <strong>TRUE</strong>または<strong>FALSE</strong></p>
<p>pcbNeeded な</em>: <strong>sizeof</strong>(BOOL)</p></td>
</tr>
<tr class="odd">
<td><p><strong>補助</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>Pbdata</em>: プリンターがサポートする extensionoption の登録値を含む ASCII 文字列 (MULTI_SZ 形式)。</p>
<p>pcbNeeded な</em>: <em>Pdata</em>が指す ASCII 文字列のバイト数 (最後の null 文字を含む)</p>
<p>注: "<em>FileSystem: True" は、 <strong></em>拡張機能</strong>に "FileSystem" オプションが含まれているかのように扱われます。 "FileSystem: False" は、<em>の拡張機能に "FileSystem" オプションがないかのように扱われます。</p></td>
</tr>
<tr class="even">
<td><p><strong>FileVersion</strong></p></td>
<td><p>pdwDataType</em>: kADT_DWORD</p>
<p><em><em>Pbdata</em>: 上位ワードにメジャーバージョン番号が含まれ、下位ワードにマイナーバージョン番号が含まれている DWORD。</p>
<p>pcbNeeded な</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>FreeVM</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p>pbData</em>: <em>FreeVM の値</p>
<p>pcbNeeded な</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><strong>LandscapeOrientation</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>Pbdata</em>: "Plus90" または "Minus90" のいずれかの NULL で終わる ASCII 文字列。</p>
<p>pcbNeeded な</em>: <em>Pdata</em>が指す ASCII 文字列のバイト数 (最後の null 文字を含む)</p>
<p>注: "Minus90" は、PPD に "<em>LandscapeOrientation: Minus90" が含まれている場合にのみ返されます。 それ以外の場合は、"Plus90" が返されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>言語のエンコード</strong></p></td>
<td><p>pdwDataType</em>: kADT_ASCII</p>
<p><em>Pbdata</em>: 次のいずれかの encodingOption 値を含む NULL で終わる ASCII 文字列。</p>
<p>"ISOLatin1"</p>
<p>対応</p>
<p>"JIS83-RKSJ"</p>
<p>存在</p>
<p><em><em>Pcbneeded</em>: <em>PBDATA</em>が指す ASCII 文字列のバイト数 (最後の null 文字を含む)</p>
<p>注意</p>
<p>"WindowsANSI" は、"ISOLatin1" と同じように扱われます。 その他の encodingOption 値はサポートされていません。</p>
<p>\* 言語エンコードが指定されていない場合、* 言語バージョンは戻り値を推測するために使用されます。</p></td>
</tr>
<tr class="even">
<td><p><strong>LanguageLevel</strong></p></td>
<td><p>pdwDataType</em>: kADT_DWORD</p>
<p><em><em>Pbdata</em>: プリンターでサポートされている PostScript 言語レベル</p>
<p>pcbNeeded な</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>ニックネーム</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_UNICODE</p>
<p><em>Pbdata</em>: NULL で終わる、PPD の * 短いニックネームの値 (* 短いニックネームが存在する場合)、または * 短いニックネームがない場合は * ニックネーム値。</p>
<p>pcbNeeded な</em>: <em>Pbdata</em>が指す Unicode 文字列のバイト数 (最後の null 文字を含む)</p></td>
</tr>
<tr class="even">
<td><p><strong>PPD-Adobe</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p>pbData</em>: 上位ワードにメジャーバージョン番号が含まれ、下位ワードにマイナーバージョン番号が含まれている DWORD。</p>
<p><em><em>Pcbneeded 必要</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>PrintPSErrors</strong></p></td>
<td><p></em>pdwDataType: kADT_BOOL</p>
<p><em><em>Pbdata</em>: <strong>TRUE</strong>または<strong>FALSE</strong></p>
<p>pcbNeeded な</em>: <strong>sizeof</strong>(BOOL)</p>
<p>注: <em>PrintPSErrors が存在しない場合は、 <strong>TRUE</strong>であると見なされます。</p></td>
</tr>
<tr class="even">
<td><p><strong>製品</strong></p></td>
<td><p>pdwDataType</em>: kADT_BINARY</p>
<p><em>Pbdata</em>: <em>製品の値</p>
<p>pcbNeeded な</em>: 出力バイナリデータのバイト数</p>
<p>注: 最初の <em>製品エントリのみが返されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>プロトコル</strong></p></td>
<td><p>pdwDataType</em>: kADT_ASCII</p>
<p><em>Pbdata</em>: プリンターがサポートする protocolOption の登録値を含む ASCII 文字列 (MULTI_SZ 形式)。</p>
<p><em><em>Pcbneeded</em>: <em>PBDATA</em>が指す ASCII 文字列のバイト数 (最後の null 文字を含む)</p></td>
</tr>
<tr class="even">
<td><p><strong>PSVersion</strong></p></td>
<td><p>pdwDataType</em>: kADT_BINARY</p>
<p><em>Pbdata</em>: <em>psversion の値</p>
<p>pcbNeeded な</em>: 出力バイナリデータのバイト数</p>
<p>注: 最初の <em>PSVersion エントリのみが返されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SuggestedJobTimeout</strong></p></td>
<td><p>pdwDataType</em>: kADT_DWORD</p>
<p><em><em>Pbdata</em>: * SuggestedJobTimeout 値。 この値が PPD に存在しない場合、は既定で0を返します。</p>
<p>pcbNeeded な</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><strong>SuggestedWaitTimeout</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p>pbData</em>: <em>SuggestedWaitTimeout 値。 この値が PPD に存在しない場合、は既定で300を返します。</p>
<p>pcbNeeded な</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="odd">
<td><p><strong>処理</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_DWORD</p>
<p>pbData</em>: <em>スループット値。 この値が PPD に存在しない場合、は既定で0を返します。</p>
<p>pcbNeeded な</em>: <strong>sizeof</strong>(DWORD)</p></td>
</tr>
<tr class="even">
<td><p><strong>TTRasterizer</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>Pbdata</em>: 次のいずれかの rasterizerOption 値を含む NULL で終わる ASCII 文字列。</p>
<p>存在</p>
<p>"Accept68K"</p>
<p>"Type42"</p>
<p>"TrueImage"</p>
<p>pcbNeeded な</em>: <em>Pdata</em>が指す ASCII 文字列のバイト数 (最後の null 文字を含む)</p>
<p>注: * TTRasterizer エントリが存在しない場合は、"None" が返されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




