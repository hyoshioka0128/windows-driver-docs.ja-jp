---
title: .nvunload (NatVis アンロード)
description: .Nvunload コマンドでは、デバッガーの環境から NatVis ファイルをアンロードします。
ms.assetid: E63BE2B5-291B-4F78-98FF-C1D7663A184E
keywords:
- .nvunload (NatVis Unload) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .nvunload (NatVis Unload)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00b7e084694d3430bf84e3c8859a0674d4f0ba55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531794"
---
# <a name="nvunload-natvis-unload"></a>.nvunload (NatVis アンロード)


.Nvunload コマンドでは、デバッガーの環境から NatVis ファイルをアンロードします。

```dbgcmd
.nvunload FileName|ModuleName  
```

<span id="_______FileName___ModuleName______"></span><span id="_______filename___modulename______"></span><span id="_______FILENAME___MODULENAME______"></span> *ファイル名 |ModuleName*   
NatVis ファイルの名前またはアンロードするモジュール名を指定します。

**FileName**アンロードに .natvis ファイルの明示的な名前を指定します。 完全修飾パスを使用できます。

**ModuleName**デバッグ中のターゲット プロセスのモジュールの名前を指定します。 名前付きモジュールの名前のシンボル (PDB) ファイル内に埋め込まれたすべての NatVis ファイルは、アンロードされます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。 [.natvis ファイルを使用して C++ のデバッガーの種類のビジュアライザーを書き込み](https://code.msdn.microsoft.com/windowsdesktop/Writing-type-visualizers-2eae77a2)します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**dx (表示 NatVis 式)**](dx--display-visualizer-variables-.md)

 

 






