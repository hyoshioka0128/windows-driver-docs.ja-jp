---
title: 廃止されたポート クラス関数
description: 廃止されたポート クラス関数
ms.assetid: 6fcb5ae6-81bc-423e-9757-34955a2de522
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3514d6e452cb9c5dd5da26e928331510acd9f204
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549851"
---
# <a name="obsolete-port-class-functions"></a>廃止されたポート クラス関数


## <span id="ddk_obsolete_port_class_functions_ks"></span><span id="DDK_OBSOLETE_PORT_CLASS_FUNCTIONS_KS"></span>


新しい PortCls 関数で置き換えられた古い PortCls 関数の名前を含むヘッダー ファイル portcls.hdefines マクロ。 これらのマクロは、新しい PortCls 関数を使用して、ソース ファイルへの編集を必要とせずに再コンパイルする PortCls 関数名を廃止されたへの参照を含む古いソース コードを許可します。

古い形式の名前を使用するソース コードをコンパイルするときに定義のパラメーター名 PC\_古い\_名。 このパラメーターは、コンパイラのコマンドライン引数を定義できます"-DPC\_古い\_名"ステートメントを導入するよりも便利なかどうかは、`#define PC_OLD_NAMES`ソースにファイル自体。

次の表には、左側にある古い PortCls 関数名が一覧表示します。 古い名ごとに、中央の列には、これを置き換える新しい PortCls 関数の名前が含まれています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">古い関数名</th>
<th align="left">新しい関数の名前</th>
<th align="left">引数は変化しましたか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AddAdapterDevice</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537683" data-raw-source="[&lt;strong&gt;PcAddAdapterDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537683)"><strong>PcAddAdapterDevice</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>CompletePendingPropertyRequest</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537687" data-raw-source="[&lt;strong&gt;PcCompletePendingPropertyRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537687)"><strong>PcCompletePendingPropertyRequest</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GetTimeInterval</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537702" data-raw-source="[&lt;strong&gt;PcGetTimeInterval&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537702)"><strong>PcGetTimeInterval</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="even">
<td align="left"><p>InitializeAdapterDriver</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537703" data-raw-source="[&lt;strong&gt;PcInitializeAdapterDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537703)"><strong>PcInitializeAdapterDriver</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NewDmaChannel</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537712" data-raw-source="[&lt;strong&gt;PcNewDmaChannel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537712)"><strong>PcNewDmaChannel</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewMiniport</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537714" data-raw-source="[&lt;strong&gt;PcNewMiniport&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537714)"><strong>PcNewMiniport</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NewPort</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537715" data-raw-source="[&lt;strong&gt;PcNewPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537715)"><strong>PcNewPort</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewResourceList</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537717" data-raw-source="[&lt;strong&gt;PcNewResourceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537717)"><strong>PcNewResourceList</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NewResourceSublist</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537718" data-raw-source="[&lt;strong&gt;PcNewResourceSublist&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537718)"><strong>PcNewResourceSublist</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewServiceGroup</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537719" data-raw-source="[&lt;strong&gt;PcNewServiceGroup&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537719)"><strong>PcNewServiceGroup</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RegisterPhysicalConnection</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537726" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537726)"><strong>PcRegisterPhysicalConnection</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>RegisterPhysicalConnectionFromExternal</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537728" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnectionFromExternal&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537728)"><strong>PcRegisterPhysicalConnectionFromExternal</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RegisterPhysicalConnectionToExternal</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537729" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnectionToExternal&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537729)"><strong>PcRegisterPhysicalConnectionToExternal</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>RegisterSubdevice</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537731" data-raw-source="[&lt;strong&gt;PcRegisterSubdevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537731)"><strong>PcRegisterSubdevice</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
</tbody>
</table>

 

場合によっては、変更は、以下の単純な名前の変更に数します。修飾子`Pc`PortCls で関数が実装されることを示す名前の先頭に挿入されます。 それ以外の場合、引数リストが変更されただけでなく、関数の名前。 上記の表に、右側の列は、引数が変更されたかどうかを示します。

引数が変更された場合、portcls.hconvert のマクロ、引数の一覧、同等の新しい PortCls 関数の引数を廃止 PortCls 関数です。 次のマクロには、引数の変換が含まれています。

```cpp
#define InitializeAdapterDriver(c1,c2,a) \
    PcInitializeAdapterDriver(PDRIVER_OBJECT(c1),PUNICODE_STRING(c2),PDRIVER_ADD_DEVICE(a))
#define AddAdapterDevice(c1,c2,s,m) \
    PcAddAdapterDevice(PDRIVER_OBJECT(c1),PDEVICE_OBJECT(c2),s,m,0)
#define RegisterSubdevice(c1,c2,n,u) \
    PcRegisterSubdevice(PDEVICE_OBJECT(c1),n,u)
#define RegisterPhysicalConnection(c1,c2,fs,fp,ts,tp) \
    PcRegisterPhysicalConnection(PDEVICE_OBJECT(c1),fs,fp,ts,tp)
#define RegisterPhysicalConnectionToExternal(c1,c2,fs,fp,ts,tp) \
    PcRegisterPhysicalConnectionToExternal(PDEVICE_OBJECT(c1),fs,fp,ts,tp)
#define RegisterPhysicalConnectionFromExternal(c1,c2,fs,fp,ts,tp) \
    PcRegisterPhysicalConnectionFromExternal(PDEVICE_OBJECT(c1),fs,fp,ts,tp)
```

 

 





