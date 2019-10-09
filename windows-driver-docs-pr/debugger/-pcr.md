---
title: pcr
description: Pcr 拡張機能には、特定のプロセッサのプロセッサ制御領域 (PCR) の現在の状態が表示されます。
ms.assetid: a9d82aa4-57de-4170-80fd-b7cd5b82f1e5
keywords:
- プロセッサ制御領域 (PCR)
- pcr Windows デバッグ
ms.date: 10/07/2019
topic_type:
- apiref
api_name:
- pcr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fefa5fa4d1d96ead2184c517e89d564535bc2388
ms.sourcegitcommit: bff7fdcac628f8b62bd9df2658ca56301d1f8b07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72030801"
---
# <a name="pcr"></a>!pcr


**! Pcr**拡張機能は、特定のプロセッサのプロセッサ制御領域 (pcr) の現在の状態を表示します。

```dbgcmd
!pcr [Processor]
```

## <a name="span-idddk__pcr_dbgspanspan-idddk__pcr_dbgspanparameters"></a><span id="ddk__pcr_dbg"></span><span id="DDK__PCR_DBG"></span>パラメータ


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*プロセッサ*   
PCR 情報を取得するプロセッサを指定します。 *プロセッサ*を省略した場合は、現在のプロセッサが使用されます。

> [!NOTE]
> このコマンドは現在サポートされていないため、正しくない出力が表示される場合があります。
>

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>



### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

PCR と PRCB の詳細については、「 *Microsoft Windows の内部*」 (Mark Russinovich と David ソロモン) を参照してください。

<a name="remarks"></a>コメント
-------

プロセッサ制御ブロック (PRCB) は、PCR の拡張機能です。 これは、 [ **! prcb**](-prcb.md)拡張機能と共に表示できます。

X86 ターゲットコンピューターの **! pcr**拡張機能の例を次に示します。

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

この表示のエントリの1つは、割り込み要求レベル (IRQL) を示しています。 **! Pcr**拡張機能には現在の irql が表示されますが、現在の irql は通常はあまり重要ではありません。 バグチェックまたはデバッガー接続の直前に存在していた IRQL は、さらに興味深いものになります。 これは[ **! irql**](-irql.md)によって表示されます。これは、windows Server 2003 以降のバージョンの windows を実行しているコンピューターでのみ使用できます。









