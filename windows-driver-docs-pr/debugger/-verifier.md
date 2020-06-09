---
title: verifier
description: 検証ツールの拡張機能には、ドライバーの検証ツールとその操作の状態が表示されます。
ms.assetid: e84993e1-da10-4041-8fc7-7f40806ee454
keywords:
- ドライバーの検証ツール
- 検証ツール Windows デバッグ
ms.date: 05/03/2018
topic_type:
- apiref
api_name:
- verifier
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc02317b658136274865ddeea5f2c8a7e0fc3448
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534847"
---
# <a name="verifier"></a>!verifier


**! Verifier**拡張機能には、ドライバーの検証ツールとその操作の状態が表示されます。

ドライバーの検証ツールは Windows に含まれています。 オンとオフの両方のビルドで動作します。 ドライバーの検証機能の詳細については、Windows Driver Kit (WDK) のドキュメントの[ドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)に関するトピックを参照してください。

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

## <a name="span-idddk__verifier_dbgspanspan-idddk__verifier_dbgspanparameters"></a><span id="ddk__verifier_dbg"></span><span id="DDK__VERIFIER_DBG"></span>パラメータ


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*フラグ*   
このコマンドの出力に表示される情報を指定します。 *Flags*が値4、8、0x20、0x40、0x80、または0x100 と等しい場合、 **! verifier**の残りの引数は、これらの値に関連付けられている特定の引数に基づいて解釈されます。 *フラグ*がその他の値と等しい場合、これらのビットの1つ以上が設定されていても、*フラグ*と*イメージ*の引数のみが許可されます。 *フラグ*には、次のビットの合計を指定できます。既定値は0です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
検証されているすべてのドライバーの名前が表示されます。 ページングされていないプールとページプールから各ドライバーに現在割り当てられているバイト数も表示されます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
プール (プールサイズ、ヘッダー、およびプールタグ) と、アンロードされたドライバーによって残された未処理のメモリ割り当てに関する情報を表示します。 ビット 0 (0x1) も設定されていない限り、このフラグは無効です。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
フォールト挿入情報を表示します。 各割り当てを要求しているコードのリターンアドレス、シンボル名、および置き換えが表示されます。 *フラグ*が完全に0x4 で、 *Quantity*パラメーターが含まれている場合は、表示されているレコードの数を選択できます。 それ以外の場合は、4つのレコードが表示されます。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
検証されているドライバーによって行われた最新の IRQL の変更を表示します。 古い IRQL、新しい IRQL、プロセッサ、タイムスタンプが表示されます。 *フラグ*が完全に0x8 で、 *Quantity*パラメーターが含まれている場合は、表示されているレコードの数を選択できます。 それ以外の場合は、4つのレコードが表示されます。

**警告**   64ビットバージョンの Windows では、IRQL を上げ下げするカーネル関数の中には、エクスポート関数としてではなくインラインコードとして実装されているものがあります。 ドライバーの検証ツールは、インラインコードによって行われた IRQL の変化を報告しないため、ドライバーの検証ツールによって生成された IRQL 遷移ログが不完全になる可能性があります。 IRQL 遷移エントリの不足の例については、「解説」を参照してください。

 

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>ビット 6 (0x40)  
(Windows Vista 以降)強制保留中の Irp のログからのトレースを含め、Driver Verifier の**Force pending I/o Requests**オプションの情報を表示します。

*Quantity*パラメーターには、表示するトレースの数を指定します。 既定では、ログ全体が表示されます。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>ビット 7 (0x80)  
(Windows Vista 以降)カーネルプールの割り当て/空きログの情報を表示します。

*Quantity*パラメーターには、表示するトレースの数を指定します。 既定では、ログ全体が表示されます。

*アドレス*を指定すると、カーネルプールの割り当て/空きログ内の指定されたアドレスに関連付けられているトレースだけが表示されます。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>ビット 8 (0x100)  
(Windows Vista 以降)IoAllocateIrp、IoCompleteRequest、および Ioallocateirp 呼び出しのログの情報を表示します。

Quantity パラメーターには、表示するトレースの数を指定します。 既定では、ログ全体が表示されます。

*アドレス*が指定されている場合は、指定された IRP アドレスに関連付けられているトレースだけが表示されます。

<span id="Bit_9__0x200_"></span><span id="bit_9__0x200_"></span><span id="BIT_9__0X200_"></span>ビット 9 (0x200)  
(Windows Vista 以降)クリティカルな領域のログにエントリを表示します。

*Address*が指定されている場合、指定されたスレッドアドレスに関連付けられているエントリのみが表示されます。

<span id="Bit_10__0x400_"></span><span id="bit_10__0x400_"></span><span id="BIT_10__0X400_"></span>ビット 10 (0x400)  
(Windows Vista 以降)現在ドライバーの検証ツールによって監視されている取り消し済みの Irp を表示します。

