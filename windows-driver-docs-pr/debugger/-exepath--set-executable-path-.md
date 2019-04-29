---
title: .exepath (実行可能ファイルのパスの設定)
description: .Exepath コマンドを設定または実行可能ファイルの検索パスが表示されます。
ms.assetid: 09f8c2f6-4df7-4039-bb92-66d42015c3dc
keywords:
- .exepath (実行可能ファイル パスの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .exepath (Set Executable Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1c705f2f67abb356c53a3f846ae6dcdb2a75e05f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334494"
---
# <a name="exepath-set-executable-path"></a>.exepath (実行可能ファイルのパスの設定)


**.Exepath**コマンドを設定または実行可能ファイルの検索パスが表示されます。

```dbgcmd
.exepath[+] [Directory [; ...]] 
```

## <a name="span-idddkmetasetexecutablepathdbgspanspan-idddkmetasetexecutablepathdbgspanparameters"></a><span id="ddk_meta_set_executable_path_dbg"></span><span id="DDK_META_SET_EXECUTABLE_PATH_DBG"></span>パラメーター


<span id="______________"></span> **+**   
デバッガーが、パスに置き換える) ではなく前の実行可能ファイルの検索パスに新しいディレクトリを追加する必要がありますを指定します。

<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span> *ディレクトリ*   
検索パスに配置する 1 つまたは複数のディレクトリを指定します。 指定しない場合*ディレクトリ*、現在のパスが表示されます。 複数のディレクトリをセミコロンで区切ることができます。

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

 

 

 





