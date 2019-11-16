---
title: Windows 上の DTrace
description: DTrace は、システム情報とイベントを表示するためのコマンドラインツールツールです。
ms.assetid: abf23d76-423d-4d1e-afde-83739015bbfe
keywords:
- DTrace WDK
- ソフトウェアトレース WDK、DTrace
- トレースメッセージの表示
- トレースメッセージの書式設定 WDK DTrace
- トレースメッセージの書式設定 WDK DTrace
- ソフトウェアトレース WDK, 書式設定メッセージ
- WDK のトレース、DTrace
- トレースメッセージフォーマットファイル WDK
ms.date: 11/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 33c0c4c513d3c1a65db4da128850bd33256ddc80
ms.sourcegitcommit: 79490c5067a50727f928f213c16c5f8f62898b60
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2019
ms.locfileid: "74119513"
---
# <a name="dtrace-on-windows"></a>Windows 上の DTrace

DTrace (caspol.exe) は、システム情報とイベントを表示するコマンドラインツールです。 DTrace は、windows に移植されたオープンソースのトレースプラットフォームです。 DTrace はもともと、Solaris オペレーティングシステム用に開発されました。  これは、ユーザー/カーネル関数の動的なインストルメンテーションと、D 言語の予測トレースを使用したスクリプト作成機能を提供します。 さらに、DTrace には、ETW インストルメンテーション、ETW イベント生成、システムコールプローブ、およびライブダンプキャプチャ機能などの Windows OS 固有の拡張機能があります。  

> [!NOTE]
> DTrace は、バージョン18980および Windows Server Insider Preview ビルド18975以降の Windows の Insider ビルドでサポートされています。

DTrace on Windows Github サイトは次の場所にあります。

