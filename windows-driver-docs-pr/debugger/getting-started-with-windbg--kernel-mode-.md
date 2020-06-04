---
title: WinDbg の概要 (カーネル モード)
description: このトピックでは、WinDbg をカーネルモードのデバッガーとして使用する際に役立つ実践的な演習について説明します。
ms.assetid: 1B61591F-0D48-4FBD-B242-68BB90D27FAF
ms.date: 06/02/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2a2ea99d6be59ed31ad8b9fb46c7ddd00c8dae06
ms.sourcegitcommit: 0e83928aac8f171980e94b67f9291468e6e68093
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/03/2020
ms.locfileid: "84336393"
---
# <a name="getting-started-with-windbg-kernel-mode"></a>WinDbg の概要 (カーネル モード)

WinDbg は、Windows 用デバッグツールに含まれているカーネルモードおよびユーザーモードのデバッガーです。 ここでは、WinDbg をカーネルモードのデバッガーとして使用する際に役立つ実践的な演習を提供します。

Windows 用のデバッグツールを入手する方法については、「 [windows 用デバッグツール (WinDbg、KD、CDB、NTSD)](index.md)」を参照してください。 デバッグツールをインストールしたら、64ビット (x64) および32ビット (x86) バージョンのツールのインストールディレクトリを見つけます。 次に例を示します。

- C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x64
- C: \\ Program Files (x86) \\ Windows kit \\ 10 \\ デバッガー \\ x86

## <a name="set-up-a-kernel-mode-debugging"></a>カーネルモードのデバッグを設定する

通常、カーネルモードのデバッグ環境には、*ホストコンピューター*と*対象コンピューター*という2台のコンピューターがあります。 デバッガーはホスト コンピューター上で実行され、デバッグ対象のコードはターゲット コンピューター上で実行されます。 ホストとターゲットは、デバッグケーブルによって接続されています。

Windows デバッガーは、デバッグ用に次の種類のケーブルをサポートしています。

- イーサネット
- USB 2.0/USB 3.0
- シリアル (null モデムとも呼ばれます)

速度と信頼性のために、ローカルネットワークハブでイーサネットを使用することをお勧めします。 この図は、イーサネットケーブル経由でデバッグするために接続されたホストとターゲットコンピューターを示しています。

![イーサネット接続を使用したホストとターゲットの図](images/configfortest01.png)

以前のバージョンの Windows では、USB やシリアルケーブルなどの直接ケーブルを使用する方法もあります。

![デバッグケーブルを使用したホストとターゲットの図](images/configfortest02.png)

ホストとターゲットコンピューターを設定する方法の詳細については、「[カーネルモードデバッグの手動](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)セットアップ」を参照してください。

### <a name="virtual-machine---vms"></a>仮想マシン-Vm

Hyper-v 仮想マシンへのデバッガーの接続の詳細については、「[仮想マシンのネットワークデバッグの設定-KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)」を参照してください。

## <a name="establish-a-kernel-mode-debugging-session"></a>カーネルモードのデバッグセッションを確立する

ホストとターゲットコンピューターを設定し、デバッグケーブルで接続したら、セットアップに使用したのと同じトピックに記載されている手順に従って、カーネルモードのデバッグセッションを確立できます。 たとえば、イーサネット上でデバッグするためにホストとターゲットコンピューターを設定する場合、カーネルモードのデバッグセッションを確立するための手順は、次のトピックに記載されています。

- [KDNET ネットワーク カーネル デバッグの自動設定](setting-up-a-network-debugging-connection-automatically.md)

## <a name="get-started-using-windbg"></a>WinDbg を使用して作業を開始する

1. ホストコンピューターで、WinDbg を開き、対象のコンピューターとのカーネルモードデバッグセッションを確立します。
2. [WinDbg] で、[**ヘルプ**] メニューの [**コンテンツ**] をクリックします。 デバッガーのドキュメント CHM ファイルが開きます。 デバッガーのドキュメントは、「 [Windows 用のデバッグツール](index.md)」にも記載されています。
3. カーネルモードのデバッグセッションを確立すると、WinDbg によって対象コンピューターが自動的に中断されることがあります。 WinDbg がまだ壊れていない場合は、[**デバッグ**] メニューの [**中断**] をクリックします。

