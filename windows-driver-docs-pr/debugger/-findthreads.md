---
title: findthreads
description: Findthreads 拡張機能は、指定された検索条件に基づいて、ターゲット システム上の 1 つまたは複数のスレッドに関する概要情報を表示します。
ms.assetid: ED14E503-0AF2-4444-81B0-7E00A6E424E5
keywords:
- Windows デバッグ findthreads
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- findthreads
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3d8de83a1055a9af0c0e6a8cc0efc810951365fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336747"
---
# <a name="findthreads"></a>!findthreads


! Findthreads 拡張機能では、指定された検索条件に基づいて、ターゲット システムに 1 つまたは複数のスレッドに関する概要情報が表示されます。 関連付けられている stack(s)、指定したオブジェクトを参照するときに、スレッドの情報が表示されます。 このコマンドは、カーネル モードのデバッグ中にのみ使用できます。

構文

```dbgcmd
!findthreads [-v][-t  <Thread Address>|-i <IRP Address>|-d <Device Address>|( -a <Pointer Address> -e <End Address> | -l <Range Length>)] 
```

## <a name="span-idddkthreaddbgspanspan-idddkthreaddbgspanparameters"></a><span id="ddk__thread_dbg"></span><span id="DDK__THREAD_DBG"></span>パラメーター


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
すべての条件と一致する詳細な情報が表示されます。

<span id="_______-t_Thread_Address______"></span><span id="_______-t_thread_address______"></span><span id="_______-T_THREAD_ADDRESS______"></span> **-t** **** *スレッド アドレス*   
検索条件では、すべてのモジュール、待機オブジェクト、および Irp をスレッドだけでなくデバイス オブジェクトと接続されている Irp から生成されたモジュールになります。 このオプションは広範な検索条件を一般に提供します。

<span id="_______-i_IRP_Address____________"></span><span id="_______-i_irp_address____________"></span><span id="_______-I_IRP_ADDRESS____________"></span> **-i** **** *IRP アドレス*   
検索条件は、すべてのモジュールと IRP 自体への参照と、指定の IRP では、デバイスになります。

<span id="_______-d_Device_Address____________"></span><span id="_______-d_device_address____________"></span><span id="_______-D_DEVICE_ADDRESS____________"></span> **-d** **** *デバイス アドレス*   
デバイス オブジェクトから、検索条件を基にします。 これは、(ドライバー オブジェクトにある) を使用してデバイス オブジェクトに関連付けられているモジュールが含まれて、デバイスの拡張機能のいずれかのデバイス オブジェクトにアタッチされている同様の情報とデバイスに任意の IRP がアタッチされています。

<span id="_______-a_Pointer_Address____________"></span><span id="_______-a_pointer_address____________"></span><span id="_______-A_POINTER_ADDRESS____________"></span> **-** **** *ポインター アドレス*   
ベース アドレスを基準に追加します。 E - または -l が正しく指定されて、この値がメモリの範囲のベースになります。 それ以外の場合、ポインターとして解釈されます。

<span id="_______-e_End_Address____________"></span><span id="_______-e_end_address____________"></span><span id="_______-E_END_ADDRESS____________"></span> **-e** **** *終了アドレス*   
-A で指定したメモリ範囲の終了アドレスを指定します。

<span id="_______-l_Range_Length______"></span><span id="_______-l_range_length______"></span><span id="_______-L_RANGE_LENGTH______"></span> **-l** **** *長さの範囲*   
-A で指定されたメモリ範囲の長さを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 10 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スレッドがカーネル モードについては、次を参照してください。[変更コンテキスト](changing-contexts.md)します。 プロセスとスレッドの分析に関する詳細については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

-V と-t オプションを使用して出力の例を次に示します。

```dbgcmd
kd> !findthreads -v -t ffffd001ee29cdc0

Added criterion for THREAD 0xffffd001ee29cdc0
  Added criterion for THREAD STACK 0xffffd001ee2bac20
  ERROR: Object 0xffffffffffffffe0 is not an IRP
ERROR: unable to completely walk thread IRP list.
  Added criterion for MODULE kdnic(0xfffff80013120000)

Found 63 threads matching the search criteria

Found 6 criteria matches for THREAD 0xffffe0016a383740, PROCESS 0xffffe0016a220200
  Kernel stack location 0xffffd001f026a0c0 references THREAD 0xffffd001ee29cdc0
  Kernel stack location 0xffffd001f026a418 references THREAD 0xffffd001ee29cdc0
  Kernel stack location 0xffffd001f026a460 references THREAD 0xffffd001ee29cdc0
  Kernel stack location 0xffffd001f026a4d0 references THREAD 0xffffd001ee29cdc0
  Kernel stack location 0xffffd001f026a4f0 references THREAD 0xffffd001ee29cdc0
  Kernel stack location 0xffffd001f026a670 references THREAD 0xffffd001ee29cdc0


    ffffd001f026a0e0 nt!KiSwapContext+76
    ffffd001f026a190 nt!KiSwapThread+1c8
    ffffd001f026a220 nt!KiCommitThreadWait+148
    ffffd001f026a2e0 nt!KeWaitForMultipleObjects+21e
    ffffd001f026a800 nt!ObWaitForMultipleObjects+2b7
    ffffd001f026aa80 nt!NtWaitForMultipleObjects+f6
    000000c8d220fa98 nt!KiSystemServiceCopyEnd+13
    000000c8d220fa98 ntdll!ZwWaitForMultipleObjects+a
... 
```

 

 





