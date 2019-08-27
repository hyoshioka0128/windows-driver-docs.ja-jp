---
title: devnode
description: Devnode 拡張機能は、デバイスツリー内のノードに関する情報を表示します。
ms.assetid: 0c8cb743-f756-461e-b92b-352b550706c1
keywords:
- デバイス ノード
- デバイスツリー
- devnode Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devnode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f912b91657f078310d6635196fb0685b7fd5d2c4
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025270"
---
# <a name="devnode"></a>!devnode


**! Devnode**拡張機能は、デバイスツリー内のノードに関する情報を表示します。

```dbgcmd
!devnode Address [Flags] [Service]  
!devnode 1 
!devnode 2
```

## <a name="span-idddk__devnode_dbgspanspan-idddk__devnode_dbgspanparameters"></a><span id="ddk__devnode_dbg"></span><span id="DDK__DEVNODE_DBG"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
ノードが表示されるデバイス拡張機能の16進数のアドレスを指定します。 この値が0の場合は、メインデバイスツリーのルートが表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*フラグ*   
表示する出力のレベルを指定します。 これは、次のビットの任意の組み合わせにすることができます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
表示に、デバイスノードのすべての子が含まれるようにします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
表示に、使用されたリソース (\_CM\_リソースリスト) が含まれるようにします。 これには\_、irp\_の全クエリ\_リソースによって報告されるブート構成と、irp\_\_の*AllocatedResources*パラメーターにデバイスに割り当てられたリソースが含まれます。デバイス\_を起動します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
IRP\_\_のフィルター\_の\_リソース\_要件によって報告されたリソース (IO リソース要件の一覧) が表示されます。\_\_

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
IRP \_AllocatedResourcesTranslatedSTART\_デバイスのパラメーターに、デバイスに割り当てられている翻訳済みリソースの一覧が表示されます。\_

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
開始されていないデバイスノードのみを表示するように指定します。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>ビット 5 (0x20)  
問題のあるデバイスノードだけを表示するように指定します。 (これらは、ビット\_dnf に問題が\_あるか、dnf\_に\_プライベート\_な問題があることを示すフラグを含むノードです)。

<span id="_______Service______"></span><span id="_______service______"></span><span id="_______SERVICE______"></span>*サービス*   
サービスの名前を指定します。 これが含まれている場合は、このサービスによって駆動されているデバイスノードだけが表示されます。 (*フラグ*にビット0x1 が含まれている場合、このサービスによって駆動されるデバイスノードとそのすべての子が表示されます)。

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

この拡張機能コマンドのアプリケーションについては、「[プラグアンドプレイデバッグ](plug-and-play-debugging.md)」を参照してください。 デバイスツリーの詳細については、Windows Driver Kit (WDK) のドキュメントと、Mark Russinovich と David ソロモンによる*Microsoft windows の内部構造*に関するドキュメントを参照してください。

<a name="remarks"></a>コメント
-------

**! Devnode 1**コマンドを実行すると、デバイスオブジェクトの保留中のすべての削除が一覧表示されます。

**! Devnode 2**コマンドは、デバイスオブジェクトのすべての保留中の取り出しを一覧表示します。

**! Devnode 0 1**を使用して、デバイスツリー全体を表示することができます。

 

 