*アドレス*を指定すると、指定したアドレスを持つ IRP のみが表示されます。

<span id="Bit_11__0x800_"></span><span id="bit_11__0x800_"></span><span id="BIT_11__0X800_"></span>ビット 11 (0x800)  
(Windows 8.1 以降)[体系的な低リソースシミュレーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/systematic-low-resource-simulation)オプションを選択したときに作成されたフォールトインジェクションログのエントリを表示します。

<span id="_______Image______"></span><span id="_______image______"></span><span id="_______IMAGE______"></span>*イメージ*   
*フラグ*が使用され、が4、8、または0x10 と等しくない場合、 *Image*はドライバーの名前を指定します。 *Image*は、 *Flags*値が0x1 および0x2 の場合に表示される情報をフィルター処理するために使用されます。指定されたドライバーのみが対象となります。 このドライバーは現在検証されている必要があります。

<span id="_______Quantity______"></span><span id="_______quantity______"></span><span id="_______QUANTITY______"></span>*数量*   
*フラグ*が0x4 と完全に等しい場合、 *Quantity*は、表示するフォールト挿入レコードの数を指定します。 *フラグ*が0x8 と同じである場合、 *Quantity*は表示する IRQL ログエントリの数を指定します。 *フラグ*が0x40 と同じ場合、 *Quantity*は、強制保留中の irp のログから表示されるトレースの数を指定します。 フラグが0x80 と厳密に等しい場合、Quantity はカーネルプールの割り当て/空きログから表示されるトレースの数を指定します。 フラグが0x100 と厳密に等しい場合、Quantity は、IoAllocateIrp、IoCompleteRequest、および Ioallocateirp 呼び出しのログから表示されるトレースの数を指定します。

<span id="_______-disable______"></span><span id="_______-DISABLE______"></span>**-disable**   
デバッグターゲットの現在のドライバーの検証の設定を消去します。 これらの設定をクリアしても、再起動によって保持されるわけではありません。 ドライバーの検証機能の設定を正常に起動するために無効にする必要がある場合は、nt! にブレークポイントを設定します。VerifierInitSystem を使用して、その時点で **! verifier-disable**コマンドを使用します。

<span id="______________"></span> **?**   
デバッガーコマンドウィンドウにこの拡張機能の簡単なヘルプテキストを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts .dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

[ドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)機能の詳細については、Windows driver KIT (WDK) のドキュメントを参照してください。


<a name="remarks"></a>注釈
-------

次の例は、64ビットバージョンの Windows では、IRQL 遷移ログが必ずしも完全ではないことを示しています。 表示される2つのエントリは、プロセッサ2のログの連続したエントリです。 最初のエントリは、2から0に向かう IRQL を示しています。 2番目のエントリは、2から2に向かう IRQL を示しています。 0から2の IRQL が発生した方法に関する情報がありません。

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

Driver Verifier を使用してグラフィックスドライバーをテストする場合は、 **! verifier**ではなく、 [**! gdikdx**](-gdikdx-verifier.md)拡張機能を使用します。

4、8、および0x20、0x40、0x80、および0x100 の値は、*フラグ*の特殊な値です。 これらの値が使用されている場合は、 **Parameters**セクションに示されている特殊な引数を使用できます。表示には、そのフラグ値に関連付けられている情報のみが含まれます。

*フラグ*に他の値が使用されている場合、これらのビットの1つ以上が設定されていても、*フラグ*と*イメージ*の引数のみが許可されます。 このような状況では、表示される他のすべての情報に加えて、 **! verifier**には、アクティブなドライバーの検証ツールのオプションと、プールの割り当て、IRQL の発生、スピンロック、およびトリムの統計が表示されます。

*フラグ*が0x20 の場合、[実行*時間*]、[ *Canceltime*]、および [ *ForceCancellation* ] に指定された値は、ドライバーの検証ツールの [ドライバーのハング検証] オプションで使用されます。 これらの新しい値は、次の起動時まで即座に有効になります。 再起動すると、既定値に戻ります。

また、*フラグ*が 0x20 (追加のパラメーターの有無にかかわらず) に等しい場合は、ドライバーのハング検証ログが出力されます。 ログの解釈の詳細については、Windows Driver Kit (WDK) のドキュメントにあるドライバーの検証ツールのドキュメントのドライバーのハング検証に関するセクションを参照してください。

Windows 7 コンピューターの **! verifier**拡張機能の例を次に示します。

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

次に示すのは、ビット7がオンになっていて*アドレス*が指定されている Windows Vista コンピューターの **! verifier**拡張機能の例です。

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

 

 