[https://github.com/microsoft/DTrace-on-Windows](https://github.com/microsoft/DTrace-on-Windows)

## <a name="open-dtrace-information"></a>DTrace 情報を開く
  
DTrace の詳細については、ケンブリッジの大学の[OpenDTrace 仕様バージョン 1.0](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-924.pdf)を参照してください。

プライマリ GitHub サイトは[https://github.com/opendtrace/](https://github.com/opendtrace/)にあります。

一連の便利なスクリプトは、 [https://github.com/opendtrace/toolkit](https://github.com/opendtrace/toolkit)で入手できます。

[DTrace.Org](https://dtrace.org)は、元の開発者の多くがヒントと秘訣を提供する web サイトです。

Illumos[動的トレースガイド](http://dtrace.org/guide/bookinfo.html)では、DTrace を使用してシステムの動作を監視、デバッグ、調整する方法について説明します。

次のような多くの DTrace ブックが用意されています。

DTrace: Brendan Gregg と Jim Mauro による*Oracle Solaris、Mac OS X および FreeBSD の動的トレース*

*Solaris のパフォーマンスとツール: DTrace および MDB での solaris 10 および OpenSolaris* (Richard McDougall、Jim Mauro、Brendan Gregg)

## <a name="providing-feedback-on-windows-dtrace"></a>Windows DTrace に関するフィードバックの提供

フィードバックハブを使用して、新しい機能を要求したり、Windows DTrace に関する問題やバグを報告したりします。

1. このリンク[https://windows-feedback:?contextid=1053](https://windows-feedback:?contextid=1053)をクリックして、Windows PC からフィードバックハブを起動します。
2. [*新しいフィードバックの追加*] を選択します。
3. 問題または提案の詳細な具体的な説明を入力します。

## <a name="dtrace-windows-extensions"></a>DTrace の Windows 拡張機能

Windows で使用可能なプロバイダーとその機能を次に示します。

- syscall – NTOS システム呼び出し

- fbt (関数境界トレース) –カーネル関数の入力と戻り値

- pid (プロセス ID) –ユーザーモードのプロセストレース。 カーネルモードの FBT と同様に、任意の関数オフセットのインストルメンテーションも許可します。

- etw (Windows イベントトレーシング) – ETW でプローブを定義できるようにします。このプロバイダーは、DTrace の既存のオペレーティングシステムのインストルメンテーションを活用するのに役立ちます。

### <a name="syscall"></a>SYSCALL

SYSCALL は、システム呼び出しごとにプローブのペアを提供します。システムコールが入力される前に起動されるエントリプローブと、システム呼び出しが完了した後、制御がユーザーレベルに戻される前に発生する戻りプローブです。 すべての SYSCALL プローブでは、関数名はインストルメント化されたシステム呼び出しの名前に設定され、モジュール名は関数が存在するモジュールになります。 SYSCALL プロバイダーによって提供されるシステム呼び出しの名前は、コマンドプロンプトから `dtrace.exe -l -P syscall` コマンドを入力することによって見つけることができます。 プローブ名は、大文字と小文字を区別しないことに注意してください。 コマンド `dtrace -ln syscall:::` には、syscall プロバイダーから取得できるすべてのプローブとそのパラメーターも表示されます。

```dtrace
C:\> dtrace -ln syscall:::
  ID   PROVIDER            MODULE                          FUNCTION NAME
    6    syscall                                 NtWaitHighEventPair entry
    7    syscall                                 NtWaitHighEventPair return
    8    syscall                       NtRegisterThreadTerminatePort entry
    9    syscall                       NtRegisterThreadTerminatePort return
...
```

これらの例では、すべての画面出力が表示されるわけではないことに注意してください。 "..."は、切り捨てられた出力を表すために使用されます。

出力をスクロールするには、次のように、パイプを使用して*more*コマンドを実行します。

`dtrace -ln syscall:::|more`

使用可能な syscall プローブに関する詳細情報を表示するには、v オプションを追加します。

```dtrace
C:\> dtrace -lvn syscall:::
...

  942    syscall                                    NtSaveMergedKeys entry

        Probe Description Attributes
                Identifier Names: Private
                Data Semantics:   Private
                Dependency Class: ISA

        Argument Attributes
                Identifier Names: Private
                Data Semantics:   Private
                Dependency Class: ISA

        Argument Types
                args[0]: HANDLE
                args[1]: HANDLE
                args[2]: HANDLE
...
```

### <a name="etw"></a>ETW

 DTrace には、既存のマニフェストプローブとトレースログ記録 ETW プローブのサポートが含まれています。 ETW イベントは、イベントの発生時に同期的にインストルメント化、フィルター処理、解析することができます。 さらに、DTrace を使用して、さまざまなイベントやシステムの状態を組み合わせて、複雑なエラー状況のデバッグに役立つ統合された出力ストリームを提供できます。  

コマンド `dtrace -ln etw:::` には、syscall プロバイダーから取得できるすべてのプローブとそのパラメーターが一覧表示されます。

```dtrace
  C:\> dtrace -ln etw:::
  ID   PROVIDER            MODULE                          FUNCTION NAME
  944        etw 048dc470-37c1-52a8-565a-54cb27be37ec           0xff_0xffffffffffffffff generic_event
  945        etw aab97afe-deaf-5882-1e3b-d7210f059dc1           0xff_0xffffffffffffffff generic_event
  946        etw b0f40491-9ea6-5fd5-ccb1-0ec63be8b674           0xff_0xffffffffffffffff generic_event
  947        etw 4ee869fa-9954-4b90-9a62-308c74f99d32           0xff_0xffffffffffffffff generic_event
  ...
  ```

詳細については、「 [DTRACE ETW](dtrace-etw.md)」を参照してください。

### <a name="function-boundary-tracing-fbt"></a>関数境界トレース (FBT)

関数境界トレース (FBT) プロバイダーは、のエントリに関連付けられているプローブを提供し、Windows カーネル内のほとんどの関数を返します。 関数は、プログラムテキストの基本単位です。 他の DTrace プロバイダーと同様に、FBT は明示的に有効になっていない場合にプローブ効果を持ちません。 有効にすると、FBT はプローブされた関数でプローブ効果を誘発するだけです。 FBT は、x86 および x64 プラットフォームに実装されています。

各命令セットには、他の関数を呼び出さず、FBT によってインストルメント化できないコンパイラ (いわゆるリーフ関数) によって高度に最適化された関数の数が少なくなっています。 これらの関数のプローブは、DTrace には存在しません。

コマンド `dtrace -ln fbt:nt::` には、nt モジュールで使用できるすべてのプローブとそのパラメーターの一覧が表示されます。 使用可能なすべてのモジュールを一覧表示するには、デバッガーの [ [lm] (読み込まれたモジュールの一覧)](https://docs.microsoft.com/windows-hardware/drivers/debugger/lm--list-loaded-modules-)コマンドを使用します。

```dtrace
C:\>dtrace -ln "fbt:nt::"
   ID   PROVIDER            MODULE                          FUNCTION NAME
 3336        fbt                nt                PiDqActionDataFree entry
 3337        fbt                nt                PiDqActionDataFree return
 3338        fbt                nt PiDqActionDataGetRequestedProperties entry
 3339        fbt                nt PiDqActionDataGetRequestedProperties return
 3340        fbt                nt _CmGetMatchingFilteredDeviceInterfaceList entry
...
```

> [!NOTE]
> Nt では何千もの呼び出しを利用できますが、データをログに記録する DTrace コマンドを実行するときは、関数名を空のままにすることはお勧めしません。 パフォーマンスへの影響を回避するために推奨される方法は、`fbt:nt:*Timer*:entry`などの関数名の一部を指定することです。

### <a name="pid"></a>PID

DTrace PID プロバイダーを使用すると、web ブラウザーやデータベースなどのユーザーモードプロセスの内部実行をトレースできます。 プロセスの起動時に DTrace をアタッチして、プロセスの起動時の問題をデバッグすることもできます。 PID 定義の一部として、関数内のプロセスおよび特定のオフセット (またはワイルドカードを使用したすべてのオフセット) で定義されている関数を指定します。 PID プロバイダーを使用するには、スクリプトの実行時にバイナリを起動または実行する必要があります。

この例のコマンドは、notepad.exe に関連付けられている PID 内の特定の呼び出しに関する情報を表示します。 使用可能なすべてのモジュールを一覧表示するには、デバッガーの [ [lm] (読み込まれたモジュールの一覧)](https://docs.microsoft.com/windows-hardware/drivers/debugger/lm--list-loaded-modules-)コマンドを使用します。

```dtrace
C:\Windows\system32>dtrace -ln "pid$target:ntdll:RtlAllocateHeap:entry" -c notepad.exe
   ID   PROVIDER            MODULE                          FUNCTION NAME
 5102    pid6100             ntdll                   RtlAllocateHeap entry
```

## <a name="dtrace-windows-architecture"></a>DTrace Windows アーキテクチャ

ユーザーは dtrace コマンドを使用して dtrace と対話します。 dtrace コマンドは、dtrace エンジンへのフロントエンドとして機能します。 D スクリプトはユーザー空間で中間形式 (差分) にコンパイルされ、実行のために DTrace カーネルコンポーネントに送信されます。これは、差分仮想マシンと呼ばれることもあります。 これは、dtrace ドライバーで実行されます。

Traceext (trace extension) は、Windows カーネル拡張機能ドライバーです。これにより、Windows は、DTrace が依存している機能を公開して、トレースを提供します。 Windows カーネルは、stackwalk またはメモリアクセス時にコールアウトを提供し、その後、トレース拡張機能によって実装されます。

![Dtrace の Windows アーキテクチャ。このファイルは、caspol.exe を呼び出す libtrace と対話します。](images/dtrace-architecture.png)

## <a name="installing-dtrace-under-windows"></a>Windows での DTrace のインストール

1. サポートされているバージョンの Windows を実行していることを確認してください。 DTrace の現在のダウンロードは、バージョン18980および Windows Server Insider Preview ビルド18975後の 20H1 Windows の Insider ビルドでサポートされています。 *このバージョンの DTrace を古いバージョンの Windows にインストールすると、システムが不安定になり、推奨されません。*

   アーカイブされたバージョンの DTrace on 19H1 は、「 [Windows 上の Dtrace ダウンロード DTrace](https://www.microsoft.com/en-us/download/58091)」で入手できます。 このバージョンの DTrace はサポートされなくなったことに注意してください。


1. MSI インストールファイルは、Microsoft ダウンロードセンターからダウンロードしてください。 [Windows で DTrace をダウンロード](https://www.microsoft.com/download/details.aspx?id=100441)してください。


2. 完全なインストールを選択します。

    > [!IMPORTANT]
    > Bcdedit を使用してブート情報を変更する前に、テスト PC での修正、BitLocker、セキュアブートなどの Windows セキュリティ機能を一時的に中断することが必要になる場合があります。
    > セキュリティ機能が無効になっている場合は、テストが完了し、テスト PC を適切に管理するときに、これらのセキュリティ機能を再び有効にします。

3. Bcdedit コマンドを使用して、コンピューターで DTrace を有効にします。  

```cmd
bcdedit /set dtrace ON
```

新しい Windows Insider build に更新する場合は、dtrace bcdedit オプションをもう一度設定する必要があります。

> [!NOTE]
> BitLocker を使用している場合は、ブート値を変更するときに無効にします。 この操作を行わないと、BitLocker 回復キーの入力を求められる場合があります。 この状況から回復する方法の1つとして、回復コンソールを起動して、bcdedit の値を `bcdedit /set {default} dtrace on`復元する方法があります。 OS 更新プログラムによって値が削除され、に追加された場合、OS を回復するには、bcdedit を使用して値を削除し、`bcdedit /deletevalue {default} dtrace`します。 次に、BitLocker を無効にしてから、`bcdedit /set dtrace ON`を再度有効にします。

"HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\DeviceGuard\EnableVirtualizationBasedSecurity" を1に設定して、VSM と Secure を有効にすることで、カーネル関数境界トレース (FBT) を有効にするために、コンピューターで VSM (仮想セキュアモード) を構成します。カーネル.

これを行うには、次のように REG Add コマンドを使用します。

```cmd
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceGuard\ /v EnableVirtualizationBasedSecurity /t REG_DWORD /d 1
```

一部の DTrace コマンドでは、Windows シンボルを使用します。 Windows シンボルを使用するには、シンボルディレクトリを作成し、シンボルパスを設定します。  

```cmd
mkdir c:\symbols
set _NT_SYMBOL_PATH=srv*C:\symbols*https://msdl.microsoft.com/download/symbols 
```

シンボルパスの詳細については、「 [Windows デバッガーのシンボルパス](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbol-path)」を参照してください。

### <a name="using-dtrace-inside-of-a-virtual-machine"></a>仮想マシン内での DTrace の使用

Vm で DTrace を実行している場合は、vm が停止しているときに、次の PowerShell コマンドを使用して、vm をサポートしているマシンで入れ子になった仮想化を有効にします。 DTrace を実行している VM の `<VMName>` を指定します。 管理者として PowerShell ウィンドウを開きます。

```powershell
Set-VMProcessor -VMName <VMName> -ExposeVirtualizationExtensions $true
```

VM をサポートする PC を再起動します。

### <a name="validating-the-dtrace-installation"></a>DTrace のインストールの検証

アクティブなプローブの一覧を表示するには、-l オプションを使用します。 DTrace がアクティブになっている場合は、etw およびシステムイベントに対して多くのプローブが一覧表示されます。

管理者として Windows コマンドプロンプトを開き、DTrace コマンドを入力します。

```dtrace
C:\> dtrace -l

...

  179    syscall                                 NtLockVirtualMemory return
  180    syscall                               NtDeviceIoControlFile entry
  181    syscall                               NtDeviceIoControlFile return
  182    syscall                                 NtCreateUserProcess entry
  183    syscall                                 NtCreateUserProcess return
  184    syscall                                      NtQuerySection entry
  185    syscall                                      NtQuerySection return

...

 3161        etw 222962ab-6180-4b88-a825-346b75f2a24a           0xff_0xffffffffffffffff generic_event
 3162        etw 3ac66736-cc59-4cff-8115-8df50e39816b           0xff_0xffffffffffffffff generic_event
 3163        etw 42695762-ea50-497a-9068-5cbbb35e0b95           0xff_0xffffffffffffffff generic_event
 3164        etw 3beef58a-6e0f-445d-b2a4-37ab737bd47e           0xff_0xffffffffffffffff generic_event

...

```

これら3つのプローブだけが一覧表示されている場合は、DTrace ドライバーの読み込みに問題があります。

```dtrace
C:\>  dtrace -l
   ID   PROVIDER            MODULE                          FUNCTION NAME
    1     dtrace                                                     BEGIN
    2     dtrace                                                     END
    3     dtrace                                                     ERROR
```

## <a name="getting-started-with-dtrace---one-line-commands"></a>DTrace の概要-1 行のコマンド

まず、管理者コマンドプロンプトから次のコマンドを実行します。

このコマンドは、5秒間のプログラム別の syscall 概要を表示します。 Tick-5sec パラメーターは、期間を指定します。 終了 (0);コマンドプロンプトに戻ったときにコマンドを終了させます。 出力は `[pid,execname] = count();` 使用して指定されます。これにより、プロセス ID (PID)、実行可能ファイルの名前、および最後の5秒間のカウントが表示されます。

``` dtrace
C:\> dtrace -Fn "tick-5sec {exit(0);} syscall:::entry{ @num[pid,execname] = count();} "  
dtrace: description 'tick-5sec ' matched 471 probes
CPU FUNCTION
  0 | :tick-5sec

     1792  svchost.exe                                                       4
     4684  explorer.exe                                                      4
     4916  dllhost.exe                                                       4
     6192  svchost.exe                                                       4
     6644  SecurityHealth                                                    4
       92  TrustedInstall                                                    5
      504  csrss.exe                                                         5
      696  svchost.exe                                                       6
...
```

このコマンドは、次の3秒間のタイマー設定/キャンセル呼び出しの概要を示します。  

``` dtrace
C:\> dtrace -Fn "tick-3sec {exit(0);} syscall::Nt*Timer*:entry { @[probefunc, execname, pid] = count();}"
dtrace: description 'tick-3sec ' matched 14 probes
CPU FUNCTION
  0 | :tick-3sec

  NtCreateTimer                                       WmiPrvSE.exe                                            948                1
  NtCreateTimer                                       svchost.exe                                             564                1
  NtCreateTimer                                       svchost.exe                                            1276                1
  NtSetTimer2                                         svchost.exe                                            1076                1
  NtSetTimer2                                         svchost.exe                                            7080                1
  NtSetTimerEx                                        WmiPrvSE.exe                                            948                1
...  
```

### <a name="one-line-commands-that-use-symbols"></a>シンボルを使用する1行のコマンド

これらのコマンドは、Windows シンボルを利用し、インストールセクションで説明されているように、シンボルパスを設定する必要があります。
前述のインストールで説明したように、ディレクトリを作成し、次のコマンドを使用してシンボルパスを設定します。

```cmd
C:\> mkdir c:\symbols
C:\> set _NT_SYMBOL_PATH=srv*C:\symbols*https://msdl.microsoft.com/download/symbols
```

この例のコマンドは、上位の NT 関数を表示します。

```dtrace
C:\> dtrace -n "fbt:nt:*Timer*:entry { @k[probefunc] = count(); } tick-5s { trunc(@k, 10);printa(@k); exit(0); }"
dtrace: description 'fbt:nt:*Timer*:entry ' matched 340 probes
CPU     ID                    FUNCTION:NAME
  0  22362                         :tick-5s
  KeCancelTimer                                                   712
  KeSetTimer2                                                     714
  HalpTimerClearProblem                                           908
  ExpSetTimerObject                                               935
  NtSetTimerEx                                                    935
  KeSetTimer                                                     1139
  KeSetCoalescableTimer                                          3159
  KeResumeClockTimerFromIdle                                    11767
  xHalTimerOnlyClockInterruptPending                            22819
  xHalTimerQueryAndResetRtcErrors                               22819
```

このコマンドは、SystemProcess カーネル構造体をダンプします。

```dtrace
C:\> dtrace -n "BEGIN {print(*(struct nt`_EPROCESS *) nt`PsInitialSystemProcess);exit(0);}"

...

   uint64_t ParentSecurityDomain = 0
    void *CoverageSamplerContext = 0
    void *MmHotPatchContext = 0
    union _PS_PROCESS_CONCURRENCY_COUNT ExpectedConcurrencyCount = {
         Fraction :20 = 0
         Count :12 = 0
        uint32_t AllFields = 0
    }
    struct _KAFFINITY_EX IdealProcessorSets = {
        uint16_t Count = 0x1
        uint16_t Size = 0x20
        uint32_t Reserved = 0
        uint64_t [32] Bitmap = [ 0x1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ]
    }
}
```

このコマンドは、過去10秒間の上位カーネルスタックを表示します。

``` dtrace
C:\> dtrace -qn "profile-997hz { @[stack()] = count(); } tick-10sec { trunc(@,5); printa(@); exit(0);}"

              nt`KiDispatchInterruptContinue
              nt`KiDpcInterrupt+0x318
              nt`KiSwapThread+0x1054
              nt`KiCommitThreadWait+0x153
              nt`KeRemoveQueueEx+0x263
              nt`IoRemoveIoCompletion+0x54
              nt`NtWaitForWorkViaWorkerFactory+0x284
              nt`KiSystemServiceCopyEnd+0x35
               14

              nt`KiDispatchInterruptContinue
              nt`KiDpcInterrupt+0x318
...
```

このコマンドは、起動中に notepad.exe によって呼び出された上位のモジュールを表示します。 -C オプションは、指定されたコマンド (notepad.exe) を実行し、完了時に終了します。

``` dtrace
C:\> dtrace -qn "pid$target:::entry { @k[probemod] = count();} tick-10s{printa(@k); exit(0);}" -c notepad.exe

  gdi32full                                                         5
  msvcp_win                                                         6
  combase                                                           7
  notepad                                                           9
  ADVAPI32                                                         10
  GDI32                                                            11
  SHELL32                                                          11
  USER32                                                           21
  win32u                                                          345
  KERNELBASE                                                     3727
  msvcrt                                                         7749
  KERNEL32                                                       9883
  RPCRT4                                                        11710
  ntdll                                                        383445

```

## <a name="see-also"></a>関連項目

[DTrace の Windows プログラミング](dtrace-programming.md)

[DTrace ETW](dtrace-etw.md)

[DTrace ライブダンプ](dtrace-live-dump.md)

[DTrace Windows コードサンプル](dtrace-code-samples.md)
