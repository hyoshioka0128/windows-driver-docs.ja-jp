---
title: .tlist (プロセス Id の一覧)
description: .Tlist コマンドでは、システムで実行されているすべてのプロセスが一覧表示します。
ms.assetid: 44d46b74-5cf1-4384-b468-baec5a87eaed
keywords:
- プロセス Id (.tlist) コマンドを一覧表示します。
- プロセス、プロセス Id の一覧 (.tlist) コマンド
- .tlist (プロセス Id の一覧) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .tlist (List Process IDs)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50a5182dcc140b561ae766d5b462a963e7360ab0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557299"
---
# <a name="tlist-list-process-ids"></a>.tlist (プロセス Id の一覧)


**.Tlist**コマンドは、システムで実行されているすべてのプロセスを一覧表示します。

```dbgcmd
.tlist [Options][FileNamePattern]
```

## <a name="span-idddkmetalistprocessidsdbgspanspan-idddkmetalistprocessidsdbgspanparameters"></a><span id="ddk_meta_list_process_ids_dbg"></span><span id="DDK_META_LIST_PROCESS_IDS_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の数を指定できます。

<span id="-v"></span><span id="-V"></span>**-v**  
詳細情報の表示をによりします。 これには、セッション数、プロセスのユーザー名、およびコマンド ライン プロセスを開始するために使用が含まれます。

<span id="-c"></span><span id="-C"></span>**-c**  
現在のプロセスだけを表示を制限します。

<span id="_______FileNamePattern______"></span><span id="_______filenamepattern______"></span><span id="_______FILENAMEPATTERN______"></span> *FileNamePattern*   
表示するには、ファイル名またはプロセスのファイル名に一致する必要があるパターンを指定します。 ファイルの名前がこのパターンに一致プロセスのみが表示されます。 *FileNamePattern*のさまざまなワイルドカードや; 指定子を含めることができますを参照してください[文字列のワイルドカード構文](string-wildcard-syntax.md)詳細についてはします。 パスではなく、実際のファイル名に対してのみ、この照合が行われます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のメソッドのプロセスを表示するには、次を参照してください。[プロセス ID の検索](finding-the-process-id.md)します。

<a name="remarks"></a>注釈
-------

各プロセス ID が表示されます、 **0n**プレフィックス、PID が 10 進数であることを強調します。

 

 