4. WinDbg ウィンドウの下部にあるコマンドラインで、次のコマンドを入力します。

   [**. sympath srv\***](-sympath--set-symbol-path-.md)

   出力は次のようになります。

   ```dbgcmd
   Symbol search path is: srv*
   Expanded Symbol search path is: cache*;SRV*https://msdl.microsoft.com/download/symbols
   ```

   シンボル検索パスは、WinDbg がシンボル (PDB) ファイルを検索する場所を指定します。 デバッガーは、コードモジュール (関数名、変数名など) に関する情報を取得するために、シンボルファイルを必要とします。

   次のコマンドを入力します。これにより、WinDbg は、シンボルファイルの最初の検索と読み込みを実行するように指示します。

   [**.reload**](-reload--reload-module-.md)

5. 読み込まれたモジュールの一覧を表示するには、次のコマンドを入力します。

   [**lm**](lm--list-loaded-modules-.md)

   出力は次のようになります。

   ```dbgcmd
   0:000>3: kd> lm
   start             end                 module name
   fffff800`00000000 fffff800`00088000   CI         (deferred)
   ...
   fffff800`01143000 fffff800`01151000   BasicRender   (deferred)
   fffff800`01151000 fffff800`01163000   BasicDisplay  (deferred)
   ...
   fffff800`02a0e000 fffff800`03191000   nt  (pdb symbols) C:\...\ntkrnlmp.pdb
   fffff800`03191000 fffff800`03200000   hal (deferred)
   ...
   ```

6. を実行している対象コンピューターを起動するには、次のコマンドを入力します。

   [**a-g-dl-p**](g--go-.md)

7. もう一度中断するには、[**デバッグ**] メニューの [**中断**] をクリックします。

8. \_Nt モジュールでファイルオブジェクトのデータ型を確認するには、次のコマンドを入力し \_ ます。

   [**dt nt! \_ファイル \_ オブジェクト**](dt--display-type-.md)

   出力は次のようになります。

   ```dbgcmd
   0:000>0: kd> dt nt!_FILE_OBJECT
      +0x000 Type             : Int2B
      +0x002 Size             : Int2B
      +0x008 DeviceObject     : Ptr64 _DEVICE_OBJECT
      +0x010 Vpb              : Ptr64 _VPB
      ...
      +0x0c0 IrpList          : _LIST_ENTRY
      +0x0d0 FileObjectExtension : Ptr64 Void
   ```

9. 次のコマンドを入力して、nt モジュール内のいくつかのシンボルを確認します。

   [**x nt! \*CreateProcess\***](x--examine-symbols-.md)

   出力は次のようになります。

   ```dbgcmd
   0:000>0: kd> x nt!*CreateProcess*
   fffff800`030821cc nt!ViCreateProcessCallbackInternal (<no parameter info>)
   ...
   fffff800`02e03904 nt!MmCreateProcessAddressSpace (<no parameter info>)
   fffff800`02cece00 nt!PspCreateProcessNotifyRoutine = <no type information>
   ...
   ```

10. 次のコマンドを入力して、 **MmCreateProcessAddressSpace**にブレークポイントを設定します。

    [**bu nt!MmCreateProcessAddressSpace**](bp--bu--bm--set-breakpoint-.md)

    ブレークポイントが設定されていることを確認するには、次のコマンドを入力します。

    [**bl**](bl--breakpoint-list-.md)

    出力は次のようになります。

    ```dbgcmd
    0:000>0: kd> bu nt!MmCreateProcessAddressSpace
    0: kd> bl
    0 e fffff800`02e03904     0001 (0001) nt!MmCreateProcessAddressSpace
    ```

    ターゲットコンピューターを実行するには、「 [**g**](g--go-.md) 」と入力します。

11. ターゲットコンピューターがすぐにデバッガーに侵入しない場合は、対象のコンピューターでいくつかの操作を実行します (たとえば、メモ帳を開きます)。 **MmCreateProcessAddressSpace**が呼び出されると、ターゲットコンピューターはデバッガーに中断します。 スタックトレースを表示するには、次のコマンドを入力します。

    [**.reload**](-reload--reload-module-.md)

    [**kb**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)

    出力は次のようになります。

    ```dbgcmd
    0:000>2: kd> k
    Child-SP          RetAddr           Call Site
    ffffd000`224b4c88 fffff800`02d96834 nt!MmCreateProcessAddressSpace
    ffffd000`224b4c90 fffff800`02dfef17 nt!PspAllocateProcess+0x5d4
    ffffd000`224b5060 fffff800`02b698b3 nt!NtCreateUserProcess+0x55b
    ...
    000000d7`4167fbb0 00007ffd`14b064ad KERNEL32!BaseThreadInitThunk+0xd
    000000d7`4167fbe0 00000000`00000000 ntdll!RtlUserThreadStart+0x1d
    ```

