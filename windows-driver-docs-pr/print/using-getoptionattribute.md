---
title: GetOptionAttribute の使用
description: GetOptionAttribute の使用
ms.assetid: d35f0811-d572-422c-8672-ffd29bf69efa
keywords:
- GetOptionAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1db41a468e2ba0a3aa2dc972ace848c4e1e304cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843613"
---
# <a name="using-getoptionattribute"></a>GetOptionAttribute の使用





この関数は、PPD 機能に対してのみサポートされています。 特定の属性が使用できない場合、 **GetOptionAttribute**は、E\_invalidarg を返します。

次の表では、 *pdwDataType*パラメーターは、 [**EATTRIBUTE\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ne-printoem-_eattribute_datatype)列挙型の値を受け取ります。

### <a name="output-parameters-for-general-option-attributes"></a>全般オプション属性の出力パラメーター

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>General オプション属性</th>
<th>出力パラメーター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DisplayName</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_UNICODE</p>
<p><em>Pbdata</em>: オプションキーワード名の翻訳文字列の null で終わる Unicode 文字列</p>
<p>pcbNeeded な</em>: <em>Pbdata</em>が指す Unicode 文字列のバイト数 (null 終端文字を含む)</p>
<p>このオプション属性は、 <strong>EnumOptions</strong>が PPD 機能で返すことができる任意のオプションで使用できます。</p></td>
</tr>
<tr class="even">
<td><p><strong>出せる</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_BINARY</p>
<p><em>Pbdata</em>: オプションの InvocationValue のバイト配列。</p>
<p>pcbNeeded な</em>: <em>Pbdata</em>が指すバイナリデータのバイト数</p>
<p>このオプション属性は、 <strong>EnumOptions</strong>が PPD 機能で返すことができる任意のオプションで使用できます。 オプションの InvocationValue が空の場合、関数は<em>pdwDataType</em>を上記のように設定し、<em><em>pcbneeded</em> = 0 を設定してから S_OK を返します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p></em>pdwDataType: kADT_LONG</p>
<p><em>の<em>Pdata</em>: このオプションに対して、PPD の <em>orderdependency または * NonUIOrderDependency キーワードによって指定された相対順序。 これらのキーワードの最初のパラメーターは、LONG に変換されて返される実数であることに注意してください。</p>
<p>pcbNeeded な</em>: <strong>sizeof</strong>(LONG)</p>
<p>このオプション属性は、PPD に <em>OrderDependency または * NonUIOrderDependency エントリを持つオプションに対してのみ使用できます。エントリは optionKeyword を省略しません。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p>pdwDataType</em>: kADT_ASCII</p>
<p><em>Pbdata</em>: "exitserver" "プロローグ" "documentsetup" "PageSetup" "jclsetup" "anysetup" というセクション名のいずれかを含む null で終わる ASCII 文字列。</p>
<p>pcbNeeded な</em>: <em>Pdata</em>が指す ASCII 文字列のバイト数 (null 終端文字を含む)</p>
<p>このオプション属性は、PPD に * OrderDependency または * NonUIOrderDependency エントリを持つオプションに対してのみ使用できます。また、このエントリは optionKeyword を省略しません。</p></td>
</tr>
</tbody>
</table>

 

### <a name="output-parameters-for-specific-option-attributes"></a>特定のオプション属性の出力パラメーター

前に説明した一般的なオプション属性に加えて、次の表に示すオプション属性には、使用可能な場合に制限があります。 一部の属性は特定の PPD 機能のすべてのオプションで使用できますが、その他の属性は、その PPD 機能の特定のオプションでのみ使用できます。 このような制限事項については、各オプション属性に記載されています。

機能オプション属性の出力パラメーターキーワード \*InputSlot

**RequiresPageRegion**

\*pdwDataType: kADT\_BOOL

*\*pbData*: \*inputslot 呼び出しコードと共に PageRegion の呼び出しコードを送信する必要がある場合 \*は**TRUE** 、それ以外の場合は**FALSE** 。 これは、PPD の \*RequiresPageRegion キーワードに基づいています。 この入力スロットオプションでキーワードが省略されている場合は、この属性に対して**TRUE**が返されます。

*\*pcbNeeded 必要*: **sizeof**(BOOL)

このオプション属性は、ドライバーによって生成されるオプション "\*UseFormTrayTable" を除き、"InputSlot" の PPD 機能の任意のオプションで使用できます。

\*OutputBin

**OutputOrderReversed**

\*pdwDataType: kADT\_BOOL

*\*pbData*: binoption の出力順序が "Reverse" の場合は**TRUE** 、出力順序が "Normal" の場合は**FALSE** 。 これは、PPD の \*DefaultOutputOrder および \*PageStackOrder キーワードに基づいています。

*\*pcbNeeded 必要*: **sizeof**(BOOL)

このオプション属性は、"OutputBin" の PPD 機能の任意のオプションで使用できます。

\*PageSize

**ImageableArea**

\*pdwDataType: kADT\_RECT

*pbData の\** : PageSize オプションのイメージ可能領域の境界ボックスは、PPD の \*ImageableArea キーワードによって指定されていますが、(Microsoft Windows SDK のドキュメントで定義されて**いる)** **RECT 構造体で返されます。下**のメンバーには llx と l の値が含まれ、 **right**メンバーと**top**メンバーには urx 値と ury 値が含まれています。 すべての値はミクロンにあります。 PPD の llx と l の値は、1ミクロンに変換される前に、最も近い整数に切り上げられます。 PPD の urx と ury の値は、1ミクロンに変換される前に、最も近い整数に丸められます。

