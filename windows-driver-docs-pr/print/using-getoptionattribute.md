---
title: GetOptionAttribute の使用
description: GetOptionAttribute の使用
ms.assetid: d35f0811-d572-422c-8672-ffd29bf69efa
keywords:
- GetOptionAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23f857b23a017d99b4640668d821dcb5bfd1c4f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379018"
---
# <a name="using-getoptionattribute"></a>GetOptionAttribute の使用





この関数は、PPD 機能のみサポートされます。 特定の属性が使用できない場合**GetOptionAttribute**返します E\_INVALIDARG します。

次の表に、 *pdwDataType*パラメーターの値には、 [ **EATTRIBUTE\_DATATYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff548692)列挙型。

### <a name="output-parameters-for-general-option-attributes"></a>[全般] オプションの属性の出力パラメーター

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>[全般] オプションの属性</th>
<th>出力パラメーター</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DisplayName</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_UNICODE</p>
<p><em>pbData</em>: オプションのキーワード名の翻訳文字列の null で終わる Unicode 文字列</p>
<p><em></em>pcbNeeded</em>: Unicode 文字列のバイト数が指す<em>pbData</em> (null 終端文字を含む)</p>
<p>このオプションの属性が使用できるいずれかのオプションを<strong>EnumOptions</strong> PPD 機能を返すことができます。</p></td>
</tr>
<tr class="even">
<td><p><strong>呼び出し</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_BINARY</p>
<p><em>pbData</em>: オプションの InvocationValue のバイト配列。</p>
<p><em></em>pcbNeeded</em>: によって示されるバイナリ データのバイト数<em>pbData</em></p>
<p>このオプションの属性が使用できるいずれかのオプションを<strong>EnumOptions</strong> PPD 機能を返すことができます。 オプションの InvocationValue が空の場合、関数は設定<em>pdwDataType</em>上記と同じ設定<em> <em>pcbNeeded</em> = 0、および、S_OK を返します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p></em>pdwDataType: kADT_LONG</p>
<p><em><em>pbData</em>: PPD のによって指定された相対順序<em>OrderDependency または * このオプションの NonUIOrderDependency キーワード。 これらのキーワードの最初のパラメーターは、長整数型に変換され、返される実数であることを確認します。</p>
<p><em></em>pcbNeeded</em>: <strong>sizeof</strong>(LONG)</p>
<p>このオプションの属性を持つオプションでのみ使用できますが、 <em>OrderDependency または *、PPD で NonUIOrderDependency エントリと、エントリが optionKeyword を省略できません。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p><em></em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: セクション名を次のいずれかを含む null で終わる ASCII 文字列。"ExitServer"「プロローグ」"DocumentSetup""PageSetup""JCLSetup""AnySetup"。</p>
<p><em></em>pcbNeeded</em>: によって示される、ASCII 文字列のバイト数<em>pbData</em> (null 終端文字を含む)</p>
<p>このオプションの属性を持つオプションでのみ使用できますが、* OrderDependency または *、PPD で NonUIOrderDependency エントリと、エントリが optionKeyword を省略できません。</p></td>
</tr>
</tbody>
</table>

 

### <a name="output-parameters-for-specific-option-attributes"></a>特定のオプションの属性の出力パラメーター

前に説明した一般的なオプションの属性の他の次の表に示すオプションの属性は使用できる場合での制限事項をもできます。 いくつかの属性は他のユーザーがその PPD 機能の特定のオプションでのみ使用できる特定の PPD 機能のすべてのオプションを使用できます。 このような制限事項は、各オプションの属性の一覧表示されます。

機能のオプションの属性は出力パラメーターのキーワード\*InputSlot

**RequiresPageRegion**

\*pdwDataType: kADT\_BOOL

*\*pbData*:**TRUE**場合\*と共に PageRegion 呼び出しコードを送信する必要があります、 \*InputSlot 呼び出しのコードと**FALSE**それ以外の場合。 これは PPD に基づいて\*RequiresPageRegion キーワード。 この入力のスロットのオプションのキーワードを省略した場合**TRUE**のこの属性が返されます。

*\*pcbNeeded*: **sizeof**(BOOL)

このオプションの属性が"InputSlot"PPD の任意のオプションを使用できる機能、ドライバーが生成したオプションを除く"\*UseFormTrayTable"。

\*OutputBin

**OutputOrderReversed**

\*pdwDataType: kADT\_BOOL

*\*pbData*:**TRUE** 、binOption の順序は「リバース」を出力する場合と**FALSE**出力順序が"Normal"の場合。 これは PPD に基づいて\*DefaultOutputOrder と\*PageStackOrder キーワード。

*\*pcbNeeded*: **sizeof**(BOOL)

このオプションの属性が"OutputBin"PPD の任意のオプションを使用できる機能。

\*PageSize

**ImageableArea**

\*pdwDataType: kADT\_RECT

