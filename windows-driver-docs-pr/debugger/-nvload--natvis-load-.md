---
title: .nvload (NatVis の読み込み)
description: Nvload コマンドは、NatVis ファイルをデバッガー環境に読み込みます。 視覚エフェクトが読み込まれると、視覚エフェクトで定義されたデータを表示するために使用されます。
ms.assetid: 9B14B3B4-EA90-426E-8555-0E5B8F63E0A9
keywords:
- . nvload (NatVis Load) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .nvload (NatVis Load)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cd188d2e6a38d445cab25b4075cec62dfb088444
ms.sourcegitcommit: 5a10ea8a98fa4b6f8c43176156530e859a71b10e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74908349"
---
# <a name="nvload-natvis-load"></a>.nvload (NatVis の読み込み)


Nvload コマンドは、NatVis ファイルをデバッガー環境に読み込みます。 視覚エフェクトが読み込まれると、視覚エフェクトで定義されたデータを表示するために使用されます。

```dbgcmd
.nvload FileName|ModuleName
```

## <a name="parameters"></a>パラメーター

*FileName |ModuleName*

読み込む NatVis ファイル名またはモジュール名を指定します。

**ファイル名**は、読み込む natvis ファイルの明示的な名前です。 完全修飾パスを使用できます。

**ModuleName**は、デバッグ対象のプロセス内のモジュールの名前です。 名前付きモジュール名のシンボルファイル (PDB) に埋め込まれているすべての NatVis ファイルが読み込まれます (使用可能なファイルがある場合)。

## <a name="environment"></a>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

## <a name="additional-information"></a>追加情報

詳細については、「[ネイティブオブジェクトのカスタムビューを作成する](https://docs.microsoft.com/visualstudio/debugger/create-custom-views-of-native-objects?view=vs-2015)」を参照してください。

## <a name="see-also"></a>関連項目

[**dx (Display NatVis Expression)** ](dx--display-visualizer-variables-.md)
