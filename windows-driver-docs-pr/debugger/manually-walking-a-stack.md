---
title: スタックの手動ウォーク
description: スタックの手動ウォーク
ms.assetid: 9235fe4d-3e94-4143-867f-18b696e489d0
keywords:
- スタック トレースを手動でスタックのウォーク
- スタックのウォーク
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcb994d4b0641161ecf7c3bd7bdf7a6af253609e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383294"
---
# <a name="manually-walking-a-stack"></a>スタックの手動ウォーク


## <span id="ddk_manually_walking_a_stack_dbg"></span><span id="DDK_MANUALLY_WALKING_A_STACK_DBG"></span>


場合によっては、スタック トレースの関数は、デバッガーで失敗します。 これは、デバッガーは、リターン アドレスの場所が失われる原因となった無効なアドレスへの呼び出しによって発生することができます。スタック トレースでは; を取得できません直接スタック ポインター間で至ったまたはまたは、その他のデバッガーの問題があります。 いずれの場合も、スタックを手動で移動できること、多くの場合、重要です。

基本的な概念としては非常に単純: スタック ポインターをダンプ、モジュールが読み込まれる確認、考えられる関数のアドレスを確認および考えられるスタックの各エントリが次の呼び出しを実行するかどうかを確認することを確認します。

重要な点は、例を説明する前に、 [ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドは、Intel システムで追加の機能が。 Kb の手順を実行して =\[ebp\] \[eip\] \[esp\]デバッガーの基本ポインター、命令ポインター、およびスタック ポインターの場合は、特定の値を持つフレームのスタック トレースが表示されますそれぞれします。

例については、最後に、結果をチェックできるように、スタック トレースは、実際に障害が使用されます。

最初の手順では、どのようなモジュールを読み込むに場所を確認します。 これを行うと、 [ **(シンボルを調べる) x** ](x--examine-symbols-.md)コマンド (一部のシンボルが編集された長さの上の理由から)。

```dbgcmd
kd> x *! 
start    end        module name
77f70000 77fb8000   ntdll     (C:\debug\ntdll.dll, \\ntstress\symbols\dll\ntdll.DBG)
80010000 80012320   Aha154x   (load from Aha154x.sys deferred)
80013000 8001aa60   SCSIPORT  (load from SCSIPORT.SYS deferred)
8001b000 8001fba0   Scsidisk  (load from Scsidisk.sys deferred)

80100000 801b7b40   NT        (ntoskrnl.exe, \\ntstress\symbols\exe\ntoskrnl.DBG)
802f0000 8033c000   Ntfs      (load from Ntfs.sys deferred)
80400000 8040c000   hal       (load from hal.dll deferred)
fe4c0000 fe4c38c0   vga       (load from vga.sys deferred)
fe4d0000 fe4d3e60   VIDEOPRT  (load from VIDEOPRT.SYS deferred)
fe4e0000 fe4f0e40   ati       (load from ati.SYS deferred)
fe500000 fe5057a0   Msfs      (load from Msfs.SYS deferred)
fe510000 fe519560   Npfs      (load from Npfs.SYS deferred)

fe520000 fe521f60   ndistapi  (load from ndistapi.sys deferred)
fe530000 fe54ed20   Fastfat   (load from Fastfat.SYS deferred)
fe5603e0 fe575360   NDIS      (NDIS.SYS, \\ntstress\symbols\SYS\NDIS.DBG)
fe580000 fe585920   elnkii    (elnkii.sys, \\ntstress\symbols\sys\elnkii.DBG)
fe590000 fe59b8a0   ndiswan   (load from ndiswan.sys deferred)
fe5a0000 fe5b7c40   nbf       (load from nbf.sys deferred)
fe5c0000 fe5c1b40   TDI       (load from TDI.SYS deferred)
fe5d0000 fe5dd580   nwlnkipx  (load from nwlnkipx.sys deferred)

fe5e0000 fe5ee220   nwlnknb   (load from nwlnknb.sys deferred)
fe5f0000 fe5fb320   afd       (load from afd.sys deferred)
fe610000 fe62bf00   tcpip     (load from tcpip.sys deferred)
fe630000 fe648600   netbt     (load from netbt.sys deferred)
fe650000 fe6572a0   netbios   (load from netbios.sys deferred)
fe660000 fe660000   Parport   (load from Parport.SYS deferred)
fe670000 fe670000   Parallel  (load from Parallel.SYS deferred)
fe680000 fe6bcf20   rdr       (rdr.sys, \\ntstress\symbols\sys\rdr.DBG)

fe6c0000 fe6f0920   srv       (load from srv.sys deferred) 
```

2 番目の手順で指定されたモジュール内のアドレスを検索するスタック ポインターがダンプ、 **x \*!** コマンド:

```dbgcmd
kd> dd esp 
fe4cc97c  80136039 00000270 00000000 00000000
fe4cc98c  fe682ae4 801036fe 00000000 fe68f57a
fe4cc99c  fe682a78 ffb5b030 00000000 00000000
fe4cc9ac  ff680e08 801036fe 00000000 00000000
fe4cc9bc  fe6a1198 00000001 fe4cca78 ffae9d98

fe4cc9cc  02000901 fe4cca68 ffb50030 ff680e08
fe4cc9dc  ffa449a8 8011c901 fe4cca78 00000000
fe4cc9ec  80127797 80110008 00000246 fe6a1430

kd> dd 
fe4cc9fc  00000270 fe6a10ae 00000270 ffa44abc
fe4cca0c  ffa449a8 ff680e08 fe6b2c04 ff680e08
fe4cca1c  ffa449a8 e12820c8 e1235308 ffa449a8
fe4cca2c  fe685968 ff680e08 e1235308 ffa449a8
fe4cca3c  ffb0ad48 ffb0ad38 00100000 ffb0ad38
fe4cca4c  00000000 ffa44a84 e1235308 0000000a
fe4cca5c  c00000d6 00000000 004ccb28 fe4ccbc4

fe4cca6c  fe680ba4 fe682050 00000000 fe4ccbd4 
```

可能性が高い関数の値を判断するアドレスとが、パラメーターまたは最初に検討することは保存済みレジスタ、スタックのさまざまな種類の情報がどのようにします。 ほとんどの整数は、(0x00000270) のような Dword として表示されるときにほとんど 0 になるためより小さい値になります。 ほとんどのポインターをローカル アドレスには、(fe4cca78) などのスタック ポインターの近くになります。 状態コードは、通常は c (c00000d6) で始まります。 Unicode および ASCII 文字列は、20 ~ 7 f の範囲内の各文字があるという事実によって識別できます。 (KD で、 [ **dc (表示メモリ)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドは、右の文字を表示します)。最も重要なは、関数のアドレスが、範囲ごとに一覧表示になります。 **x \*!** します。

8040 c 000 77f70000 と fe6f0920 に fe4c0000 の範囲内にリストされているすべてのモジュールがあることを確認します。 上記の考えられる関数のアドレスは、しますこれらの範囲に基づいて。80136039、801036fe (可能性が高いため、2 回記載パラメーター)、fe682ae4、fe68f57a、fe682a78、fe6a1198、8011 c 901、80127797、80110008、fe6a1430、fe6a10ae、fe6b2c04、fe685968、fe680ba4、fe682050 とします。 使用してこれらの場所を調査、 [ **ln (最も近いシンボルの一覧)** ](ln--list-nearest-symbols-.md)コマンドでは、各アドレス。

```dbgcmd
kd> ln 80136039 
(80136039)   NT!_KiServiceExit+0x1e  |  (80136039)   NT!_KiServiceExit2-0x177
kd> ln fe682ae4 
(fe682ae4)   rdr!_RdrSectionInfo+0x2c | (fe682ae4)   rdr!_RdrFcbReferenceLock-0xb4
kd> ln 801036fe 
(801036fe)   NT!_KeWaitForSingleObject | (801036fe)   NT!_MmProbeAndLockPages-0x2f8
kd> ln fe68f57a 
(fe68f57a)   rdr!_RdrDereferenceDiscardableCode+0xb4  
                         (fe68f57a)   rdr!_RdrUninitializeDiscardableCode-0xa
kd> ln fe682a78 
(fe682a78)   rdr!_RdrDiscardableCodeLock | (fe682a78) rdr!_RdrDiscardableCodeTimeout-0x38

kd> ln fe6a1198 
(fe6a1198)   rdr!_SubmitTdiRequest+0xae | (fe6a1198)   rdr!_RdrTdiAssociateAddress-0xc
kd> ln 8011c901 
(8011c901)   NT!_KeSuspendThread+0x13 | (8011c901)   NT!_FsRtlCheckLockForReadAccess-0x55
kd> ln 80127797 
(80127797)   NT!_ZwCloseObjectAuditAlarm+0x7 | (80127797)   NT!_ZwCompleteConnectPort-0x9
kd> ln 80110008 
(80110008)   NT!_KeWaitForMultipleObjects+0x27c | (80110008) NT!_FsRtlLookupMcbEntry-0x164
kd> ln fe6a1430 
(fe6a1430)   rdr!_RdrTdiCloseConnection+0xa | (fe6a1430)   rdr!_RdrDoTdiConnect-0x4

kd> ln fe6a10ae 
(fe6a10ae)   rdr!_RdrTdiDisconnect+0x56 | (fe6a10ae)   rdr!_SubmitTdiRequest-0x3c
kd> ln fe6b2c04 
(fe6b2c04)   rdr!_CleanupTransportConnection+0x64 | (fe6b2c04)rdr!_RdrReferenceServer-0x20
kd> ln fe685968 
(fe685968)   rdr!_RdrReconnectConnection+0x1b6
                        (fe685968)   rdr!_RdrInvalidateServerConnections-0x32
kd> ln fe682050 
(fe682050)   rdr!__strnicmp+0xaa  |  (fe682050)   rdr!_BackPackSpinLock-0xa10 
```

前述したとおり、801036fe が 2 回記載されているとスタック トレースの一部である可能性があります。 戻り値のアドレスのオフセットが 0 の場合は、それらは無視できます (関数の先頭に戻ることはできません)。 この情報に基づいて、あるスタック トレースが表示されました。

```dbgcmd
NT!_KiServiceExit+0x1e
rdr!_RdrSectionInfo+0x2c
rdr!_RdrDereferenceDiscardableCode+0xb4  
rdr!_SubmitTdiRequest+0xae
NT!_KeSuspendThread+0x13
NT!_ZwCloseObjectAuditAlarm+0x7
NT!_KeWaitForMultipleObjects+0x27c
rdr!_RdrTdiCloseConnection+0xa
rdr!_RdrTdiDisconnect+0x56
rdr!_CleanupTransportConnection+0x64
rdr!_RdrReconnectConnection+0x1b6
rdr!__strnicmp+0xaa 
```

各シンボルを確認するには、指定するかどうかは、上記の関数の呼び出しを参照してください。 差出人住所の直前に逆アセンブルします。 次の編集長を減らすためには、(使用されるオフセットを試行錯誤で見つかりました)。

```dbgcmd
kd> u 80136039-2 l1      //  looks ok, its a call
NT!_KiServiceExit+0x1c:
80136037 ffd3             call    ebx
kd> u fe682ae4-2 l1      //  paged out (all zeroes) unknown
rdr!_RdrSectionInfo+0x2a:
fe682ae2 0000             add     [eax],al
kd> u fe68f57a-6 l1      //  looks ok, its a call, but not anything above
rdr!_RdrDereferenceDiscardableCode+0xae:
fe68f574 ff15203568fe     call dword ptr [rdr!__imp__ExReleaseResourceForThreadLite]
kd> u fe682a78-6 l1      //  paged out (all zeroes) unknown

rdr!_DiscCodeInitialized+0x2:
fe682a72 0000             add     [eax],al
kd> u  fe6a1198-5 l1      //  looks good, call to something above
rdr!_SubmitTdiRequest+0xa9:
fe6a1193 e82ee3feff       call  rdr!_RdrDereferenceDiscardableCode (fe68f4c6)
kd> u 8011c901-2 l1      //  not good, its a jump in the function
NT!_KeSuspendThread+0x11:
8011c8ff 7424             jz      NT!_KeSuspendThread+0x37 (8011c925)
kd> u 80127797-2 l1      //  looks good, an int 2e -> KiServiceExit

NT!_ZwCloseObjectAuditAlarm+0x5:
80127795 cd2e             int     2e
kd> u 80110008-2 l1      //  not good, its a test instruction not a call
NT!_KeWaitForMultipleObjects+0x27a:
80110006 85c9             test    ecx,ecx
kd> u 80110008-5 l1      //  paged out (all zeroes) unknown
NT!_KeWaitForMultipleObjects+0x277:
80110003 0000             add     [eax],al
kd> u fe6a1430-6 l1      //  looks good its a call to ZwClose...
rdr!_RdrTdiCloseConnection+0x4:
fe6a142a ff15f83468fe     call    dword ptr [rdr!__imp__ZwClose (fe6834f8)]

kd> u fe6a10ae-2 l1      //  paged out (all zeroes) unknown
rdr!_RdrTdiDisconnect+0x54:
fe6a10ac 0000             add     [eax],al
kd> u  fe6b2c04-5 l1      //  looks good, call to something above
rdr!_CleanupTransportConnection+0x5f:
fe6b2bff e854e4feff       call    rdr!_RdrTdiDisconnect (fe6a1058)
kd> u fe685968-5 l1      //  looks good, call to immediately above
rdr!_RdrReconnectConnection+0x1b1:
fe685963 e838d20200       call    rdr!_CleanupTransportConnection (fe6b2ba0)

kd> u fe682050-2 l1      //  paged out (all zeroes) unknown
rdr!__strnicmp+0xa8:
fe68204e 0000             add     [eax],al 
```

これに基づいて、表示される**RdrReconnectConnection**と呼ばれる**RdrCleanupTransportConnection**を**RdrTdiDisconnect**を**ZwCloseObjectAuditAlarm**を**KiSystemServiceExit**します。 スタック上の他の関数は、以前にアクティブなスタックの部分が残っている可能性があります。

この場合、スタック トレースが正しく動作します。 解答を確認する実際のスタック トレースを次に示します。

```dbgcmd
kd> k 
ChildEBP RetAddr
fe4cc978 80136039 NT!_NtClose+0xd
fe4cc978 80127797 NT!_KiServiceExit+0x1e

fe4cc9f4 fe6a1430 NT!_ZwCloseObjectAuditAlarm+0x7
fe4cca10 fe6b2c04 rdr!_RdrTdiCloseConnection+0xa
fe4cca28 fe685968 rdr!_CleanupTransportConnection+0x64
fe4cca78 fe688157 rdr!_RdrReconnectConnection+0x1b6
fe4ccbd4 80106b1e rdr!_RdrFsdCreate+0x45b
fe4ccbe8 8014b289 NT!IofCallDriver+0x38
fe4ccc98 8014decd NT!_IopParseDevice+0x693
fe4ccd08 8014d6d2 NT!_ObpLookupObjectName+0x487
fe4ccde4 8014d3ad NT!_ObOpenObjectByName+0xa2
fe4cce90 8016660d NT!_IoCreateFile+0x433
fe4cced0 80136039 NT!_NtCreateFile+0x2d 
```

最初のエントリが現在の場所は、スタック トレースに基づくが、それ以外の場合、スタックされた時点まで適切な場所**RdrReconnectConnection**が呼び出されました。 同じプロセスは、スタック全体をトレースに使用されている可能性があります。 手動のスタック ウォークのより正確なメソッドでは、各潜在的な関数を逆アセンブルし、次の各する必要は**プッシュ**と**pop**スタック上の各 DWORD を識別するためにします。

 

 





