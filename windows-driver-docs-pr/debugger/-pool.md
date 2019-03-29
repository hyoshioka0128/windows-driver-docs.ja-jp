---
title: プールの拡張機能コマンド
description: プールの拡張機能では、システム全体のプールを全体または特定のプール割り当てに関する情報が表示されます。
ms.assetid: 1c224e0c-d50c-487e-8238-9be054368ac2
keywords:
- プール
- pooltag.txt ファイル
- プール タグ
- メモリ プール タグ
- プールの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3cf251bdbfcc78380be579d49c36c0732164db8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573987"
---
# <a name="pool"></a>!pool


**! プール**拡張機能には、システム全体のプールを全体または特定のプール割り当てに関する情報が表示されます。

```dbgcmd
!pool [Address [Flags]]
```

## <a name="span-idddkpooldbgspanspan-idddkpooldbgspanparameters"></a><span id="ddk__pool_dbg"></span><span id="DDK__POOL_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示するプールのエントリを指定します。 場合*アドレス*は-1 です。 このコマンドは、プロセス内のすべてのヒープに関する情報を表示します。

場合*アドレス*が 0 または省略すると、このコマンドは、プロセス ヒープに関する情報が表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
使用する詳細レベルを指定します。 次のビット値の任意の組み合わせを指定できます。既定値は、0 です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
プールのヘッダーだけでなく、プールのコンテンツを追加するためにディスプレイをによりします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
実際には、指定されたを含む 1 つを除く、すべてのプールのプールのヘッダー情報を抑制する表示*アドレス*します。

<span id="Bit_31__0x80000000_"></span><span id="bit_31__0x80000000_"></span><span id="BIT_31__0X80000000_"></span>ビット (0x80000000) 31  
プールの種類と、表示内のプール タグの説明を抑制します。

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

メモリ プールの詳細については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>コメント
-------

Windows XP および Windows での以降のバージョンで、 **! プール**拡張機能には、各割り当てに関連付けられているプール タグが表示されます。 プール タグの所有者も表示されます。 この表示は、pooltag.txt ファイルの内容に基づきます。 このファイルは、Windows のツールをデバッグ インストールのトリアージ サブディレクトリにあります。 する場合は、プロジェクトに関連するその他のプール タグを追加するには、このファイルを編集できます。

**警告**   pooltag.txt を含めて、そのディレクトリ内のファイルのすべてが上書きされますが、現在のバージョンと同じディレクトリ内の Windows 内のデバッグ ツールの更新バージョンをインストールする場合。 変更するか、またはサンプル pooltag.txt ファイルを置き換える場合は、別のディレクトリに、そのコピーを保存することを確認します。 デバッガーを再インストール後には、既定のバージョンを保存した pooltag.txt をコピーできます。

 

場合、 **! プール**プールの破損をレポートする拡張機能は、使用する必要があります[ **! poolval** ](-poolval.md)を調査します。

次に例を示します。 場合*アドレス*0xE1001050 を指定します。 このブロック内のすべてのプールのヘッダーを表示および 0xE1001050 自体はアスタリスクでマークされている (\*)。

```dbgcmd
kd> !pool e1001050 
 e1001000 size:   40 previous size:    0  (Allocated)  MmDT
 e1001040 size:   10 previous size:   40  (Free)       Mm  
*e1001050 size:   10 previous size:   10  (Allocated) *ObDi
 e1001060 size:   10 previous size:   10  (Allocated)  ObDi
 e1001070 size:   10 previous size:   10  (Allocated)  Symt
 e1001080 size:   40 previous size:   10  (Allocated)  ObDm
 e10010c0 size:   10 previous size:   40  (Allocated)  ObDi
.....
```

この例では、右端の列には、プール タグが表示されます。 これの左側の列は、プールが無料または割り当てられているかどうかを示します。

次のコマンドは、プールのヘッダーとプールの内容を示しています。

```dbgcmd
kd> !pool e1001050 1
 e1001000 size:   40 previous size:    0  (Allocated)  MmDT
 e1001008  ffffffff 0057005c 004e0049 004f0044
    e1001018  ffffffff 0053005c 00730079 00650074

 e1001040 size:   10 previous size:   40  (Free)       Mm  
 e1001048  ffffffff e1007ba8 e1501a58 01028101
    e1001058  ffffffff 00000000 e1000240 01028101

*e1001050 size:   10 previous size:   10  (Allocated) *ObDi
 e1001058  ffffffff 00000000 e1000240 01028101
    e1001068  ffffffff 00000000 e10009c0 01028101

 e1001060 size:   10 previous size:   10  (Allocated)  ObDi
 e1001068  ffffffff 00000000 e10009c0 01028101
    e1001078  ffffffff 00000000 00000000 04028101

......
```

 

 





