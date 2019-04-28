---
title: WinDbg ドライバーの概要 (カーネル モード)
description: このトピックでは、カーネル モード デバッガーとして WinDbg を使用するのに役立つ実践的な演習を開始します。
ms.assetid: 1B61591F-0D48-4FBD-B242-68BB90D27FAF
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5c119aa1994b53ce79b7983bbee559455084b464
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362187"
---
# <a name="span-iddebuggergettingstartedwithwindbgkernel-modespangetting-started-with-windbg-kernel-mode"></a><span id="debugger.getting_started_with_windbg__kernel-mode_"></span>WinDbg (カーネル モード) の概要


WinDbg では、Windows のツールのデバッグに含まれるカーネル モードとユーザー モード デバッガーです。 ここで、カーネル モード デバッガーとして WinDbg を使用するのに役立つ実践的な演習を開始する提供されています。

Windows のツールのデバッグを取得する方法については、次を参照してください。[デバッグ ツールの Windows (WinDbg、KD、CDB、NTSD)](index.md)します。 デバッグ ツールをインストールした後は、64 ビット (x64) と、ツールの 32 ビット (x86) バージョンのインストール ディレクトリを見つけます。 以下に例を示します。

-   C:\\プログラム ファイル (x86)\\Windows キット\\8.1\\デバッガー\\x64
-   C:\\プログラム ファイル (x86)\\Windows キット\\8.1\\デバッガー\\x86

## <a name="span-idsetupakernel-modedebuggingspanspan-idsetupakernel-modedebuggingspanspan-idsetupakernel-modedebuggingspanset-up-a-kernel-mode-debugging"></a><span id="Set_up_a_kernel-mode_debugging"></span><span id="set_up_a_kernel-mode_debugging"></span><span id="SET_UP_A_KERNEL-MODE_DEBUGGING"></span>カーネル モード デバッグのセットアップします。


カーネル モードのデバッグ環境は、2 台のコンピューターを通常、:*ホスト コンピューター*と*ターゲット コンピューター*。 デバッガーは、ホスト コンピューターで実行し、ターゲット コンピューターでデバッグ中のコードを実行します。 ホストとターゲットは、デバッグ ケーブルで接続されます。

Windows デバッガーのデバッグ ケーブルのこれらの型をサポートします。

-   Ethernet
-   USB 2.0
-   USB 3.0
-   1394
-   シリアル (も呼び出されるヌル モデム)

8 またはそれ以降、ターゲット コンピューターが Windows を実行している場合は、デバッグ ケーブル、イーサネットなどの任意の型を使用することができます。 この図は、ホストとターゲットのコンピューターがイーサネット ケーブル経由でのデバッグのために接続を示しています。

![ホストとターゲットのイーサネット接続でのダイアグラム](images/configfortest01.png)

デバッグ イーサネットを使用することはできませんし、対象のコンピューターがウィンドウの 8 より前のバージョンの Windows を実行している場合1394、またはシリアル、USB を使用する必要があります。 この図は、USB、1394、またはシリアル デバッグ ケーブルで接続されたホストとターゲットのコンピューターを示しています。

![ホストとデバッグ ケーブルで対象のダイアグラム](images/configfortest02.png)

詳細については、ホストとターゲット コンピューターを設定する方法は、次を参照してください。[カーネル モード デバッグ手作業でセットアップ](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)します。

## <a name="span-idestablishakernel-modedebuggingsessionspanspan-idestablishakernel-modedebuggingsessionspanspan-idestablishakernel-modedebuggingsessionspanestablish-a-kernel-mode-debugging-session"></a><span id="Establish_a_kernel-mode_debugging_session"></span><span id="establish_a_kernel-mode_debugging_session"></span><span id="ESTABLISH_A_KERNEL-MODE_DEBUGGING_SESSION"></span>カーネル モードのデバッグ セッションを確立します。


