---
title: フォントの置き換え
description: フォントの置き換え
ms.assetid: a67f42cd-1c10-46b7-8d24-0cb26339bc92
keywords:
- WDK Unidrv、代替プリンターのフォントの記述
- 代替フォント表 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4090f8ed6b1bfa1c8bb0c8659ef9a3e3559b6536
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552755"
---
# <a name="font-substitution"></a>フォントの置き換え





ハードウェアに常駐またはカートリッジのフォントを提供するプリンターをフォント代替表を指定できます。 、、フォント代替表を提供し、ダウンロードする必要がある TrueType フォントの代わりに使用できるハードウェアに常駐またはカートリッジのフォントを指定します。 Unidrv では、このような TrueType フォントでテキストを受け取る、フォントのハードウェアに常駐置換フォント代替表が含まれているをまず確認します。 Unidrv が代替のフォントを検索し、(文字セット、重量、斜体、印刷の向きや) フォント メトリックは互換性がある場合は、常駐のフォントが使用されます。

既定のフォント代替表を作成するには、一連を使用して\*TTFS エントリ。 各エントリの形式です。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p>
* TTFS:<em>FontName</em> { *TTFontName:&quot;<em>TTFontNameString</em>&quot; *DevFontName:&quot;<em>DeviceFontNameString</em>&quot; <strong>}</strong></td>
</tr>
</tbody>
</table>

 

場所*FontName*は、エントリ名を指定する記号*TTFontNameString*が置き換えられる TrueType フォントを識別するテキスト文字列と*DeviceFontNameString*は使用するハードウェアに常駐またはカートリッジのフォントを識別するテキスト文字列。 テーブルの例を次に示します。

```cpp
*TTFS: Arial
{
    *TTFontName: "Arial"
    *DevFontName "Arial"
}
*TTFS: TNR
{
    *TTFontName: "Times New Roman"
    *DevFontName: "Times New Roman"
}
*TTFS: CurrierNew 
{
    *TTFontName:  "Courier New"
    *DevFontName: "Courier New"
}
```

重複がある場合\*が同じ TTFS エントリ*FontName*パーサーによって読み取られた最後のエントリの値には、前よりも優先されます。

指定した代替表では、既定のテーブルは Unidrv 代替文字列を変更するユーザーを許可するためです。

すべて\*TTFS エントリは、GPD ファイルのルート レベルである必要があります (つまり、中かっこ内にありません)。

フォントの置き換えが既定で有効になっているかどうかを制御するには、使用、 \*TTFSEnabled でしょうか。 エントリ。 このエントリの形式です。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* TTFSEnabled:<em>BooleanValue</em></p></td>
</tr>
</tbody>
</table>

 

場所*BooleanValue*は**TRUE**または**FALSE**します。 場合*BooleanValue*は**TRUE**Unidrv にフォントの置き換えができるようにします。 場合*BooleanValue*は**FALSE**、含めない場合、または、 \*TTFSEnabled でしょうか。 GPD ファイルのエントリ、Unidrv を無効にフォントの置き換えまで、ユーザーが有効になっています。

\*TTFSEnable でしょうか。 エントリが再配置すること、が\*TTFS エントリではありません。 (再配置可能なエントリについては、配置中に確認\*スイッチ、\*の場合も、および\*Default ステートメント)。

### <a name="default-truetype-font-substitutions"></a>既定の TrueType フォントの置換

TrueType フォント置換の既定のテーブルは、ttfsub.gpd という名前のファイルで提供されます。 これを使用する、GPD ファイルのルート レベルで、次のエントリを追加します (つまり、中かっこ内ではなく)。

```cpp
*Include: "ttfsub.gpd"
```

さらに、このファイルをインストールする必要があります。 詳細については、次を参照してください。[プリンター INF ファイルのインストール セクション](printer-inf-file-install-sections.md)します。

 

 




