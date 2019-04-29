---
title: Tp
description: Tp の拡張機能には、スレッド プールの情報が表示されます。
ms.assetid: 33b22e04-b781-4890-8142-c2624fdc4055
keywords:
- スレッド プール
- Windows デバッグ tp
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a8a69493a7dc793784e5ac1cd56adb231258e46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334191"
---
# <a name="tp"></a>!tp


**! Tp**拡張機能には、スレッド プールの情報が表示されます。

```dbgcmd
!tp pool Address [Flags] 
!tp tqueue Address [Flags] 
!tp ItemType Address [Flags] 
!tp ThreadType [Address] 
!tp stats Address [Flags] 
!tp wfac Address 
!tp wqueue Address Priority Node 
!tp -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______pool_Address_____________"></span><span id="_______pool_address_____________"></span><span id="_______POOL_ADDRESS_____________"></span> **プール** **** *アドレス*   
全体のスレッド プールと、*アドレス*に表示されます。 場合*アドレス*0 の場合は、すべてのスレッド プールが表示されます。

<span id="_______tqueue_______Address______"></span><span id="_______tqueue_______address______"></span><span id="_______TQUEUE_______ADDRESS______"></span> **キュー** **** *アドレス*   
アクティブ タイマー キューが*アドレス*に表示されます。

<span id="_______ItemType_Address______"></span><span id="_______itemtype_address______"></span><span id="_______ITEMTYPE_ADDRESS______"></span> *ItemType のアドレス*   
により、指定したスレッド プール アイテムは表示します。 *アドレス*項目のアドレスを指定します。 *ItemType*項目の種類を指定しますこの可能性には次のいずれかを含めることができます。

<span id="obj"></span><span id="OBJ"></span>**obj**  
(IO の項目) などの汎用的なプールの項目が表示されます。

<span id="timer"></span><span id="TIMER"></span>**タイマー**  
タイマーの項目が表示されます。

<span id="wait"></span><span id="WAIT"></span>**待機**  
待機の項目が表示されます。

<span id="work"></span><span id="WORK"></span>**作業**  
作業項目が表示されます。

<span id="_______ThreadType__Address_"></span><span id="_______threadtype__address_"></span><span id="_______THREADTYPE__ADDRESS_"></span> *ThreadType* \[*アドレス*\]  
表示される指定した型のスレッドをによりします。 場合*アドレス*が含まれると、0 以外の場合、このアドレスにあるスレッドのみが表示されます。 場合*アドレス*0 の場合に一致するすべてのスレッドは、 *ThreadType*が表示されます。 場合*アドレス*を省略すると、一致するスレッドのみ*ThreadType*に現在関連付けられているスレッドが表示されます。 *ThreadType*表示するスレッドの種類を指定します。 この可能性には次のいずれかを含めることができます。

<span id="waiter"></span><span id="WAITER"></span>**待機**  
スレッド プールの待機スレッドが表示されます。

<span id="worker"></span><span id="WORKER"></span>**ワーカー**  
スレッド プールのワーカー スレッドが表示されます。

<span id="stats__Address_"></span><span id="stats__address_"></span><span id="STATS__ADDRESS_"></span>**stats** **\[**<em>アドレス</em>**\]**  
表示される現在のスレッドのデバッグの統計をによりします。 *アドレス*は省略できますが、-1 (負の値は 1 つ) を表す、現在のスレッドを等しく必要があります指定されている場合。

<span id="_______wfac_______Address______"></span><span id="_______wfac_______address______"></span><span id="_______WFAC_______ADDRESS______"></span> **wfac** **** *アドレス*   
(Windows 7 と以降のみ)ワーカーの工場出荷時に発生*アドレス*に表示されます。 指定した*アドレス*0 以外のアドレスを有効にする必要があります。

<span id="_______wqueue_______Address______"></span><span id="_______wqueue_______address______"></span><span id="_______WQUEUE_______ADDRESS______"></span> **wqueue** **** *アドレス*   
(Windows 7 と以降のみ)その matche、次の作業キューおよび NUMA ノードの表示を原因: 指定された優先度で指定した NUMA ノード、NUMA ノードが属している、指定したアドレスで、プール。 *アドレス*プールのアドレスを指定します。 ときに、 **wqueue**パラメーターを使用、によってその後にする必要があります*アドレス*、*優先度*、および*ノード*します。

<span id="_______Priority______"></span><span id="_______priority______"></span><span id="_______PRIORITY______"></span> *優先順位*   
(Windows 7 と以降のみ)表示する作業キューの優先度レベルを指定します。 *優先順位*値は次のいずれかを指定できます。

<span id="0"></span>**0**  
優先度の高い作業キューが表示されます。

<span id="1"></span>**1**  
通常の優先順位での作業キューが表示されます。

<span id="2"></span>**2**  
優先度の低い作業キューが表示されます。

<span id="-1"></span>**-1**  
すべての作業キューが表示されます。

<span id="_______Node______"></span><span id="_______node______"></span><span id="_______NODE______"></span> *ノード*   
(Windows 7 と以降のみ)指定されたプールに属する NUMA ノードを示す*アドレス*します。 場合*ノード*-1 (負の値は 1 つ) は、すべての NUMA ノードが表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示に含める必要がありますを指定します。 これは、次のビット値 (既定値は 0x0) のいずれかの合計になります。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
単一行の出力に表示をによりします。 このビット値が出力に影響を与えませんときに、 *ItemType*が表示されます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
メンバーの情報が追加ディスプレイをによりします。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
このフラグは、関連する場合にのみ、**プール**オプションを使用します。 Windows XP、Windows Server 2003、Windows Vista、および Windows Server 2008 では、このフラグによって、プールの作業キューが表示されます。 Windows 7 以降では、このフラグにより、通常の優先順位は、プール内のすべての作業キューおよびすべての NUMA ノードに表示にします。

<span id="_______-_______"></span> **-?**   
デバッガー コマンド ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スレッド プールについては、Microsoft Windows SDK のドキュメントを参照してください。

 

 