ホストおよびターゲット コンピューターをセットアップしてデバッグ ケーブルで接続されていることと後、は、次の手順を設定する際に使用した同じトピック内で、カーネル モードのデバッグ セッションを確立できます。 たとえば、イーサネット経由のデバッグと、ホストとターゲット コンピューターを設定することを決定した場合は、カーネル モードのデバッグ セッションは、このトピックで確立するための手順を見つけることができます。

-   [デバッグが自動的に KDNET ネットワーク カーネルの設定](setting-up-a-network-debugging-connection-automatically.md)


## <a name="span-idgetstartedusingwindbgspanspan-idgetstartedusingwindbgspanspan-idgetstartedusingwindbgspanget-started-using-windbg"></a><span id="Get_started_using_WinDbg"></span><span id="get_started_using_windbg"></span><span id="GET_STARTED_USING_WINDBG"></span>WinDbg の使用を開始します。


1. ホスト コンピューターには、WinDbg を開き、対象のコンピューターに、カーネル モードのデバッグ セッションを確立します。
2. 、WinDbg で次のように選択します。**内容**から、**ヘルプ**メニュー。 デバッガーのドキュメントの CHM ファイルが開きます。 デバッガーのドキュメントは回線で利用できるも[ここ](index.md)します。
3. カーネル モードのデバッグ セッションを確立するときに WinDbg 可能性がありますの中断、ターゲット コンピューターに自動的にあります。 WinDbg 既に壊れていない場合、選択**中断**から、**デバッグ**メニュー。

