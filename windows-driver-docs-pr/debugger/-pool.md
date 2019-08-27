---
title: プール拡張コマンド
description: プールの拡張機能には、特定のプール割り当てに関する情報、またはシステム全体のプール全体に関する情報が表示されます。
ms.assetid: 1c224e0c-d50c-487e-8238-9be054368ac2
keywords:
- 管理
- pooltag .txt ファイル
- プールタグ
- メモリ、プールタグ
- プール Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2fff8b18eb0c0f6a2706471eedcd3bc422d36bab
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025195"
---
# <a name="pool"></a>!pool


**! Pool** extension には、特定のプール割り当てに関する情報、またはシステム全体のプールに関する情報が表示されます。

```dbgcmd
!pool [Address [Flags]]
```

## <a name="span-idddk__pool_dbgspanspan-idddk__pool_dbgspanparameters"></a><span id="ddk__pool_dbg"></span><span id="DDK__POOL_DBG"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
表示するプールエントリを指定します。 *アドレス*が-1 の場合、このコマンドはプロセス内のすべてのヒープに関する情報を表示します。

*Address*が0または省略された場合、このコマンドはプロセスヒープに関する情報を表示します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*フラグ*   
使用する詳細レベルを指定します。 これは、次のビット値の任意の組み合わせにすることができます。既定値は0です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
プールのヘッダーだけでなく、プールの内容を表示するようにします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
指定された*アドレス*を実際に含むプールを除き、すべてのプールのプールヘッダー情報を表示しないようにします。

<span id="Bit_31__0x80000000_"></span><span id="bit_31__0x80000000_"></span><span id="BIT_31__0X80000000_"></span>ビット 31 (0x80000000)  
プールの種類とプールタグの説明が表示されないようにします。

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

メモリプールの詳細については、「Windows Driver Kit (WDK)」のドキュメントと*Microsoft windows の内部構造*を参照してください。これには、Mark Russinovich と David ソロモンが使用されます。

<a name="remarks"></a>コメント
-------

Windows XP 以降のバージョンの Windows では、 **! pool** extension によって、各割り当てに関連付けられたプールタグが表示されます。 そのプールタグの所有者も表示されます。 この表示は、pooltag .txt ファイルの内容に基づいています。 このファイルは、デバッグツールの Windows インストール用のトリアージサブディレクトリにあります。 必要に応じて、このファイルを編集して、プロジェクトに関連するプールタグを追加できます。

**警告更新バージョン**の Windows 用デバッグツールを現在のバージョンと同じディレクトリにインストールすると、そのディレクトリ内のすべてのファイル (pooltag .txt など) が上書きされます。   サンプルの pooltag .txt ファイルを変更または置き換える場合は、そのコピーを別のディレクトリに保存してください。 デバッガーを再インストールした後、保存された pooltag を既定のバージョンにコピーできます。

 

**! Pool** extension がプールの破損を報告する場合は、 [ **! poolval**](-poolval.md)を使用して調査する必要があります。

次に例を示します。 *Address*が0xE1001050 を指定した場合、このブロック内のすべてのプールのヘッダーが表示され、0xe1001050 自体\*はアスタリスク () でマークされます。

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

この例では、右端の列はプールタグを示しています。 左側の列には、プールが空いているか、割り当てられているかが表示されます。

次のコマンドは、プールのヘッダーとプールの内容を表示します。

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

 

 





