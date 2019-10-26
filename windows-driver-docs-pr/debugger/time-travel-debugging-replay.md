---
title: Time Travel Debugging - トレースの再生
description: このセクションでは、タイムトラベルトレースを再生する方法について説明します。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2639b5e4654a2e52554295243aa0ada484b8b1a3
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916139"
---
# <a name="time-travel-debugging---replay-a-trace"></a>Time Travel Debugging - トレースの再生

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png) 

このセクションでは、時間旅行トレースを再生し、前後を移動する方法について説明します。

## <a name="command-time-travel-navigation"></a>コマンドタイムトラベルナビゲーション

次のコマンドで末尾のマイナス記号を使用して、時間をさかのぼって移動します。

| コマンド  | 
|----------------|
| p-(ステップバック) | 
| t-(トレースバック)| 
| g-(戻る)   |

詳細については、「[タイムトラベルのデバッグ-ナビゲーションコマンド](time-travel-debugging-navigation-commands.md)」を参照してください。 

## <a name="ribbon-button-time-travel-navigation"></a>リボンボタンのタイムトラベルナビゲーション

または、リボンのボタンを使用してトレース内を移動します。

![記録の開始チェックボックスが表示されている WinDbg プレビューのスクリーンショット](images/ttd-ribbon-buttons.png)


## <a name="example-ttd-trace-replay"></a>TTD トレース再生の例

TTD トレースのイベントまたは先頭に到達するまで、コマンドを使用して後方に実行します。 逆方向の実行を停止できるイベントは、実行を停止するイベントと同じです。 この例では、トレースの開始に達しています。


```dbgcmd
0:000> g-
TTD: Start of trace reached.
(3f78.4274): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 29:0
ntdll!ZwTestAlert+0x14:
00007ffc`61f789d4 c3              ret
```

[P (ステップ)](https://docs.microsoft.com/windows-hardware/drivers/debugger/p--step-)コマンドを使用して、TTD トレースでステップフォワードします。 

```dbgcmd
0:000> p
Time Travel Position: F:1
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774f828 esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x1bc5:
7774f828 740b            je      ntdll!LdrpInitializeProcess+0x1bd2 (7774f835) [br=1]
0:000> p
Time Travel Position: F:2
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774f835 esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x1bd2:
7774f835 83bdd0feffff00  cmp     dword ptr [ebp-130h],0 ss:002b:010ff454=00000000
0:000> p
Time Travel Position: F:3
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774f83c esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x1bd9:
7774f83c 0f8450e8ffff    je      ntdll!LdrpInitializeProcess+0x42f (7774e092) [br=1]
```

また、 [t (trace)](https://docs.microsoft.com/windows-hardware/drivers/debugger/t--trace-)コマンドを使用してトレース内を移動することもできます。

```dbgcmd
0:000> t
Time Travel Position: F:4
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774e092 esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x42f:
7774e092 33c0            xor     eax,eax
0:000> t
Time Travel Position: F:5
eax=00000000 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774e094 esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x431:
7774e094 e9f5170000      jmp     ntdll!LdrpInitializeProcess+0x1c2b (7774f88e)
```


TTD トレースで前に進むには、p-コマンドを使用します。 

```dbgcmd
0:000> p-
Time Travel Position: F:4
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774e092 esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x42f:
7774e092 33c0            xor     eax,eax
0:000> p-
Time Travel Position: F:3
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774f83c esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x1bd9:
7774f83c 0f8450e8ffff    je      ntdll!LdrpInitializeProcess+0x42f (7774e092) [br=1]
```

また、t-sql を使用して、時間をさかのぼって移動することもできます。


## <a name="tt-navigation-commands"></a>! tt ナビゲーションコマンド

! Tt コマンドを使用して、トレース内の特定の位置にスキップすることにより、時間の前後に移動します。 

! tt [位置]

その時点に移動するには、次のいずれかの形式で時刻の位置を指定します。
           
- [Position] が0から100までの10進数である場合、トレースに約そのパーセント移動します。 たとえば `!tt 50` は、トレースを通じて中間に移動します。

- {Position} が #: # の場合 (# は16進数)、その位置に移動します。 たとえば、`!tt 1A0:12F` はトレースで 1A0: 12F の位置に移動します。

詳細については、「[タイムトラベルデバッグ-! tt (タイムトラベル)](time-travel-debugging-extension-tt.md)」を参照してください。


## <a name="positions"></a>! 位置

`!positions` を使用すると、トレース内のすべてのアクティブなスレッドを表示できます。 詳細については、「[タイムトラベルデバッグ-! 位置 (タイムトラベル)](time-travel-debugging-extension-positions.md)」を参照してください。

```dbgcmd
0:000> !positions
>Thread ID=0x1C74 - Position: F:2
 Thread ID=0x1750 - Position: A5:0
 Thread ID=0x3FFC - Position: 200:0
 Thread ID=0x36B8 - Position: 403:0
 Thread ID=0x3BC4 - Position: 5F2:0
 Thread ID=0x392C - Position: B45:0
 Thread ID=0x32B4 - Position: C87:0
 Thread ID=0x337C - Position: DF1:0