4. コマンドラインで、WinDbg ウィンドウの下部の近くには、このコマンドを入力します。

   [**.sympath srv\\***](https://go.microsoft.com/fwlink/p?linkid=399238)

   出力は次のようにします。

   ```dbgcmd
   Symbol search path is: srv*
   Expanded Symbol search path is: cache*;SRV*https://msdl.microsoft.com/download/symbols
   ```

   シンボルの検索パスは、シンボル (PDB) ファイルを検索する場所を WinDbg に指示します。 デバッガーでは、シンボル ファイルのコード モジュール (関数名、変数名、およびなど) に関する情報を取得する必要があります。

   このコマンドは、最初に行う WinDbg に指示を入力します。 検索とシンボル ファイルの読み込み。

   [**.reload**](https://go.microsoft.com/fwlink/p?linkid=399239)

5. 読み込まれたモジュールの一覧を表示するには、このコマンドを入力します。

   [**lm**](https://go.microsoft.com/fwlink/p?linkid=399237)

   出力は次のようにします。

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

6. 実行しているターゲット コンピューターを起動するには、このコマンドを入力します。

   [**g**](https://go.microsoft.com/fwlink/p?linkid=399388)

7. もう一度解除、選択**Break**から、**デバッグ**メニュー。

8. 確認するには、このコマンドを入力して、\_ファイル\_nt モジュール内のデータ型のオブジェクト。

   [**dt nt!\_ファイル\_オブジェクト**](https://go.microsoft.com/fwlink/p?linkid=399397)

   出力は次のようにします。

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

9. Nt モジュールのシンボルのいくつかを確認するには、このコマンドを入力します。

   [**nt x!\*CreateProcess\\***](https://go.microsoft.com/fwlink/p?linkid=399240)

   出力は次のようにします。

   ```dbgcmd
   0:000>0: kd> x nt!*CreateProcess*
   fffff800`030821cc nt!ViCreateProcessCallbackInternal (<no parameter info>)
   ...
   fffff800`02e03904 nt!MmCreateProcessAddressSpace (<no parameter info>)
   fffff800`02cece00 nt!PspCreateProcessNotifyRoutine = <no type information>
   ...
   ```

10. ブレークポイントを配置するには、このコマンドを入力して**MmCreateProcessAddressSpace**:

    [**bu nt!MmCreateProcessAddressSpace**](https://go.microsoft.com/fwlink/p?linkid=399390)

    ブレークポイントが設定されていることを確認するには、このコマンドを入力します。

    [**bl**](https://go.microsoft.com/fwlink/p?linkid=399391)

    出力は次のようにします。

    ```dbgcmd
    0:000>0: kd> bu nt!MmCreateProcessAddressSpace
    0: kd> bl
    0 e fffff800`02e03904     0001 (0001) nt!MmCreateProcessAddressSpace
    ```

    入力[ **g** ](https://go.microsoft.com/fwlink/p?linkid=399388)実行対象のコンピュータをできるようにします。

11. 対象のコンピュータは中断されませんデバッガーにすぐに場合、は、いくつかのアクションをターゲット コンピューター (たとえば、メモ帳を開く) を実行します。 対象のコンピュータは、デバッガーを中断時に**MmCreateProcessAddressSpace**が呼び出されます。 スタック トレースを表示するには、これらのコマンドを入力します。

    [**.reload**](https://go.microsoft.com/fwlink/p?linkid=399239)

    [**k**](https://go.microsoft.com/fwlink/p?linkid=399389)

    出力は次のようにします。

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

12. **ビュー** ] メニューの [選択**逆アセンブル**します。

    **デバッグ**] メニューの [選択**ステップ オーバー** (またはキーを押します**F10**)。 入力ステップ コマンドをいくつか回逆アセンブル ウィンドウを見ながらします。

13. このコマンドを入力して、ブレークポイントをクリアします。

    [**ビジネス継続性 \\***](https://go.microsoft.com/fwlink/p?linkid=399401)

    入力[ **g** ](https://go.microsoft.com/fwlink/p?linkid=399388)実行対象のコンピュータをできるようにします。 選択してもう一度中断**中断**から、**デバッグ**メニューまたはキーを押して**Ctrl + break**します。

14. すべてのプロセスの一覧を表示するには、このコマンドを入力します。

    [**!process 0 0**](https://go.microsoft.com/fwlink/p?linkid=399241)

    出力は次のようにします。

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

15. 1 つのプロセスのアドレスをコピーし、このコマンドを入力します。

    [**! プロセス***アドレス* **2**](https://go.microsoft.com/fwlink/p?linkid=399241)

    例: **! プロセス ffffe00000d5290 2**

    プロセスのスレッドが出力されます。

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

16. 1 つのスレッドのアドレスをコピーし、このコマンドを入力します。

    [**! スレッド***アドレス*](https://go.microsoft.com/fwlink/p?linkid=399244)

    例: **! ffffe00000e6d080 スレッド**

    出力には、個々 のスレッドに関する情報が表示されます。

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

17. プラグ アンド プレイ デバイス ツリー内のすべてのデバイス ノードを表示するには、このコマンドを入力します。

    [**!devnode 0 1**](https://go.microsoft.com/fwlink/p?linkid=399242)

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

18. そのハードウェアのリソースと一緒にデバイス ノードを表示するには、このコマンドを入力します。

    [**!devnode 0 9**](https://go.microsoft.com/fwlink/p?linkid=399242)

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

19. ディスクのサービスの名前を持つデバイス ノードを表示するには、このコマンドを入力します。

    [**! devnode 0 1 ディスク**](https://go.microsoft.com/fwlink/p?linkid=399242)

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

20. 出力[ **! devnode 0 1** ](https://go.microsoft.com/fwlink/p?linkid=399242)ノードの物理デバイス オブジェクト (PDO) のアドレスが表示されます。 物理デバイス オブジェクト (PDO) のアドレスをコピーし、このコマンドを入力します。

    [**! devstack** *PdoAddress*](https://go.microsoft.com/fwlink/p?linkid=399245)

    次に、例を示します。<em>PdoAddress</em>**! devstack 0xffffe00001159610**

    ```dbgcmd
    0:000>0: kd> !devstack 0xffffe00001159610
      !DevObj           !DrvObj            !DevExt           ObjectName
      ffffe00001d50040  \Driver\partmgr    ffffe00001d50190  
      ffffe00001d51450  \Driver\disk       ffffe00001d515a0  DR0
      ffffe00001156e50  \Driver\ACPI       ffffe000010d8bf0  
    ```

21. ドライバー disk.sys に関する情報を取得するには、このコマンドを入力します。

    [**! drvobj ディスク 2**](https://go.microsoft.com/fwlink/p?linkid=399246)

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

22. 出力! drvobj ディスパッチ ルーチンのアドレスが表示されます: たとえば、CLASSPNP!ClassGlobalDispatch します。 ClassGlobalDispatch にブレークポイントを確認し、するには、これらのコマンドを入力します。

    [**bu CLASSPNP!ClassGlobalDispatch**](https://go.microsoft.com/fwlink/p?linkid=399390)

    [**bl**](https://go.microsoft.com/fwlink/p?linkid=399391)

    G を実行する対象のコンピュータを入力します。

    対象のコンピュータは中断されませんデバッガーにすぐに場合、は、ターゲット コンピューターに、いくつかの操作を実行 (メモ帳を開くし、ファイルの保存など)。 対象のコンピュータは、デバッガーを中断時に**ClassGlobalDispatch**が呼び出されます。 スタック トレースを表示するには、これらのコマンドを入力します。

    [**.reload**](https://go.microsoft.com/fwlink/p?linkid=399239)

    [**k**](https://go.microsoft.com/fwlink/p?linkid=399389)

    出力は次のようにします。

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

23. デバッグ セッションを終了するには、このコマンドを入力します。

    [**qd**](https://go.microsoft.com/fwlink/p?linkid=399394)

## <a name="span-idsummaryofcommandsspanspan-idsummaryofcommandsspanspan-idsummaryofcommandsspansummary-of-commands"></a><span id="Summary_of_commands"></span><span id="summary_of_commands"></span><span id="SUMMARY_OF_COMMANDS"></span>コマンドの概要


-   **内容**コマンドを**ヘルプ**メニュー
-   [.sympath (シンボル パスの設定)](https://go.microsoft.com/fwlink/p?linkid=399238)
-   [.reload (モジュールの再読み込み)](https://go.microsoft.com/fwlink/p?linkid=399239)
-   [x (シンボルの検証)](https://go.microsoft.com/fwlink/p?linkid=399240)
-   [g (移動)](https://go.microsoft.com/fwlink/p?linkid=399388)
-   [dt (表示の種類)](https://go.microsoft.com/fwlink/p?linkid=399397)
-   **中断**コマンドを**デバッグ**メニュー
-   [lm (読み込まれたモジュールを一覧表示)](https://go.microsoft.com/fwlink/p?linkid=399237)
-   [k (Display Stack Backtrace)](https://go.microsoft.com/fwlink/p?linkid=399389)
-   [bu (ブレークポイントの設定)](https://go.microsoft.com/fwlink/p?linkid=399390)
-   [bl (ブレークポイントの一覧)](https://go.microsoft.com/fwlink/p?linkid=399391)
-   [bc (ブレークポイント クリア)](https://go.microsoft.com/fwlink/p?linkid=399401)
-   **ステップ イン**コマンドを**デバッグ**メニュー (**F11**)
-   [! プロセス](https://go.microsoft.com/fwlink/p?linkid=399241)
-   [!thread](https://go.microsoft.com/fwlink/p?linkid=399244)
-   [! devnode](https://go.microsoft.com/fwlink/p?linkid=399242)
-   [! devstack](https://go.microsoft.com/fwlink/p?linkid=399245)
-   [!drvobj](https://go.microsoft.com/fwlink/p?linkid=399246)
-   [qd (Quit およびデタッチ)](https://go.microsoft.com/fwlink/p?linkid=399394)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WinDbg ドライバーの概要 (ユーザー モード)](getting-started-with-windbg.md)

[カーネル モードのデバッグを手動での設定](https://go.microsoft.com/fwlink/p?linkid=272138)

[デバッガーの操作](https://go.microsoft.com/fwlink/p?linkid=399247)

[デバッグの手法](https://go.microsoft.com/fwlink/p?linkid=399248)

[(WinDbg、KD、CDB、NTSD)、Windows 用デバッグ ツール](https://go.microsoft.com/fwlink/p?linkid=223405)

 

 






