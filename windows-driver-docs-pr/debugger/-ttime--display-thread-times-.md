---
title: .ttime (スレッドの表示時間)
description: .Ttime コマンドでは、スレッドの実行時間が表示されます。
ms.assetid: ff48310f-3eb9-4112-b5ab-b7c16878ac8f
keywords:
- .ttime (スレッドの表示時間) の Windows デバッグ
ms.date: 08/01/2018
topic_type:
- apiref
api_name:
- .ttime (Display Thread Times)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 49fd367035c7fb38f99c1c30782701d211fd0f36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552536"
---
# <a name="ttime-display-thread-times"></a>.ttime (スレッドの表示時間)


**.Ttime**コマンドは、スレッドの実行中の時間を表示します。

```dbgcmd
.ttime 
```

## <span id="ddk_meta_display_thread_times_dbg"></span><span id="DDK_META_DISPLAY_THREAD_TIMES_DBG"></span>


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
<td align="left"><p>x86 のみ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このコマンドは、ユーザー モードでのみ機能します。 カーネル モードで使用する必要があります[ **! スレッド**](-thread.md)代わりにします。 このコマンドは、作成された場合に限りユーザー モードのミニダンプには、 **/mt**または **/ma**オプション; を参照してください[ユーザー モード ダンプ ファイル](user-mode-dump-files.md)詳細についてはします。

**.Ttime**コマンドはカーネル モードとユーザー モードで実行された時間数と同様に、スレッドの作成時刻を示します。

以下に例を示します。

```dbgcmd
0:000> .ttime
Created: Sat Jun 28 17:58:42 2003
Kernel:  0 days 0:00:00.131
User:    0 days 0:00:02.109
```

 

 





