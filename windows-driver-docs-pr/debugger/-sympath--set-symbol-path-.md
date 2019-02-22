---
title: .sympath (シンボル パスの設定)
description: .Sympath コマンドを設定またはシンボル パスを変更します。 シンボル パスには、デバッガーがシンボル ファイルを検索する場所の場所を指定します。
ms.assetid: 32146871-a59f-4c93-b886-137c5ecf5c99
keywords:
- シンボル パス (.sympath) コマンドを設定します。
- シンボル ファイルとパス、シンボルのパスを設定する (.sympath) コマンド
- .sympath (シンボル パスの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .sympath (Set Symbol Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35abbd135a02d86ef44baab83858a989ec4f3d4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535818"
---
# <a name="sympath-set-symbol-path"></a>.sympath (シンボル パスの設定)


**.Sympath**コマンドを設定またはシンボル パスを変更します。 シンボル パスには、デバッガーがシンボル ファイルを検索する場所の場所を指定します。

```dbgcmd
.sympath[+] [Path [; ...]]
```

## <a name="span-idddkmetasetsymbolpathdbgspanspan-idddkmetasetsymbolpathdbgspanparameters"></a><span id="ddk_meta_set_symbol_path_dbg"></span><span id="DDK_META_SET_SYMBOL_PATH_DBG"></span>パラメーター


<span id="______________"></span> **+**   
指定する新しい場所に追加されます (ではなく置き換える) 前のシンボル検索パス。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *パス*   
完全修飾パスまたは完全修飾パスの一覧。 複数のパスについては、セミコロンで区切ります。 場合*パス*は省略すると、現在のシンボル パスが表示されます。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細とこのパスを変更するには、他の方法では、次を参照してください。[シンボル パス](symbol-path.md)します。

<a name="remarks"></a>注釈
-------

シンボル パスが変更されたときに、新しいシンボル情報は読み込まれません。 使用することができます、 [ **.reload (モジュールの再読み込み)** ](-reload--reload-module-.md)シンボルの再読み込みするコマンド。

 

 