*\*pbData*: PPD の規定に従い、PageSize オプションのイメージ可能領域の境界ボックス\*ImageableArea のキーワードが返されます (Microsoft Windows SDK のドキュメントで定義されている) RECT 構造体である**左**と**下部**、llx と機械的の値を持つメンバーが含まれて**右**と**上部**urx と ury 値がメンバーに含めることが。 すべての値では、ミクロンです。 PPD の llx、され機械的値が切り上げを最も近い整数ミクロン内に変換する前にします。 PPD の urx と ury 値に切り上げられます、最も近い整数ミクロン内に変換する前にします。

*\*pcbNeeded*: **sizeof**(RECT)

このオプションの属性が"PageSize"PPD の任意のオプションを使用可能な"CustomPageSize"オプションを除く、機能します。

**PaperDimension**

\*pdwDataType: kADT\_サイズ

*\*pbData*: PPD の規定に従い、PageSize オプションの物理的なディメンション\*PaperDimension のキーワードが返されます (Windows SDK のドキュメントで定義されている) SIZE 構造体である**cx**メンバー幅の値と持つ**cy**メンバーには高さの値が含まれています。 すべての値では、ミクロンです。

*\*pcbNeeded*: **sizeof**(サイズ)

このオプションの属性が"PageSize"PPD の任意のオプションを使用可能な"CustomPageSize"オプションを除く、機能します。

\*PageSize:CustomPageSize

**HWMargins**

\*pdwDataType: kADT\_RECT

*\*pbData*: PPD のによって指定された 4 つの値\*HWMargins キーワードは (Windows SDK のドキュメントで定義されている) RECT 構造体で返されます。 すべての値では、ミクロンです。

*\*pcbNeeded*: **sizeof**(RECT)

このオプションの属性が"PageSize"PPD の"CustomPageSize"オプションにのみ使用可能な機能です。

**MaxMediaHeight**

*\*pdwDataType*: kADT\_DWORD

*\*pbData*: PPD のによって指定された値\*ミクロン、MaxMediaHeight キーワード。

*\*pcbNeeded*: **sizeof**(DWORD)

このオプションの属性が"PageSize"PPD の"CustomPageSize"オプションにのみ使用可能な機能です。

**MaxMediaWidth**

*\*pdwDataType*: kADT\_DWORD

*\*pbData*: PPD のによって指定された値\*ミクロン、MaxMediaWidth キーワード。

*\*pcbNeeded*: **sizeof**(DWORD)

このオプションの属性が"PageSize"PPD の"CustomPageSize"オプションにのみ使用可能な機能です。

**ParamCustomPageSize**

*\*pdwDataType*: kADT\_CUSTOMSIZEPARAMS

*pbData*: CUSTOMPARAM の配列\_最大の要素、各要素が、 [ **CUSTOMSIZEPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff547337)構造体。 この配列の各要素で PPD の指定された値を格納する\*ParamCustomPageSize キーワードの paramOption エントリ。 「方向」以外 paramOption、ミクロン lMinVal と lMaxVal 値です。 LMinVal と lMaxVal 値は「方向」の範囲で\[0、3\]します。

*\*pcbNeeded*: **sizeof**(CUSTOMSIZEPARAM) \* CUSTOMPARAM\_MAX

このオプションの属性が"PageSize"PPD の"CustomPageSize"オプションにのみ使用可能な機能です。

次の注を参照してください。

\*InstalledMemory

**VMOption**

*\*pdwDataType*: kADT\_DWORD

*\*pbData*: PPD のによって指定された値\*VMOption キーワード、または PPD で指定されていない場合は 0、 \*VMOption キーワードは、このオプションをします。

*\*pcbNeeded*: **sizeof**(DWORD)

このオプションの属性が"InstalledMemory"PPD の任意のオプションを使用できる機能。

**FCacheSize**

*\*pdwDataType*: kADT\_DWORD

*\*pbData*: PPD のによって指定された値\*FCacheSize キーワード、または PPD で指定されていない場合は 0、 \*FCacheSize キーワードは、このオプションをします。

*\*pcbNeeded*: **sizeof**(DWORD)

このオプションの属性が"InstalledMemory"PPD の任意のオプションを使用できる機能。

 

### <a name="note-on-paramcustompagesize"></a>ParamCustomPageSize に関する注意事項

PPD ファイルの元の順序、min、および最大値を取得する方法を示すいくつかのサンプル コードをここでは、"\*ParamCustomPageSize 幅"エントリ。 CUSTOMPARAM\_printoem.h で定義されている幅定数のオフセットを示す、 [ **CUSTOMSIZEPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff547337)幅エントリに関連する情報を格納する構造体。 この構造体は CUSTOMPARAM のいずれかの\_このような構造体の配列を形成する最大 CUSTOMSIZEPARAM 構造体。 Printoem.h ヘッダー CUSTOMPARAM という名前の定数のセットを定義する\_XXX (幅、高さ、WidthOffset、HeightOffset、および印刷の向き) は、この配列内の構造体のオフセットを一覧表示します。

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

 

 




