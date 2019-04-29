---
title: devnode
description: Devnode 拡張機能は、デバイス ツリー内のノードに関する情報を表示します。
ms.assetid: 0c8cb743-f756-461e-b92b-352b550706c1
keywords:
- デバイス ノード
- デバイスのツリー
- Windows デバッグ devnode
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devnode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d033ae27542c9a75445df6705f2a47fc99e06ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334586"
---
# <a name="devnode"></a>!devnode


**! Devnode**拡張機能は、デバイス ツリー内のノードに関する情報を表示します。

```dbgcmd
!devnode Address [Flags] [Service]  
!devnode 1 
!devnode 2
```

## <a name="span-idddkdevnodedbgspanspan-idddkdevnodedbgspanparameters"></a><span id="ddk__devnode_dbg"></span><span id="DDK__DEVNODE_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
あるノードが表示されるデバイスの拡張機能の 16 進数のアドレスを指定します。 0 の場合は、デバイスの主なツリーのルートが表示されます。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示される出力のレベルを指定します。 次のビットを組み合わせてこのことができます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
[デバイス] ノードのすべての子が表示をによりします。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
表示に使用されるリソースを含める (CM\_リソース\_リスト)。 IRP によって報告された boot 構成が含まれます\_MN\_クエリ\_でデバイスに割り当てられているリソースと同様に、リソース、 *AllocatedResources*の IRPパラメーター\_MN\_開始\_デバイス。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
表示するために必要なリソースが含まれます (IO\_リソース\_要件\_一覧) IRP によって報告された\_MN\_フィルター\_リソース\_要件。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
表示のデバイスに割り当て済みとして変換されたリソースの一覧を含める、 *AllocatedResourcesTranslated* IRP のパラメーター\_MN\_開始\_デバイス。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
開始されていないデバイス ノードのみを表示することを指定します。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>Bit 5 (0x20)  
問題のあるデバイス ノードのみを表示することを指定します。 (これらは DNF フラグのビットを含むノード\_HAS\_問題または DNF\_HAS\_プライベート\_問題です)。

<span id="_______Service______"></span><span id="_______service______"></span><span id="_______SERVICE______"></span> *サービス*   
サービスの名前を指定します。 これが含まれる場合は、このサービスによってデバイス ノードのみが表示されます。 (場合*フラグ*によってこのサービスとその子が表示されるすべてのデバイス ノードにはビット 0x1 が含まれています)。

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

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドのアプリケーション。 デバイス ツリーについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

**! Devnode 1**コマンドには、デバイス オブジェクトのすべて保留中の削除が一覧表示します。

**! Devnode 2**保留中のすべてのデバイス オブジェクトの排出コマンドの一覧。

使用することができます **! devnode 0 1**にデバイス全体のツリーを参照してください。

 

 





