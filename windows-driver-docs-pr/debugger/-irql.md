---
title: irql 拡張コマンド
description: Irql 拡張は、デバッガーが中断する前に、ターゲットコンピューター上のプロセッサの割り込み要求レベル (IRQL) を表示します。
ms.assetid: 52dd3b9f-c03c-4b90-a01b-25289de67f5a
keywords:
- IRQL
- 割り込み要求レベル
- irql Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- irql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e2db8736b25b6615c793625f5f2248e47ccb4629
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826688"
---
# <a name="irql"></a>!irql


**! Irql** extension は、デバッガーが中断する前に、ターゲットコンピューター上のプロセッサの割り込み要求レベル (irql) を表示します。

```dbgcmd
!irql [Processor] 
```

## <a name="span-idddk__irql_dbgspanspan-idddk__irql_dbgspanparameters"></a><span id="ddk__irql_dbg"></span><span id="DDK__IRQL_DBG"></span>パラメータ


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*プロセッサ*   
プロセッサを指定します。 プロセッサ番号を入力します。 このパラメーターを省略した場合、デバッガーは現在のプロセッサの IRQL を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

**! Irql**拡張機能は、windows Server 2003 以降のバージョンの windows でのみ使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Server 2003 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

IRQLs の詳細については、Windows Driver Kit (WDK) のドキュメントおよび*Microsoft windows の内部*(Mark Russinovich と David ソロモン) を参照してください。

<a name="remarks"></a>注釈
-------

対象のコンピューターがデバッガーに侵入すると、IRQL は変わりますが、デバッガーの中断直前に有効だった IRQL が保存されます。 **! Irql** extension には、保存された irql が表示されます。

同様に、バグチェックが発生し、クラッシュダンプファイルが作成された場合、クラッシュダンプファイルに保存されている IRQL は、 [**kebug Checkex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kebugcheckex)ルーチンが実行された irql ではなく、バグチェックの直前のものになります。

どちらの場合も、x86 アーキテクチャを除き、\_レベルをディスパッチするために現在の IRQL が発生します。 そのため、このようなイベントが複数発生した場合、表示される IRQL もディスパッチ\_レベルになるため、デバッグ目的では役に立ちません。

[ **! Pcr**](-pcr.md)拡張機能では、すべてのバージョンの Windows で現在の irql が表示されますが、現在の irql は通常は役に立ちません。 バグチェックまたはデバッガー接続の直前に存在していた IRQL はさらに興味深いものであり、 **! irql**を使用した場合にのみ表示されます。

無効なプロセッサ番号を指定した場合、またはカーネルが破損している場合は、"PRCB アドレスを取得できません" というメッセージが表示されます。

デュアルプロセッサ x86 コンピューターからのこの拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !irql 0
Debugger saved IRQL for processor 0x0 -- 28 (CLOCK2_LEVEL)

kd> !irql 1
Debugger saved IRQL for processor 0x1 -- 0 (LOW_LEVEL)
```

デバッガーが詳細モードの場合は、IRQL 自体の説明が含まれます。 Itanium プロセッサの例を次に示します。

```dbgcmd
kd> !irql
Debugger saved IRQL for processor 0x0 -- 12 (PC_LEVEL) [Performance counter level]
```

IRQL 番号の意味は、多くの場合、プロセッサに依存します。 X64 プロセッサの例を次に示します。 IRQL 番号は前の例と同じですが、IRQL の意味が異なることに注意してください。

```dbgcmd
kd> !irql
Debugger saved IRQL for processor 0x0 -- 12 (SYNCH_LEVEL) [Synchronization level]
```

 

 





