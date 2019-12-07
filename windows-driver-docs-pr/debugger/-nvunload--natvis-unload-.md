---
title: .nvunload (NatVis のアンロード)
description: Nvunload コマンドは、デバッガー環境から NatVis ファイルをアンロードします。
ms.assetid: E63BE2B5-291B-4F78-98FF-C1D7663A184E
keywords:
- . nvunload (NatVis Unload) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .nvunload (NatVis Unload)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cad98e4a17c9203a3cf5a0e1517177a031a522dd
ms.sourcegitcommit: 5a10ea8a98fa4b6f8c43176156530e859a71b10e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74908353"
---
# <a name="nvunload-natvis-unload"></a>.nvunload (NatVis のアンロード)

Nvunload コマンドは、デバッガー環境から NatVis ファイルをアンロードします。

```dbgcmd
.nvunload FileName|ModuleName  
```

*FileName |ModuleName*

アンロードする NatVis ファイル名またはモジュール名を指定します。

**ファイル名**は、アンロードする natvis ファイルの明示的な名前です。 完全修飾パスを使用できます。

**ModuleName**は、デバッグ対象のプロセス内のモジュールの名前です。 名前付きモジュール名のシンボルファイル (PDB) 内に埋め込まれているすべての NatVis ファイルがアンロードされます。

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
