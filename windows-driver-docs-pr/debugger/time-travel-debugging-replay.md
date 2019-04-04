---
title: タイム トラベル デバッグ - トレースの再生
description: 時間を再生する方法を説明するトレースを移動します。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4f9eb21ef930c66b3995e4afbd587a347049b880
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537754"
---
![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png) 

# <a name="time-travel-debugging---replay-a-trace"></a>タイム トラベル デバッグ - トレースの再生 

時間の直接的および下位タイム トラベルを再生するトレース、転送を移動する方法について説明します。

## <a name="command-time-travel-navigation"></a>コマンドに旅行ナビゲーション

次のコマンドで、末尾の負符号を使用して、時点に戻り。

| コマンド  | 
|----------------|
| p – (バックアップの手順) | 
| t-(さかのぼって)| 
| g: (戻る)   |

詳細については、[タイム トラベルのデバッグ - ナビゲーション コマンド](time-travel-debugging-navigation-commands.md)を参照してください。 

## <a name="ribbon-button-time-travel-navigation"></a>リボン ボタン タイム トラベル ナビゲーション

代わりに、リボン ボタンを使用して、トレースに移動します。

![チェック ボックスをオンの記録の開始を示す WinDbg プレビューのスクリーン ショット](images/ttd-ribbon-buttons.png)


## <a name="example-ttd-trace-replay"></a>例 TTD トレースの再生

G コマンドを使用して、イベントを実行する下位まで、または TTD トレースの先頭に到達します。 旧バージョンとの実行を停止するイベントとフォワード実行が停止すると同じです。 この例では、トレースの開始に到達します。


```dbgcmd
0:000> g-
TTD: Start of trace reached.
(3f78.4274): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 29:0
ntdll!ZwTestAlert+0x14:
00007ffc`61f789d4 c3              ret
```

使用して、 [p (ステップ)](https://docs.microsoft.com/windows-hardware/drivers/debugger/p--step-) TTD トレースでステップ前進するコマンド。 

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

使用しても、 [t (トレース)](https://docs.microsoft.com/windows-hardware/drivers/debugger/t--trace-)トレース内を移動するコマンド。

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


P コマンドを使用して、後退 TTD トレースします。 

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

戻る操作を t コマンドを使用することもできます。


## <a name="tt-navigation-commands"></a>! tt ナビゲーション コマンド

使用して、!、トレース内の指定位置にスキップすることで、前方または後方を移動する tt コマンド。 

! tt [位置]

時間の点に移動する次の形式のいずれかの時間位置を指定します。
           
- [位置] が 0 から 100 までの 10 進数である場合は、トレースに約その % に移動します。 たとえば`!tt 50`が途中で、トレースに移動します。

- {0} 位置} が # である場合: #, # は、16 進数、送信するときにその位置にします。 たとえば、 `!tt 1A0:12F` 1A0:12F をトレースに位置に移動します。

詳細については、[時のデバッグ出張 -! tt (タイム トラベル)](time-travel-debugging-extension-tt.md)を参照してください。


## <a name="positions"></a>! 位置

使用`!positions`アクティブなすべてのスレッドをトレース内の位置を含むを表示します。 詳細については、[時のデバッグ出張 -! 位置 (タイム トラベル)](time-travel-debugging-extension-positions.md)を参照してください。

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
この例では、現在の位置にある 8 つのスレッドがあることを示します。 現在のスレッドが付いている 3604 ' >'。  

> [!TIP] 
> 現在のスレッドとそれらの位置の一覧を表示する別の方法では、データ モデルの dx コマンドを使用します。
>
> `dx -g @$curprocess.Threads.Select(t => new { IsCurrent = t.Id == @$curthread.Id, ThreadId = t.Id, Position = t.TTD.Position })`
>

ユーザー モードを使用して、 [~ (スレッド ステータス)](---thread-status-.md)コマンドは、同じ 8 個のスレッドを表示しで現在のスレッドをマーク '.'。

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

内の 3 番目のスレッド (3FFC) の横にあるリンクをクリックして、! 200:0 は、トレース内の位置をタイム トラベルへの出力を配置します。

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

使用して、 [~ (スレッド ステータス)](---thread-status-.md)コマンドをしましたが、3ffc、3 番目のスレッドで今すぐ配置されていることを確認します。

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
> *~ S #* ここで、 *#* もスイッチを特定のスレッドで、スレッドの番号ですが、トレース内の現在位置は変更されません。  ときに *! tt*が別のスレッドの位置への移動にかかる時間を使用して、(およびデバッガー) がメモリから読み取られた値を検索する位置にします。 スレッドを切り替えるときに *~ s #* デバッガーは現在位置を変更内部的には、メモリのすべてのクエリに使用されます。 この方法が主にこれは、動作を *~ s #* デバッガーの内側のループをリセットする必要はありません。


## <a name="time-travel-debugging-extension-commands"></a>タイム トラベルの拡張機能コマンドのデバッグ

については、 `!tt`、`!positions`と`!index`コマンドを参照してください[タイム トラベルのデバッグ - 拡張コマンド](time-travel-debugging-extension-commands.md)します。

 
## <a name="see-also"></a>参照

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

[タイム トラベル デバッグ - トレースの記録](time-travel-debugging-record.md)

[タイム トラベル デバッグ - トレース ファイルの使用](time-travel-debugging-trace-file-information.md)

[旅行のデバッグ時間 - サンプル アプリのチュートリアル](time-travel-debugging-walkthrough.md)

---






