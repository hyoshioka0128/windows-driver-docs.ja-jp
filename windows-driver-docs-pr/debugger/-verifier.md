---
title: verifier
description: 検証拡張機能は、Driver Verifier とそのアクションの状態を表示します。
ms.assetid: e84993e1-da10-4041-8fc7-7f40806ee454
keywords:
- ドライバーの検証ツール
- Windows デバッグの検証ツール
ms.date: 05/03/2018
topic_type:
- apiref
api_name:
- verifier
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b6d34dc523b2e22ba854f1d4ade395862c60b29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362418"
---
# <a name="verifier"></a>!verifier


**! Verifier**拡張機能は、Driver Verifier とそのアクションの状態を表示します。

Driver Verifier は、Windows に含まれます。 オンで、無料のビルドで動作します。 Driver Verifier については、次を参照してください。、 [Driver Verifier](https://go.microsoft.com/fwlink/p/?linkid=120480) Windows Driver Kit (WDK) ドキュメントのトピックです。

構文

```dbgcmd
!verifier [Flags [Image]] 
!verifier 4 [Quantity] 
!verifier 8 [Quantity]  
!verifier 0x40 [Quantity] 
!verifier 0x80 [Quantity]
!verifier 0x80 Address
!verifier 0x100 [Quantity]
!verifier 0x100 Address
!verifier 0x200 [Address]
!verifier 0x400 [Address]
!verifier -disable
!verifier ?
```

## <a name="span-idddkverifierdbgspanspan-idddkverifierdbgspanparameters"></a><span id="ddk__verifier_dbg"></span><span id="DDK__VERIFIER_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
このコマンドの出力に表示される情報を指定します。 場合*フラグ*4、8、0x20、値と等しく、0x40、0x80、または 0x100、残りの引数を **! verifier**それらの値に関連付けられている特定の引数に基づいて解釈されます。 場合*フラグ*でもこれらのビットが 1 つ以上設定されている場合のみ、その他の値と等しいが、*フラグ*と*イメージ*引数が許可されます。 *フラグ*以下のビット値の合計を指定できます。 既定値は 0。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
検証されているすべてのドライバーの名前が表示されます。 非ページ プールとページ プールからドライバーごとに現在割り当てられているバイト数も表示されます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
プール (プールのサイズ、ヘッダー、およびプール タグ) とアンロードされたドライバーを左の未処理のメモリ割り当てに関する情報が表示されます。 ビット 0 (0x1) が設定されてもいない場合は、このフラグを指定しても効果はありません。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
フォールト インジェクションの情報が表示されます。 戻り値のアドレス、シンボル名、および各割り当てを要求するコードの移動距離が表示されます。 場合*フラグ*0x4 正確には、および*数量*パラメーターを含めると、表示されるこれらのレコードの数を選択できます。 それ以外の場合、4 つのレコードが表示されます。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
検証されているドライバーによって行われた最新の IRQL 変更を表示します。 古い IRQL、新しい IRQL、プロセッサ、およびタイムスタンプが表示されます。 場合*フラグ*0x8 正確には、および*数量*パラメーターを含めると、表示されるこれらのレコードの数を選択できます。 それ以外の場合、4 つのレコードが表示されます。

**警告**  のいくつかのカーネル関数は IRQL を上げたり下げたりするには、Windows の 64 ビット バージョンがエクスポートされた関数ではなくインライン コードとして実装されます。 Driver Verifier は、IRQL 移行ログが不完全になるドライバーの検証ツールによって生成される可能性がありますので、インライン コードによって行われたレポート IRQL 変更されません。 不足している IRQL 遷移エントリの例については、「解説」を参照してください。

 

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>ビット 6 (0x40)  
(Windows Vista 以降)情報が表示されます、 **Force 保留中の I/O 要求**保留中の Irp のログからのトレースを含む、Driver Verifier のオプションの強制します。

*数量*パラメーターを表示するトレースの数を指定します。 既定では、ログ全体が表示されます。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>ビット 7 (0x80)  
(Windows Vista 以降)カーネル プールの割り当て/空きログから情報を表示します。

*数量*パラメーターを表示するトレースの数を指定します。 既定では、ログ全体が表示されます。

場合*アドレス*を指定すると、カーネル プールの割り当て/空きログ内の指定したアドレスに関連付けられているトレースだけが表示されます。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>ビット 8 (0x100)  
(Windows Vista 以降)IoAllocateIrp、IoCompleteRequest および IoCancelIrp 呼び出しのログから情報を表示します。

数量のパラメーターには、表示するトレースの数を指定します。 既定では、ログ全体が表示されます。

場合*アドレス*を指定すると、指定した IRP アドレスに関連付けられているトレースだけが表示されます。

<span id="Bit_9__0x200_"></span><span id="bit_9__0x200_"></span><span id="BIT_9__0X200_"></span>ビット 9 (0x200)  
(Windows Vista 以降)クリティカル領域は、ログにエントリを表示します。

場合*アドレス*を指定すると、指定されたスレッドのアドレスに関連付けられたエントリだけが表示されます。

<span id="Bit_10__0x400_"></span><span id="bit_10__0x400_"></span><span id="BIT_10__0X400_"></span>ビット 10 (0x400)  
(Windows Vista 以降)表示には、Driver Verifier で現在監視されている Irp が取り消されました。

場合*アドレス*を指定すると、指定したアドレス IRP のみが表示されます。

<span id="Bit_11__0x800_"></span><span id="bit_11__0x800_"></span><span id="BIT_11__0X800_"></span>Bit 11 (0x800)  
(Windows 8.1 以降)選択したときに作成されるフォールト インジェクション ログからエントリを表示、[体系的な低リソース シミュレーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/systematic-low-resource-simulation)オプション。

<span id="_______Image______"></span><span id="_______image______"></span><span id="_______IMAGE______"></span> *イメージ*   
場合*フラグ*は使用され、4、8、または 0x10、等しくない*イメージ*ドライバーの名前を指定します。 *イメージ*によって表示される情報をフィルター処理するために使用*フラグ*0x1 と 0x2 の値。 指定されたドライバーのみを考慮します。 このドライバーは、現在検証する必要があります。

<span id="_______Quantity______"></span><span id="_______quantity______"></span><span id="_______QUANTITY______"></span> *数量*   
場合*フラグ*0x4 に正確に一致*数量*表示するフォールト インジェクションのレコードの数を指定します。 場合*フラグ*0x8 に正確に一致*数量*IRQL のログ エントリを表示する数を指定します。 場合*フラグ*0x40 に正確に一致*数量*強制的に保留中のログから表示されるトレースの数を指定します。 Irp します。 フラグが 0x80 に等しい場合は、数量にカーネル プールの割り当て/空きログから表示されるトレースの数を指定します。 フラグが 0x100 に等しい場合は、数量に IoAllocateIrp、IoCompleteRequest および IoCancelIrp 呼び出しのログから表示されるトレースの数を指定します。

<span id="_______-disable______"></span><span id="_______-DISABLE______"></span> **-を無効にします。**    
デバッグ対象の現在のドライバーの検証設定をクリアします。 これらの設定の消去は、再起動後に保持されません。 正常にブートするドライバーの検証設定を無効にする必要がある場合は、nt にブレークポイントを設定します。VerifierInitSystem を使用して、 **! verifier-を無効にする**その時点でコマンドします。

<span id="______________"></span> **?**    
デバッガー コマンド ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

について[Driver Verifier](https://go.microsoft.com/fwlink/p/?linkid=120480)、Windows Driver Kit (WDK) ドキュメントを参照してください。


<a name="remarks"></a>コメント
-------

次の例では、Windows の 64 ビット バージョンでは、IRQL の移行のログが常に不完全で示しています。 2 つの項目は、プロセッサ 2 のログの連続するエントリです。 最初のエントリは、2 から 0 へと向かう IRQL を示しています。 2 番目のエントリは、2 から 2 にしようとする IRQL を示しています。 IRQL を 2 に 0 から発生が状況に関する情報がありません。

```dbgcmd
Thread:             fffffa80068c9400
Old irql:           0000000000000002
New irql:           0000000000000000
Processor:          0000000000000002
Time stamp:         0000000000000857

    fffff8800140f12a ndis!ndisNsiGetInterfaceInformation+0x20a
    fffff88001509478 NETIO!NsiGetParameterEx+0x178
    fffff88005f062f2 nsiproxy!NsippGetParameter+0x24a
    fffff88005f086db nsiproxy!NsippDispatchDeviceControl+0xa3
    fffff88005f087a0 nsiproxy!NsippDispatch+0x48

Thread:             fffffa80068c9400
Old irql:           0000000000000002
New irql:           0000000000000002
Processor:          0000000000000002
Time stamp:         0000000000000857

    fffff8800140d48d ndis!ndisReferenceTopMiniportByNameForNsi+0x1ce
    fffff8800140f072 ndis!ndisNsiGetInterfaceInformation+0x152
    fffff88001509478 NETIO!NsiGetParameterEx+0x178
    fffff88005f062f2 nsiproxy!NsippGetParameter+0x24a
    fffff88005f086db nsiproxy!NsippDispatchDeviceControl+0xa3
```

Driver Verifier グラフィック ドライバーをテストするを使用するとき、 [ **! gdikdx.verifier** ](-gdikdx-verifier.md)拡張機能の **! verifier**します。

値は、4、8、および 0x20、0x40、0x80、0x100 の特殊な値は、*フラグ*します。 これらの値を使用している場合に、特別な引数が記載、**パラメーター**セクションを使用して、表示はそのフラグの値に関連付けられている情報のみが含まれます。

値の他の場合は*フラグ*でもこれらのビットが 1 つ以上設定されている場合のみ、使用、*フラグ*と*イメージ*引数が許可されます。 表示されているその他のすべての情報だけでなく、この状況で **! verifier**プールの割り当て、IRQL が発生、スピン ロック、およびトリミングに関する統計情報とともに、アクティブな Driver Verifier のオプションが表示されます。

場合*フラグ*0x20、指定した値に等しい*CompletionTime*、 *CancelTime*、および*ForceCancellation*ドライバーが使用されますDriver Verifier の確認オプションのハングします。 これらの新しい値は、次のブートまで、すぐに有効にし、最後を実行します。 コンピューターを再起動するときに、既定値に元に戻します。

また場合、*フラグ*0x20 に等しい (またはその他のパラメーターを指定せず)、ハングのドライバー検証ログが出力されます。 ログを解釈する方法の詳細については、Driver Verifier のドキュメントを Windows Driver Kit (WDK) ドキュメントでのドライバーのハングの検証セクションを参照してください。

次の例に示します、 **! verifier** Windows 7 コンピューター上で拡張します。

```dbgcmd
2: kd> !verifier 0xf

Verify Level 9bb ... enabled options are:
    Special pool
    Special irql
    All pool allocations checked on unload
    Io subsystem checking enabled
    Deadlock detection enabled
    DMA checking enabled
    Security checks enabled
    Miscellaneous checks enabled

Summary of All Verifier Statistics

RaiseIrqls                             0x0
AcquireSpinLocks                       0x362
Synch Executions                       0x0
Trims                                  0xa34a

Pool Allocations Attempted             0x7b058
Pool Allocations Succeeded             0x7b058
Pool Allocations Succeeded SpecialPool 0x7b058
Pool Allocations With NO TAG           0x0
Pool Allocations Failed                0x0
Resource Allocations Failed Deliberately   0x0

Current paged pool allocations         0x1a for 00000950 bytes
Peak paged pool allocations            0x1b for 00000AC4 bytes
Current nonpaged pool allocations      0xe3 for 00046110 bytes
Peak nonpaged pool allocations         0x10f for 00048E40 bytes

Driver Verification List

Entry     State           NonPagedPool   PagedPool   Module

fffffa8003b6f670 Loaded           000000a0       00000854    videoprt.sys

Current Pool Allocations  00000002    00000013
Current Pool Bytes        000000a0    00000854
Peak Pool Allocations     00000006    00000014
Peak Pool Bytes           000008c0    000009c8

PoolAddress  SizeInBytes    Tag       CallersAddress
fffff9800157efc0     0x0000003c     Vprt      fffff88002c62963
fffff9800146afc0     0x00000034     Vprt      fffff88002c62963
fffff980015bafe0     0x00000018     Vprt      fffff88002c628f7
...

fffffa8003b6f620 Loaded           00046070       000000fc    usbport.sys

Current Pool Allocations  000000e1    00000007
Current Pool Bytes        00046070    000000fc
Peak Pool Allocations     0000010d    0000000a
Peak Pool Bytes           00048da0    00000254

PoolAddress  SizeInBytes    Tag       CallersAddress
fffff98003a38fc0     0x00000038     usbp      fffff88004215e34
fffff98003a2cfc0     0x00000038     usbp      fffff88004215e34
fffff9800415efc0     0x00000038     usbp      fffff88004215e34
...

----------------------------------------------- 
Fault injection trace log                       
----------------------------------------------- 

Driver Verifier didn't inject any faults.

----------------------------------------------- 
Track irql trace log                            
----------------------------------------------- 

Displaying most recent 0x0000000000000004 entries from the IRQL transition log.
There are up to 0x100 entries in the log.

Thread:             fffff80002bf8c40
Old irql:           0000000000000002
New irql:           0000000000000002
Processor:          0000000000000000
Time stamp:         000000000000495e

    fffff8800420f2ca USBPORT!USBPORT_DM_IoTimerDpc+0x9a
    fffff80002a5b5bf nt!IopTimerDispatch+0x132
    fffff80002a7c29e nt!KiProcessTimerDpcTable+0x66
    fffff80002a7bdd6 nt!KiProcessExpiredTimerList+0xc6
    fffff80002a7c4be nt!KiTimerExpiration+0x1be

Thread:             fffff80002bf8c40
Old irql:           0000000000000002
New irql:           0000000000000002
Processor:          0000000000000000
Time stamp:         000000000000495e

    fffff88004205f3a USBPORT!USBPORT_AcquireEpListLock+0x2e
    fffff880042172df USBPORT!USBPORT_Core_TimeoutAllTransfers+0x1f
    fffff8800420f2ca USBPORT!USBPORT_DM_IoTimerDpc+0x9a
    fffff80002a5b5bf nt!IopTimerDispatch+0x132
    fffff80002a7c29e nt!KiProcessTimerDpcTable+0x66

Thread:             fffff80002bf8c40
Old irql:           0000000000000002
New irql:           0000000000000002
Processor:          0000000000000000
Time stamp:         000000000000495e

    fffff88004201694 USBPORT!MPf_CheckController+0x4c
    fffff8800420f26a USBPORT!USBPORT_DM_IoTimerDpc+0x3a
    fffff80002a5b5bf nt!IopTimerDispatch+0x132
    fffff80002a7c29e nt!KiProcessTimerDpcTable+0x66
    fffff80002a7bdd6 nt!KiProcessExpiredTimerList+0xc6

Thread:             fffff80002bf8c40
Old irql:           0000000000000002
New irql:           0000000000000002
Processor:          0000000000000000
Time stamp:         000000000000495e

    fffff8800420167c USBPORT!MPf_CheckController+0x34
    fffff8800420f26a USBPORT!USBPORT_DM_IoTimerDpc+0x3a
    fffff80002a5b5bf nt!IopTimerDispatch+0x132
    fffff80002a7c29e nt!KiProcessTimerDpcTable+0x66
    fffff80002a7bdd6 nt!KiProcessExpiredTimerList+0xc6
```

次の例に示します、 **! verifier**ビットがオンの 7 と Windows Vista コンピューター上で拡張と*アドレス*指定します。

```dbgcmd
0: kd> !verifier 80 a2b1cf20
# Parsing 00004000 array entries, searching for address a2b1cf20.

Pool block a2b1ce98, Size 00000168, Thread a2b1ce98
808f1be6 ndis!ndisFreeToNPagedPool+0x39
808f11c1 ndis!ndisPplFree+0x47
808f100f ndis!NdisFreeNetBufferList+0x3b
8088db41 NETIO!NetioFreeNetBufferAndNetBufferList+0xe
8c588d68 tcpip!UdpEndSendMessages+0xdf
8c588cb5 tcpip!UdpSendMessagesDatagramsComplete+0x22
8088d622 NETIO!NetioDereferenceNetBufferListChain+0xcf
8c5954ea tcpip!FlSendNetBufferListChainComplete+0x1c
809b2370 ndis!ndisMSendCompleteNetBufferListsInternal+0x67
808f1781 ndis!NdisFSendNetBufferListsComplete+0x1a
8c04c68e pacer!PcFilterSendNetBufferListsComplete+0xb2
809b230c ndis!NdisMSendNetBufferListsComplete+0x70
# 8ac4a8ba test1!HandleCompletedTxPacket+0xea

Pool block a2b1ce98, Size 00000164, Thread a2b1ce98
822af87f nt!VerifierExAllocatePoolWithTagPriority+0x5d
808f1c88 ndis!ndisAllocateFromNPagedPool+0x1d
808f11f3 ndis!ndisPplAllocate+0x60
808f1257 ndis!NdisAllocateNetBufferList+0x26
80890933 NETIO!NetioAllocateAndReferenceNetBufferListNetBufferMdlAndData+0x14
8c5889c2 tcpip!UdpSendMessages+0x503
8c05c565 afd!AfdTLSendMessages+0x27
8c07a087 afd!AfdTLFastDgramSend+0x7d
8c079f82 afd!AfdFastDatagramSend+0x5ae
8c06f3ea afd!AfdFastIoDeviceControl+0x3c1
8217474f nt!IopXxxControlFile+0x268
821797a1 nt!NtDeviceIoControlFile+0x2a
8204d16a nt!KiFastCallEntry+0x127
```

 

 





