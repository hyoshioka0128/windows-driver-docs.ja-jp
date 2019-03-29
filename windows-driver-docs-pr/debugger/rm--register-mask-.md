---
title: rm (レジスタ マスク)
description: Rm コマンドは、変更または登録の表示のマスクが表示されます。 このマスクは、r (レジスタ) コマンドでのレジスタの表示方法を制御します。
ms.assetid: b3203bf3-b614-490b-8cbd-6abb291a801a
keywords:
- rm (登録マスク) Windows のデバッグ
ms.date: 07/12/2018
topic_type:
- apiref
api_name:
- rm (Register Mask)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 76526208eb8ed0ccf8457bbd6f8768e708cbb6a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577736"
---
# <a name="rm-register-mask"></a>rm (レジスタ マスク)


**Rm**コマンドを変更するか、登録の表示のマスクが表示されます。 このマスクでのレジスタを表示する方法を制御、 [ **r (レジスタ)** ](r--registers-.md)コマンド。

```dbgcmd
rm 
rm ? 
rm Mask 
```

## <a name="span-idddkcmdregistermaskdbgspanspan-idddkcmdregistermaskdbgspanparameters"></a><span id="ddk_cmd_register_mask_dbg"></span><span id="DDK_CMD_REGISTER_MASK_DBG"></span>パラメーター


<span id="______________"></span> **?**   
候補の一覧を表示します*マスク*ビット。

<span id="_______Mask______"></span><span id="_______mask______"></span><span id="_______MASK______"></span> *マスク*   
デバッガー、レジスタを表示するときに使用するマスクを指定します。 *マスク*はレジスタの表示について何かを示すビットの合計です。 ビットの意味は、プロセッサと、モードによって異なります。 詳細については次の「解説」表を参照してください。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>



<a name="remarks"></a>コメント
-------

コマンド名の"m"は、小文字である必要があります。

使用する場合**rm**パラメーターなしで、現在の値が表示され、そのビットについて説明します。

基本の整数を表示するには、登録、ビット 0 (0x1) を設定するか、ビット 1 (0x2) 必要があります。 既定では、32 ビット ターゲット 0x1 に設定されてし、0x2 は 64 ビット ターゲットの設定。 これら 2 つのビットを設定することはできません - 同時に両方のビットを設定しようとする場合 0x2 オーバーライド 0x1 です。

既定のマスクを使用してオーバーライドすることができます、 [ **r (レジスタ)** ](r--registers-.md)コマンドと共に、 **M**オプション。

次*マスク*x86 ベースのプロセッサまたは x64 ベースのプロセッサのビットがサポートされています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット</th>
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
0 1</td>
<td align="left"><p></p>
0x1 0x2</td>
<td align="left"><p>基本整数レジスタを表示します。 (これらのビットの一方または両方を設定するのと同じ効果です。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x4</p></td>
<td align="left"><p>浮動小数点レジスタが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0x8</p></td>
<td align="left"><p>セグメントのレジスタが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0x10</p></td>
<td align="left"><p>MMX レジスタが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>デバッグのレジスタが表示されます。 カーネル モードでこのビットを設定も表示されます、CR4 レジスタ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>0x40</p></td>
<td align="left"><p>SSE の XMM レジスタを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>0x80</p></td>
<td align="left"><p>(カーネル モードのみ)CR0、CR2、CR3 および CR8 などの制御レジスタが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>0x100</p></td>
<td align="left"><p>(カーネル モードのみ)記述子およびタスクの状態のレジスタが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>0x200</p></td>
<td align="left"><p>AVX YMM を浮動小数点の登録を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>0x400</p></td>
<td align="left"><p>AVX YMM を 10 進整数で登録を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>11</p></td>
<td align="left"><p>0x800</p></td>
<td align="left"><p>10 進整数での AVX XMM レジスタを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>12</td>
<td align="left"><p></p>0x1000</td>
<td align="left"><p>浮動小数点形式で表示 avx-512 の zmm0 zmm31 を登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>13</p></td>
<td align="left"><p>0x2000</p></td>
<td align="left"><p>整数形式で表示 avx-512 の zm00 zmm31 を登録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>14</p></td>
<td align="left"><p>0x4000</p></td>
<td align="left"><p>Avx-512 k0 k7 レジスタが表示されます。</p></td>
</tr>
</tbody>
</table>


## <a name="examples"></a>使用例

整数の状態を有効にし、セグメントを登録します。

```dbgcmd
0: kd> rm 0x00a
0: kd> rm
Register output mask is a:
       2 - Integer state (64-bit)
       8 - Segment registers
```


0x1000 (avx-512 zmm0 zmm31 レジスタは、浮動小数点形式で表示されます) を有効にします。

```dbgcmd
0: kd> rm 0x100a
0: kd> rm
Register output mask is 100a:
       2 - Integer state (64-bit)
       8 - Segment registers
    1000 - AVX-512 ZMM registers
```


マスク 0x2000 (avx-512 の zmm00 zmm31 を整数形式で登録が表示される) を有効にします。

```dbgcmd
0: kd> rm 0x200a
0: kd> rm
Register output mask is 200a:
       2 - Integer state (64-bit)
       8 - Segment registers
    2000 - AVX-512 ZMM Integer registers
```


すべてのマスクを avx-512 登録を有効にします。

```dbgcmd
0: kd> rm 0x700a
0: kd> rm
Register output mask is 700a:
       2 - Integer state (64-bit)
       8 - Segment registers
    1000 - AVX-512 ZMM registers
    2000 - AVX-512 ZMM Integer registers
    4000 - AVX-512 Opmask registers
```

しようとするがサポートしていないハードウェア レジスタ マスクを設定すると、登録マスクの無効なビットは無視されます。

```dbgcmd
kd> rm 0x100a
Ignored invalid bits 1000
kd> rm
Register output mask is a:
      2 - Integer state (64-bit)
       8 - Segment registers
```





