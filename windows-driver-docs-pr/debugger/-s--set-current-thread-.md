---
title: ~s (現在のスレッドの設定)
description: ~ S コマンドを設定または現在のスレッド数が表示されます。
ms.assetid: 689d578b-8d31-4049-a374-19ae94d452a9
keywords:
- ~ s (現在のスレッドのセット) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~s (Set Current Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 114768f905bef5a601b4883fc72df1160e8ef34c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570679"
---
# <a name="s-set-current-thread"></a>~s (現在のスレッドの設定)


**~ S**コマンドを設定または現在のスレッド数が表示されます。

ユーザー モードで **~ s**現在のスレッドを設定します。 このコマンドの混同を混同しないでください、 [ **~ s (変更の現在のプロセッサ)** ](-s--change-current-processor-.md) (これは、カーネル モードでのみ機能します) のコマンドを[ **| s (設定現在のプロセス)**](-s--set-current-process-.md)コマンド、 [ **| |s (現在のシステムの設定)** ](--s--set-current-system-.md)コマンド、または[ **s (メモリの検索)** ](s--search-memory-.md)コマンド。

```dbgcmd
~Thread s 
~ s 
```

## <a name="span-idddkcmdsetcurrentthreaddbgspanspan-idddkcmdsetcurrentthreaddbgspanparameters"></a><span id="ddk_cmd_set_current_thread_dbg"></span><span id="DDK_CMD_SET_CURRENT_THREAD_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
設定または表示するスレッドを指定します。 構文の詳細については、[スレッド構文](thread-syntax.md)を参照してください。

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
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

表示するためのプロセスとスレッドを制御するには、他の方法と詳細については、[を制御するプロセスとスレッド](controlling-processes-and-threads.md)を参照してください。

<a name="remarks"></a>コメント
-------

スレッドは、ユーザー モードでのみ指定できます。 カーネル モードではチルダ (~) は、プロセッサを表します。

使用する場合、 **~ s**構文、デバッガーには、現在のスレッドに関する情報が表示されます。

このコマンドでは、現在のシステム、プロセス、およびスレッドの現在の命令も逆アセンブルします。

 

 





