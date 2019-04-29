---
title: .eventlog (最近のイベントの表示)
description: .Eventlog コマンドでは、モジュールの読み込み、プロセスの作成と終了、およびスレッドの作成や終了など、最新の Microsoft Win32 デバッグ イベントが表示されます。
ms.assetid: 8075007a-42a2-4973-bb04-cca9a4a1b9b6
keywords:
- .eventlog (最近のイベントを表示する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .eventlog (Display Recent Events)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56a217b2d6bd5da76af50c85d8ad134bc23bf859
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334500"
---
# <a name="eventlog-display-recent-events"></a>.eventlog (最近のイベントの表示)


**.Eventlog**コマンド モジュールの読み込み、プロセスの作成と終了、およびスレッドの作成や終了など、最新の Microsoft Win32 デバッグ イベントを表示します。

```dbgcmd
.eventlog 
```

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

 

<a name="remarks"></a>注釈
-------

**.Eventlog**コマンドは 1,024 文字を示しています。

次の例は、 **.eventlog**コマンド。

```dbgcmd
0:000> .eventlog
0904.1014: Load module C:\Windows\system32\ADVAPI32.dll at 000007fe`fed80000
0904.1014: Load module C:\Windows\system32\RPCRT4.dll at 000007fe`fe8c0000
0904.1014: Load module C:\Windows\system32\GDI32.dll at 000007fe`fea00000
0904.1014: Load module C:\Windows\system32\USER32.dll at 00000000`76b10000
0904.1014: Load module C:\Windows\system32\msvcrt.dll at 000007fe`fe450000
0904.1014: Load module C:\Windows\system32\COMDLG32.dll at 000007fe`fecf0000
0904.1014: Load module C:\Windows\system32\SHLWAPI.dll at 000007fe`fe1f0000
0904.1014: Load module C:\Windows\WinSxS\amd64_microsoft.windows.common-controls_6595b6414
4ccf1df_6.0.6000.16386_none_1559f1c6f365a7fa\COMCTL32.dll at 000007fe`fbda0000
0904.1014: Load module C:\Windows\system32\SHELL32.dll at 000007fe`fd4a0000
0904.1014: Load module C:\Windows\system32\WINSPOOL.DRV at 000007fe`f77d0000
0904.1014: Load module C:\Windows\system32\ole32.dll at 000007fe`feb10000
0904.1014: Load module C:\Windows\system32\OLEAUT32.dll at 000007fe`feeb0000
Last event: Break instruction exception - code 80000003 (first chance)
```

 

 





