---
title: .dumpcab (ダンプ ファイル CAB の作成)
description: .Dumpcab コマンドは、現在のダンプ ファイルを含む CAB ファイルを作成します。
ms.assetid: 65ed766f-b049-47b0-90d7-e21d510a35ba
keywords:
- .dumpcab (ダンプ ファイル CAB を作成する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dumpcab (Create Dump File CAB)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 06c2fcc275f203af634eec64ec989f61d3fb82e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336793"
---
# <a name="dumpcab-create-dump-file-cab"></a>.dumpcab (ダンプ ファイル CAB の作成)


**.Dumpcab**コマンドは、現在のダンプ ファイルを含む CAB ファイルを作成します。

```dbgcmd
.dumpcab [-a] CabName 
```

## <a name="span-idddkmetacreatedumpfilecabdbgspanspan-idddkmetacreatedumpfilecabdbgspanparameters"></a><span id="ddk_meta_create_dump_file_cab_dbg"></span><span id="DDK_META_CREATE_DUMP_FILE_CAB_DBG"></span>パラメーター


<span id="_______-a______"></span><span id="_______-A______"></span> **-**   
CAB ファイルに含まれるすべての現在読み込まれているシンボル。 ミニダンプのすべての読み込まれたイメージが含まれますも。 使用[**人生が大好き**](lm--list-loaded-modules-.md)どのシンボルとイメージを読み込むかを決定します。

<span id="_______CabName______"></span><span id="_______cabname______"></span><span id="_______CABNAME______"></span> *CabName*   
拡張子を含む CAB ファイル名。 *CabName*絶対または相対パスを含めることができます。 相対パスは、デバッガーが起動されたディレクトリに対して相対的な。 拡張子 .cab を選択することをお勧めします。

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
<td align="left"><p>クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

クラッシュ ダンプについて詳しくは、次を参照してください。[クラッシュ ダンプ ファイル](crash-dump-files.md)します。

<a name="remarks"></a>コメント
-------

このコマンドは、既にダンプ ファイルをデバッグしている場合にのみ使用できます。

使用する必要がありますをデバッグする場合、ライブのターゲットとダンプを作成するファイルし cab ファイルに配置、 [ **.dump (ダンプ ファイルの作成)** ](-dump--create-dump-file-.md)コマンド。 次に、そのターゲットとしてダンプ ファイルを使用して新しいデバッグ セッションを開始しを使用して、 **.dumpcab**します。

**.Dumpcab**を 1 つの CAB ファイルに複数のダンプ ファイルを格納するコマンドは使用できません。

 

 





