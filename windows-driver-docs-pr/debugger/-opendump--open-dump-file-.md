---
title: .opendump (開いているダンプ ファイル)
description: .Opendump コマンドでは、デバッグ ダンプ ファイルを開きます。
ms.assetid: 751af9ea-be7e-4aef-a6f6-fc99e3b3a56e
keywords:
- .opendump (開いているダンプ ファイル) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .opendump (Open Dump File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 820a38241bfc83ea1a8929132da3298cdd77eeb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552348"
---
# <a name="opendump-open-dump-file"></a>.opendump (開いているダンプ ファイル)


**.Opendump**コマンドは、デバッグ ダンプ ファイルを開きます。

```dbgcmd
.opendump DumpFile 
.opendump /c "DumpFileInArchive" [CabFile] 
```

## <a name="span-idddkmetaopendumpfiledbgspanspan-idddkmetaopendumpfiledbgspanparameters"></a><span id="ddk_meta_open_dump_file_dbg"></span><span id="DDK_META_OPEN_DUMP_FILE_DBG"></span>パラメーター


<span id="_______DumpFile______"></span><span id="_______dumpfile______"></span><span id="_______DUMPFILE______"></span> *ダンプ ファイル*   
開く、ダンプ ファイルの名前を指定します。 *DumpFile* (.dmp 通常または .mdmp) ファイル名拡張子を含める必要があり、絶対または相対パスを含めることができます。 相対パスで、デバッガーを起動しているディレクトリに対して相対的な。

<span id="________c__DumpFileInArchive_"></span><span id="________c__dumpfileinarchive_"></span><span id="________C__DUMPFILEINARCHIVE_"></span> **/c** **"**<em>DumpFileInArchive</em>**"**  
デバッグ ダンプ ファイルの名前を指定します。 このダンプ ファイルをアーカイブに含める必要があるファイルを*キャビネット*を指定します。 囲む必要があります、 *DumpFileInArchive*引用符で囲まれたファイルです。

<span id="_______CabFile______"></span><span id="_______cabfile______"></span><span id="_______CABFILE______"></span> *キャビネット*   
開くアーカイブ ファイルの名前を指定します。 *キャビネット*(通常は .cab) ファイル名拡張子を含める必要があり、絶対または相対パスを含めることができます。 相対パスで、デバッガーを起動しているディレクトリに対して相対的な。 使用する場合、 **/c**アーカイブでダンプ ファイルを指定するスイッチは省略する*キャビネット*デバッガーは、最近開いたアーカイブ ファイルを再利用されます。

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
<td align="left"><p>クラッシュ ダンプのみ (ただし、このコマンドを使用するには、他のセッションが実行されている場合)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

使用した後、 **.opendump**コマンドを使用する必要があります、 [ **g (移動)** ](g--go-.md)ダンプ ファイルの読み込みが完了するコマンド。

使用する必要があります (CAB ファイル) などのアーカイブ ファイルを開くとき、 **/c**スイッチします。 このスイッチを使用しないし、アーカイブを指定する*DumpFile*デバッガーがこのアーカイブ内 .mdmp または .dmp ファイル名拡張子を持つ最初のファイルを開きます。

使用することができます **.opendump**場合でも、デバッグ セッションは既に進行中です。 この機能では、同時に 1 つ以上のクラッシュ ダンプをデバッグすることができます。 複数のターゲットのセッションを制御する方法の詳細については、次を参照してください。[複数のターゲットのデバッグ](debugging-multiple-targets.md)します。

 
**注**  コマンドのデバッグの種類ごとに異なる方法で動作しているために、ライブのターゲットと、ダンプ ターゲットをデバッグするときに、問題があります。 たとえば、使用する場合、 **g (移動)** コマンドの場合は、現在のシステムは、ダンプ ファイル、デバッガーが実行を開始がすることはできません戻るデバッガーに割り込む、break コマンドが認識されないため、ダンプ ファイルのデバッグの有効とします。
 





