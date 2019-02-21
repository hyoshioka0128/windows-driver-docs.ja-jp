---
title: .nvload (NatVis 負荷)
description: .Nvload コマンドは、デバッガーの環境に NatVis ファイルを読み込みます。 視覚エフェクトが読み込まれた後、視覚エフェクトで定義されているデータを表示するために使用されます。
ms.assetid: 9B14B3B4-EA90-426E-8555-0E5B8F63E0A9
keywords:
- .nvload (NatVis 負荷) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .nvload (NatVis Load)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1f4a08aeb8e7676a6759a89726701a6a2f24ae44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552466"
---
# <a name="nvload-natvis-load"></a>.nvload (NatVis 負荷)


.Nvload コマンドは、デバッガーの環境に NatVis ファイルを読み込みます。 視覚エフェクトが読み込まれた後、視覚エフェクトで定義されているデータを表示するために使用されます。

```dbgcmd
.nvload FileName|ModuleName   
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______FileName___ModuleName______"></span><span id="_______filename___modulename______"></span><span id="_______FILENAME___MODULENAME______"></span> *ファイル名 |ModuleName*   
NatVis ファイルの名前または読み込むモジュールの名前を指定します。

**FileName** .natvis ファイルを読み込むの明示的な名前を指定します。 完全修飾パスを使用できます。

**ModuleName**デバッグ中のターゲット プロセスのモジュールの名前を指定します。 使用可能な場合、名前付きモジュールの名前のシンボル (PDB) ファイル内で埋め込まれたすべての .natvis ファイルが読み込まれます。

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

 

 