12. [**表示**] メニューの [**逆アセンブリ**] をクリックします。

    [**デバッグ**] メニューの [**ステップオーバー** ] をクリックするか、 **F10**キーを押します。 [逆アセンブル] ウィンドウを見ると、ステップコマンドを数回入力します。

13. 次のコマンドを入力して、ブレークポイントをクリアします。

    [**bc\***](bc--breakpoint-clear-.md)

    ターゲットコンピューターを実行するには、「 [**g**](g--go-.md) 」と入力します。 [**デバッグ**] メニューの [**中断**] をクリックするか、 **CTRL + break**キーを押して、もう一度中断します。

14. すべてのプロセスの一覧を表示するには、次のコマンドを入力します。

    [**! プロセス 0 0**](-process.md)

    出力は次のようになります。

    ```dbgcmd
    0:000>0: kd> !process 0 0
    **** NT ACTIVE PROCESS DUMP ****
    PROCESS ffffe000002287c0
        SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
        DirBase: 001aa000  ObjectTable: ffffc00000003000  HandleCount: <Data Not Accessible>
        Image: System

    PROCESS ffffe00001e5a900
        SessionId: none  Cid: 0124    Peb: 7ff7809df000  ParentCid: 0004
        DirBase: 100595000  ObjectTable: ffffc000002c5680  HandleCount: <Data Not Accessible>
        Image: smss.exe
    ...
    PROCESS ffffe00000d52900
        SessionId: 1  Cid: 0910    Peb: 7ff669b8e000  ParentCid: 0a98
        DirBase: 3fdba000  ObjectTable: ffffc00007bfd540  HandleCount: <Data Not Accessible>
        Image: explorer.exe
    ```

15. 1つのプロセスのアドレスをコピーし、次のコマンドを入力します。

    [**! プロセス***アドレス* **2**](-process.md)

    例: **! process ffffe00000d5290 2**

    出力には、プロセス内のスレッドが表示されます。

    ```dbgcmd
    0:000>0:000>0: kd> !process ffffe00000d52900 2
    PROCESS ffffe00000d52900
        SessionId: 1  Cid: 0910    Peb: 7ff669b8e000  ParentCid: 0a98
        DirBase: 3fdba000  ObjectTable: ffffc00007bfd540  HandleCount:
        Image: explorer.exe

            THREAD ffffe00000a0d880  Cid 0910.090c  Teb: 00007ff669b8c000
                ffffe00000d57700  SynchronizationEvent

            THREAD ffffe00000e48880  Cid 0910.0ad8  Teb: 00007ff669b8a000
                ffffe00000d8e230  NotificationEvent
                ffffe00000cf6870  Semaphore Limit 0xffff
                ffffe000039c48c0  SynchronizationEvent
            ...
            THREAD ffffe00000e6d080  Cid 0910.0cc0  Teb: 00007ff669a10000
                ffffe0000089a300  QueueObject
    ```

16. 1つのスレッドのアドレスをコピーし、次のコマンドを入力します。

    [**! スレッド***アドレス*](-thread.md)

    例: **! thread ffffe00000e6d080**

    出力には、個々のスレッドに関する情報が表示されます。

    ```dbgcmd
    0: kd> !thread ffffe00000e6d080
    THREAD ffffe00000e6d080  Cid 0910.0cc0  Teb: 00007ff669a10000 Win32Thread: 0000000000000000 WAIT: ...
        ffffe0000089a300  QueueObject
    Not impersonating
    DeviceMap                 ffffc000034e7840
    Owning Process            ffffe00000d52900       Image:         explorer.exe
    Attached Process          N/A            Image:         N/A
    Wait Start TickCount      13777          Ticks: 2 (0:00:00:00.031)
    Context Switch Count      2              IdealProcessor: 1
    UserTime                  00:00:00.000
    KernelTime                00:00:00.000
    Win32 Start Address ntdll!TppWorkerThread (0x00007ffd14ab2850)
    Stack Init ffffd00021bf1dd0 Current ffffd00021bf1580
    Base ffffd00021bf2000 Limit ffffd00021bec000 Call 0
    Priority 13 BasePriority 13 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5
    ...
    ```