```
この例は、現在の位置に8つのスレッドがあることを示しています。 現在のスレッドは3604で、' > ' でマークされています。  

> [!TIP] 
> 現在のスレッドの一覧とその位置を表示するもう1つの方法は、データモデルの dx コマンドを使用することです。
>
> `dx -g @$curprocess.Threads.Select(t => new { IsCurrent = t.Id == @$curthread.Id, ThreadId = t.Id, Position = t.TTD.Position })`
>

User mode [~ (スレッドの状態)](---thread-status-.md)コマンドを使用すると、同じ8つのスレッドが表示され、現在のスレッドに '. ' がマークされます。

```dbgcmd
0:000> ~
.  0  Id: 954.1c74 Suspend: 4096 Teb: 00fdb000 Unfrozen
   1  Id: 954.1750 Suspend: 4096 Teb: 00fea000 Unfrozen
   2  Id: 954.3ffc Suspend: 4096 Teb: 00fde000 Unfrozen
   3  Id: 954.36b8 Suspend: 4096 Teb: 00fe1000 Unfrozen
   4  Id: 954.3bc4 Suspend: 4096 Teb: 00fe4000 Unfrozen
   5  Id: 954.392c Suspend: 4096 Teb: 00fed000 Unfrozen
   6  Id: 954.32b4 Suspend: 4096 Teb: 00ff0000 Unfrozen
   7  Id: 954.337c Suspend: 4096 Teb: 00ff3000 Unfrozen
```

! Position 出力の3番目のスレッド (3FFC) の横にあるリンクをクリックして、トレースのその位置 (200:0) に移動します。

```dbgcmd
0:002> !ttdext.tt 200:0
Setting position: 200:0
(954.3ffc): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 200:0
eax=00000000 ebx=012da718 ecx=7775396c edx=00000000 esi=012e1848 edi=012e1a08
eip=7775396c esp=014cf9f8 ebp=014cfbfc iopl=0         nv up ei ng nz ac po cy
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000293
ntdll!NtWaitForWorkViaWorkerFactory+0xc:
7775396c c21400          ret     14h
```

[~ (スレッドの状態)](---thread-status-.md)コマンドを使用して、現在、3番目のスレッド3ffc に配置されていることを確認します。

```dbgcmd
0:002> ~
   0  Id: 954.1c74 Suspend: 4096 Teb: 00fdb000 Unfrozen
   1  Id: 954.1750 Suspend: 4096 Teb: 00fea000 Unfrozen
.  2  Id: 954.3ffc Suspend: 4096 Teb: 00fde000 Unfrozen
   3  Id: 954.36b8 Suspend: 4096 Teb: 00fe1000 Unfrozen
   4  Id: 954.3bc4 Suspend: 4096 Teb: 00fe4000 Unfrozen
   5  Id: 954.392c Suspend: 4096 Teb: 00fed000 Unfrozen
   6  Id: 954.32b4 Suspend: 4096 Teb: 00ff0000 Unfrozen
   7  Id: 954.337c Suspend: 4096 Teb: 00ff3000 Unfrozen
```


> [!NOTE]
> *~ S #* では、 *#* はスレッド番号ですが、指定されたスレッドにも切り替わりますが、トレースの現在位置は変更されません。  *! Tt*を使用して別のスレッドの位置に時間を移動すると、メモリから読み取られた値 (およびデバッガー) がその位置で検索されます。 *~ S #* のスレッドを切り替えると、デバッガーは現在の位置を内部で変更しません。これは、すべてのメモリクエリに使用されます。 これは主に、 *~ s #* でデバッガーの内側のループをリセットする必要がないため、この方法で動作します。


## <a name="time-travel-debugging-extension-commands"></a>タイムトラベルデバッグ拡張コマンド

`!tt`の詳細については `!index` `!positions`、「[タイムトラベルデバッグ-拡張コマンド](time-travel-debugging-extension-commands.md)」を参照してください。

 
## <a name="see-also"></a>参照

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)

[タイムトラベルデバッグ-トレースを記録する](time-travel-debugging-record.md)

[タイムトラベルデバッグ-トレースファイルの操作](time-travel-debugging-trace-file-information.md)

[タイムトラベルデバッグ-サンプルアプリのチュートリアル](time-travel-debugging-walkthrough.md)

