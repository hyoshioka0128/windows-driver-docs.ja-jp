---
title: lsf、lsf- (ソース ファイルの読み込みまたはアンロード)
description: Lsf と lsf コマンドの読み込みまたはソース ファイルをアンロードします。
ms.assetid: e788a778-e331-4b7b-8aad-072b3d08442b
keywords:
- lsf - (ロードまたはアンロード ソース ファイル) の Windows デバッグ lsf
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lsf, lsf- (Load or Unload Source File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7715ea4d9f0f9a2db7d8c1031b5974a735203b4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572055"
---
# <a name="lsf-lsf--load-or-unload-source-file"></a>lsf、lsf- (ソース ファイルの読み込みまたはアンロード)


**Lsf**と**lsf-** コマンドの読み込みまたはソース ファイルをアンロードします。

```dbgcmd
lsf Filename 
lsf- Filename
```

## <a name="span-idddkcmdloadorunloadsourcefiledbgspanspan-idddkcmdloadorunloadsourcefiledbgspanparameters"></a><span id="ddk_cmd_load_or_unload_source_file_dbg"></span><span id="DDK_CMD_LOAD_OR_UNLOAD_SOURCE_FILE_DBG"></span>パラメーター


<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *ファイル名*   
読み込みまたはアンロードするファイルを指定します。 このファイルは、デバッガーがから開かれたディレクトリにない場合は、絶対または相対パスを含める必要があります。 ファイル名は、Microsoft Windows ファイル名前付け規則に従う必要があります。

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

 

<a name="remarks"></a>コメント
-------

**Lsf**コマンドは、ソース ファイルを読み込みます。

**Lsf-** コマンドは、ソース ファイルをアンロードします。 以前に読み込まれているファイルのアンロードにこのコマンドを使用する**lsf**またはソース ファイルを自動的に読み込まれます。 使用することはできません**lsf -** WinDbg から読み込まれたファイルをアンロードする[ファイル |ソース ファイルを開く](file---open-source-file.md)コマンドまたは WinDbg ワークスペースが読み込まれているファイル。

CDB または KD、内のソース ファイルを表示することができます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。 ソース ファイルが新規として読み込まれる、WinDbg で[ソース windows](source-window.md)します。

ソース ファイル、ソース パス、およびその他のソース ファイルを読み込む方法の詳細については、[ソース パス](source-path.md)を参照してください。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**%.*ls は、lsa (一覧のソース行)**](ls--lsa--list-source-lines-.md)

[**lsc (現在のソースの一覧)**](lsc--list-current-source-.md)

 

 