*\*pcbNeeded 必要*: **sizeof**(RECT)

このオプション属性は、"PageSize" PPD 機能のオプション ("CustomPageSize" オプションを除く) で使用できます。

**用紙ディメンション**

\*pdwDataType: kADT\_SIZE

*\*の Pdata*: PPD の \*pagedimension キーワードで指定されている PageSize オプションの物理次元は、サイズ構造 (Windows SDK ドキュメントで定義されています) ( **cx**メンバーに幅の値が含まれている) で返されます。および**cy**メンバーに高さの値が含まれている。 すべての値はミクロンにあります。

*\*pcbNeeded 必要*: **sizeof**(サイズ)

このオプション属性は、"PageSize" PPD 機能の任意のオプションで使用できます。ただし、"CustomPageSize" オプションは除きます。

\*PageSize: CustomPageSize

**HWMargins**

\*pdwDataType: kADT\_RECT

*\*pbData*: PPD の \*HWMargins キーワードによって指定された4つの値が、(Windows SDK のドキュメントで定義されている) RECT 構造体で返されます。 すべての値はミクロンにあります。

*\*pcbNeeded 必要*: **sizeof**(RECT)

このオプション属性は、"PageSize" PPD 機能の "CustomPageSize" オプションでのみ使用できます。

**MaxMediaHeight**

*\*pdwDataType*: KADT\_DWORD

*\*pbData*: PPD の \*MaxMediaHeight キーワードによって指定された値 (ミクロン単位)。

*\*pcbNeeded 必要*: **sizeof**(DWORD)

このオプション属性は、"PageSize" PPD 機能の "CustomPageSize" オプションでのみ使用できます。

**MaxMediaWidth**

*\*pdwDataType*: KADT\_DWORD

*\*pbData*: PPD の \*MaxMediaWidth キーワードによって指定された値 (ミクロン単位)。

*\*pcbNeeded 必要*: **sizeof**(DWORD)

このオプション属性は、"PageSize" PPD 機能の "CustomPageSize" オプションでのみ使用できます。

**ParamCustomPageSize**

*\*pdwDataType*: KADT\_CUSTOMSIZEPARAMS

*Pbdata*: customparam\_MAX 要素の配列。各要素は[**customsizeparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_customsizeparam)構造体です。 この配列の各要素は、PPD の \*ParamCustomPageSize キーワードの paramOption エントリに指定された値を格納します。 ParamOption が "Orientation" 以外の場合、lMinVal と Lminval の値はミクロンにあります。 "Orientation" の場合、lMinVal と Lminval の値は \[0, 3\]の範囲内です。

*\*pcbNeeded*: **sizeof**(customsizeparam) \* customparam\_MAX

このオプション属性は、"PageSize" PPD 機能の "CustomPageSize" オプションでのみ使用できます。

次の注意事項を参照してください。

\*のメモリ不足

**VMOption 場合**

*\*pdwDataType*: KADT\_DWORD

*\*pbData*: ppd の \*vmoption キーワードによって指定された値。または、ppd でこのオプションに対して \*vmoption キーワードが指定されていない場合は0です。

*\*pcbNeeded 必要*: **sizeof**(DWORD)

このオプション属性は、"使用可能なメモリ" の PPD 機能の任意のオプションで使用できます。

**FCacheSize**

*\*pdwDataType*: KADT\_DWORD

*\*pbData*: ppd の \*fcachesize キーワードによって指定された値。または、ppd でこのオプションに \*fcachesize キーワードが指定されていない場合は0です。

*\*pcbNeeded 必要*: **sizeof**(DWORD)

このオプション属性は、"使用可能なメモリ" の PPD 機能の任意のオプションで使用できます。

 

### <a name="note-on-paramcustompagesize"></a>ParamCustomPageSize に関する注意事項

ここでは、"\*ParamCustomPageSize Width" エントリの PPD ファイルの元の順序、最小値、および最大値を取得する方法を示すサンプルコードを示します。 CUSTOMPARAM\_WIDTH 定数は、printoem .h に定義されており、Width エントリに関連する情報を含む[**Customsizeparam**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_customsizeparam)構造体のオフセットを示します。 この構造体は、このような構造体の配列を形成する CUSTOMPARAM\_MAX CUSTOMSIZEPARAM 構造体の1つです。 Printoem .h ヘッダーは、この配列内の構造体のオフセット (Width、Height、WidthOffset、HeightOffset、Orientation) を一覧表示する CUSTOMPARAM\_XXX という名前の一連の定数を定義します。

```cpp
PCUSTOMSIZEPARAM  pCSParam;

pCSParam = (PCUSTOMSIZEPARAM)pbData + CUSTOMPARAM_WIDTH;

order = pCSParam->dwOrder;
// Convert lMinVal and lMaxVal from microns to points.
//   To convert microns to inches, divide by 25400.
//   To convert inches to points, multiply by 72.
min = pCSParam->lMinVal / 25400.0 * 72.0;
max = pCSParam->lMaxVal / 25400.0 * 72.0;
```

 

 




