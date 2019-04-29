---
title: .ignore_missing_pages ("ページが見つからない" エラーの非表示)
description: .Ignore_missing_pages コマンドは、ページが不足しているがあるカーネル メモリ ダンプとエラー メッセージを抑制します。
ms.assetid: 74f4944e-6f0b-4541-b32f-a2da58df7f03
keywords:
- 不足しているページのエラー (.ignore_missing_pages) コマンドを非表示します。
- .ignore_missing_pages (非表示のページ エラーのない) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .ignore_missing_pages (Suppress Missing Page Errors)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ef9064462f24c7e48d6bf16bbdf9bbb9aad2488
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336468"
---
# <a name="ignoremissingpages-suppress-missing-page-errors"></a>.ignore\_不足している\_ページ (不足しているページ エラーの抑制)


**.Ignore\_不足している\_ページ**落丁があるカーネル メモリ ダンプするときに、コマンドがエラー メッセージを抑制します。

```dbgcmd
.ignore_missing_pages 0
.ignore_missing_pages 1
.ignore_missing_pages 
```

## <a name="span-idddkmetasuppressmissingpageerrorsdbgspanspan-idddkmetasuppressmissingpageerrorsdbgspanparameters"></a><span id="ddk_meta_suppress_missing_page_errors_dbg"></span><span id="DDK_META_SUPPRESS_MISSING_PAGE_ERRORS_DBG"></span>パラメーター


<span id="_______0______"></span> **0**   
カーネル メモリ ダンプのデバッグ中に不足しているすべてのページ エラーが表示されます。 これは、デバッガーの既定の動作です。

<span id="_______1"></span> **1**  
カーネル メモリ ダンプのデバッグ中にページ エラーが不足しているの表示をしません。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モードのみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ダンプ ファイルのデバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

これらをデバッグする方法についての詳細については、ダンプ ファイルを参照してください[カーネル メモリ ダンプ](kernel-memory-dump.md)します。

<a name="remarks"></a>注釈
-------

パラメーターを指定せず **.ignore\_不足している\_ページ**この設定の現在の状態が表示されます。

 

 