17. プラグアンドプレイデバイスツリー内のすべてのデバイスノードを表示するには、次のコマンドを入力します。

    [**! devnode 0 1**](-devnode.md)

    ```dbgcmd
    0:000>0: kd> !devnode 0 1
    Dumping IopRootDeviceNode (= 0xffffe000002dbd30)
    DevNode 0xffffe000002dbd30 for PDO 0xffffe000002dc9e0
      InstancePath is "HTREE\ROOT\0"
      State = DeviceNodeStarted (0x308)
      Previous State = DeviceNodeEnumerateCompletion (0x30d)
      DevNode 0xffffe000002d9d30 for PDO 0xffffe000002daa40
        InstancePath is "ROOT\volmgr\0000"
        ServiceName is "volmgr"
        State = DeviceNodeStarted (0x308)
        Previous State = DeviceNodeEnumerateCompletion (0x30d)
        DevNode 0xffffe00001d49290 for PDO 0xffffe000002a9a90
          InstancePath is "STORAGE\Volume\{3007dfd3-df8d-11e3-824c-806e6f6e6963}#0000000000100000"
          ServiceName is "volsnap"
          TargetDeviceNotify List - f 0xffffc0000031b520  b 0xffffc0000008d0f0
          State = DeviceNodeStarted (0x308)
          Previous State = DeviceNodeStartPostWork (0x307)
    ...
    ```

18. ハードウェアリソースと共にデバイスノードを表示するには、次のコマンドを入力します。

    [**! devnode 0 9**](-devnode.md)

    ```dbgcmd
    0:000>...
            DevNode 0xffffe000010fa770 for PDO 0xffffe000010c2060
              InstancePath is "PCI\VEN_8086&DEV_2937&SUBSYS_2819103C&REV_02\3&33fd14ca&0&D0"
              ServiceName is "usbuhci"
              State = DeviceNodeStarted (0x308)
              Previous State = DeviceNodeEnumerateCompletion (0x30d)
              TranslatedResourceList at 0xffffc00003c78b00  Version 1.1  Interface 0x5  Bus #0
                Entry 0 - Port (0x1) Device Exclusive (0x1)
                  Flags (0x131) - PORT_MEMORY PORT_IO 16_BIT_DECODE POSITIVE_DECODE
                  Range starts at 0x3120 for 0x20 bytes
                Entry 1 - DevicePrivate (0x81) Device Exclusive (0x1)
                  Flags (0000) -
                  Data - {0x00000001, 0x00000004, 0000000000}
                Entry 2 - Interrupt (0x2) Shared (0x3)
                  Flags (0000) - LEVEL_SENSITIVE
                  Level 0x8, Vector 0x81, Group 0, Affinity 0xf
    ...
    ```

19. ディスクのサービス名を持つデバイスノードを表示するには、次のコマンドを入力します。

    [**! devnode 0 1 ディスク**](-devnode.md)

    ```dbgcmd
    0: kd> !devnode 0 1 disk
    Dumping IopRootDeviceNode (= 0xffffe000002dbd30)
    DevNode 0xffffe0000114fd30 for PDO 0xffffe00001159610
      InstancePath is "IDE\DiskST3250820AS_____________________________3.CHL___\5&14544e82&0&0.0.0"
      ServiceName is "disk"
      State = DeviceNodeStarted (0x308)
      Previous State = DeviceNodeEnumerateCompletion (0x30d)
    ...
    ```

20. [**! Devnode 0 1**](-devnode.md)の出力には、ノードの物理デバイスオブジェクト (PDO) のアドレスが表示されます。 物理デバイスオブジェクト (PDO) のアドレスをコピーし、次のコマンドを入力します。

    [**! devstack** *PdoAddress*](-devstack.md)

    例: <em>PdoAddress</em>**! devstack 0xffffe00001159610**

    ```dbgcmd
    0:000>0: kd> !devstack 0xffffe00001159610
      !DevObj           !DrvObj            !DevExt           ObjectName
      ffffe00001d50040  \Driver\partmgr    ffffe00001d50190  
      ffffe00001d51450  \Driver\disk       ffffe00001d515a0  DR0
      ffffe00001156e50  \Driver\ACPI       ffffe000010d8bf0  
    ```

