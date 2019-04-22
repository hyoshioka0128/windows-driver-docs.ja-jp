---
title: pcr
description: Pcr 拡張機能は、特定のプロセッサ上のプロセッサ コントロール リージョン (PCR) の現在の状態を表示します。
ms.assetid: a9d82aa4-57de-4170-80fd-b7cd5b82f1e5
keywords:
- プロセッサのコントロールの領域 (PCR)
- pcr Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 018741ae2a8f28b7b29c55ca10b00f6564a5c5f5
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239213"
---
# <a name="pcr"></a>!pcr


**! Pcr**拡張機能は、特定のプロセッサのプロセッサ コントロール リージョン (PCR) の現在の状態を表示します。

```dbgcmd
!pcr [Processor]
```

## <a name="span-idddkpcrdbgspanspan-idddkpcrdbgspanparameters"></a><span id="ddk__pcr_dbg"></span><span id="DDK__PCR_DBG"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
PCR 情報を取得するプロセッサを指定します。 場合*プロセッサ*は省略すると、現在のプロセッサが使用されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>



### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

PCR、および、PRCB については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

プロセッサの制御ブロック (PRCB) は、PCR の拡張機能です。 表示できますが、 [ **! prcb** ](-prcb.md)拡張機能。

次の例に示します、 **! pcr** x86 拡張対象のコンピューター。

```dbgcmd
kd> !pcr 0
KPCR for Processor 0 at ffdff000:
    Major 1 Minor 1
      NtTib.ExceptionList: 801626e0
          NtTib.StackBase: 801628f0
         NtTib.StackLimit: 8015fb00
       NtTib.SubSystemTib: 00000000
            NtTib.Version: 00000000
        NtTib.UserPointer: 00000000
            NtTib.SelfTib: 00000000

                  SelfPcr: ffdff000
                     Prcb: ffdff120
                     Irql: 00000000
                      IRR: 00000000
                      IDR: ffffffff
            InterruptMode: 00000000
                      IDT: 80043400
                      GDT: 80043000
                      TSS: 803cc000

            CurrentThread: 8015e8a0
               NextThread: 00000000
               IdleThread: 8015e8a0

                DpcQueue:  0x80168ee0 0x80100d04 ntoskrnl!KiTimerExpiration
```

この表示でエントリの 1 つは、割り込み要求レベル (IRQL) を示しています。 **! Pcr**拡張機能は、IRQL が現在の IRQL は通常、関係のないくらい現在を示します。 直前に、バグを確認またはデバッガーの接続が存在していた IRQL はより興味深いものです。 によって表示されるこの[ **! irql**](-irql.md)、Windows Server 2003 または以降のバージョンの Windows を実行しているコンピューターに収録されてのみです。









