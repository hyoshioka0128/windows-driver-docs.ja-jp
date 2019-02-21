---
title: ~ m (Resume スレッド)
description: ~ M コマンドは、指定したスレッドの実行を再開します。M (メモリの移動) コマンドを使用してこのコマンドを混同しないでください。
ms.assetid: fc4eec45-2a28-4571-abf5-3896b77a52c9
keywords:
- ~ m (Resume スレッド) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~m (Resume Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f783fe1bc23252fbc40d936124711d8b2ccd0d3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536428"
---
# <a name="m-resume-thread"></a>~ m (Resume スレッド)


**~ M**コマンドは、指定したスレッドの実行を再開します。

このコマンドを混同しないでください、 [ **m (メモリの移動)** ](m--move-memory-.md)コマンド。

```dbgcmd
~Thread m 
```

## <a name="span-idddkcmdresumethreaddbgspanspan-idddkcmdresumethreaddbgspanparameters"></a><span id="ddk_cmd_resume_thread_dbg"></span><span id="DDK_CMD_RESUME_THREAD_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
スレッドまたは再開するスレッドを指定します。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

中断の詳細についてはカウントとどのように中断されたスレッドの動作し、中断とスレッドの固定を制御するその他のコマンドの一覧は、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

<a name="remarks"></a>注釈
-------

スレッドは、ユーザー モードでのみ指定できます。 カーネル モードではチルダ (~) は、プロセッサを表します。

使用するたびに、 **~ m**コマンド、スレッドの数を中断する 1 つ減らされます。

 

 