21. ドライバーの disk.sys に関する情報を取得するには、次のコマンドを入力します。

    [**! drvobj disk 2**](-drvobj.md)

    ```dbgcmd
    0:000>0: kd> !drvobj disk 2
    Driver object (ffffe00001d52680) is for:
     \Driver\disk
    DriverEntry:   fffff800006b1270 disk!GsDriverEntry
    DriverStartIo: 00000000
    DriverUnload:  fffff800010b0b5c CLASSPNP!ClassUnload
    AddDevice:     fffff800010aa110 CLASSPNP!ClassAddDevice

    Dispatch routines:
    [00] IRP_MJ_CREATE                      fffff8000106d160    CLASSPNP!ClassGlobalDispatch
    [01] IRP_MJ_CREATE_NAMED_PIPE           fffff80002b0ab24    nt!IopInvalidDeviceRequest
    [02] IRP_MJ_CLOSE                       fffff8000106d160    CLASSPNP!ClassGlobalDispatch
    [03] IRP_MJ_READ                        fffff8000106d160    CLASSPNP!ClassGlobalDispatch
    ...
    [1b] IRP_MJ_PNP                         fffff8000106d160    CLASSPNP!ClassGlobalDispatch
    ```

22. ! Drvobj の出力には、ディスパッチルーチンのアドレスが表示されます。例: CLASSPNP!ClassGlobalDispatch。 ClassGlobalDispatch にブレークポイントを設定して確認するには、次のコマンドを入力します。

    [**bu CLASSPNP!ClassGlobalDispatch**](bp--bu--bm--set-breakpoint-.md)

    [**bl**](bl--breakpoint-list-.md)

    ターゲットコンピューターを実行するには、「g」と入力します。

    ターゲットコンピューターがすぐにデバッガーに侵入しない場合は、対象のコンピューターでいくつかの操作を実行します (たとえば、メモ帳を開き、ファイルを保存します)。 **Classglobaldispatch**が呼び出されると、ターゲットコンピューターはデバッガーに中断します。 スタックトレースを表示するには、次のコマンドを入力します。

    [**.reload**](-reload--reload-module-.md)

    [**kb**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)

    出力は次のようになります。

    ```dbgcmd
    2: kd> k
    Child-SP          RetAddr           Call Site
    ffffd000`21d06cf8 fffff800`0056c14e CLASSPNP!ClassGlobalDispatch
    ffffd000`21d06d00 fffff800`00f2c31d volmgr!VmReadWrite+0x13e
    ffffd000`21d06d40 fffff800`0064515d fvevol!FveFilterRundownReadWrite+0x28d
    ffffd000`21d06e20 fffff800`0064578b rdyboost!SmdProcessReadWrite+0x14d
    ffffd000`21d06ef0 fffff800`00fb06ad rdyboost!SmdDispatchReadWrite+0x8b
    ffffd000`21d06f20 fffff800`0085cef5 volsnap!VolSnapReadFilter+0x5d
    ffffd000`21d06f50 fffff800`02b619f7 Ntfs!NtfsStorageDriverCallout+0x16
    ...
    ```

23. デバッグセッションを終了するには、次のコマンドを入力します。

    [**qd**](qd--quit-and-detach-.md)

## <a name="summary-of-commands"></a>コマンドの概要

- [**ヘルプ**] メニューの [**コンテンツ**] コマンド
- [.sympath (シンボル パスの設定)](-sympath--set-symbol-path-.md)
- [.reload (モジュールの再読み込み)](-reload--reload-module-.md)
- [x (シンボルの検証)](x--examine-symbols-.md)
- [g (実行)](g--go-.md)
- [dt (型の表示)](dt--display-type-.md)
- [**デバッグ**] メニューの [**中断**] コマンド
- [lm (読み込まれたモジュールの一覧表示)](lm--list-loaded-modules-.md)
- [k (スタックバックトレースの表示)](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)
- [bu (ブレークポイントの設定)](bp--bu--bm--set-breakpoint-.md)
- [bl (ブレークポイントの一覧)](bl--breakpoint-list-.md)
- [bc (ブレークポイントのクリア)](bc--breakpoint-clear-.md)
- [**デバッグ**] メニューの [**ステップイン**] コマンド (**F11**)
- [! プロセス](-process.md)
- [! スレッド](-thread.md)
- [!devnode](-devnode.md)
- [!devstack](-devstack.md)
- [!drvobj](-drvobj.md)
- [qd (終了してデタッチ)](qd--quit-and-detach-.md)

## <a name="related-topics"></a>関連トピック

[WinDbg ドライバーの概要 (ユーザー モード)](getting-started-with-windbg.md)

[KDNET ネットワーク カーネル デバッグの自動設定](setting-up-a-network-debugging-connection-automatically.md)

[デバッガーの操作](debugger-operation-win8.md)

[デバッグの手法](debugging-techniques.md)

[Debugging Tools for Windows (WinDbg、KD、CDB、NTSD)](https://docs.microsoft.com/windows-hardware/drivers/debugger/)

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)
