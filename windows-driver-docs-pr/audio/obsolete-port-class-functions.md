---
title: 廃止されたポート クラス関数
description: 廃止されたポート クラス関数
ms.assetid: 6fcb5ae6-81bc-423e-9757-34955a2de522
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e9ad4ea37508455ad714b870d286886a973b52c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830315"
---
# <a name="obsolete-port-class-functions"></a>廃止されたポート クラス関数


## <span id="ddk_obsolete_port_class_functions_ks"></span><span id="DDK_OBSOLETE_PORT_CLASS_FUNCTIONS_KS"></span>


ヘッダーファイル portcls は、新しい PortCls 関数に置き換えられた古い PortCls 関数の名前を含むマクロを定義します。 これらのマクロを使用すると、古い PortCls 関数名への参照を含む古いソースコードを再コンパイルして、ソースファイルを編集しなくても新しい PortCls 関数を使用できます。

互換性のために残されている名前を使用するソースコードをコンパイルするときに、パラメーター名として古い\_名\_定義します。 このパラメーターは、コンパイラのコマンドライン引数 "-DPC\_OLD\_NAMES" によって定義できます。これは、ステートメント `#define PC_OLD_NAMES` をソースファイル自体に導入するよりも便利です。

次の表に、左側の列に残されている PortCls 関数の名前を示します。 互換性のために残されている各名前について、中央の列には、それを置き換える新しい PortCls 関数の名前が含まれています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">廃止された関数名</th>
<th align="left">新しい関数名</th>
<th align="left">引数は変更しましたか?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AddAdapterDevice</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice" data-raw-source="[&lt;strong&gt;PcAddAdapterDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice)"><strong>PcAddAdapterDevice</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>CompletePendingPropertyRequest</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest" data-raw-source="[&lt;strong&gt;PcCompletePendingPropertyRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest)"><strong>PcCompletePendingPropertyRequest</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GetTimeInterval</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgettimeinterval" data-raw-source="[&lt;strong&gt;PcGetTimeInterval&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgettimeinterval)"><strong>PcGetTimeInterval</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="even">
<td align="left"><p>InitializeAdapterDriver</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver" data-raw-source="[&lt;strong&gt;PcInitializeAdapterDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcinitializeadapterdriver)"><strong>PcInitializeAdapterDriver</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NewDmaChannel</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel" data-raw-source="[&lt;strong&gt;PcNewDmaChannel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel)"><strong>PcNewDmaChannel</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewMiniport ポート</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport" data-raw-source="[&lt;strong&gt;PcNewMiniport&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)"><strong>PcNewMiniport ポート</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ニューポート</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport" data-raw-source="[&lt;strong&gt;PcNewPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)"><strong>PcNewPort</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewResourceList</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist" data-raw-source="[&lt;strong&gt;PcNewResourceList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcelist)"><strong>PcNewResourceList</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NewResourceSublist</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist" data-raw-source="[&lt;strong&gt;PcNewResourceSublist&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewresourcesublist)"><strong>PcNewResourceSublist</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="even">
<td align="left"><p>NewServiceGroup</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewservicegroup" data-raw-source="[&lt;strong&gt;PcNewServiceGroup&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewservicegroup)"><strong>PcNewServiceGroup</strong></a></p></td>
<td align="left"><p>no</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RegisterPhysicalConnection</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)"><strong>Pcregiphysicalconnection</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>RegisterPhysicalConnectionFromExternal</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnectionFromExternal&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal)"><strong>外部への物理接続</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RegisterPhysicalConnectionToExternal</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal" data-raw-source="[&lt;strong&gt;PcRegisterPhysicalConnectionToExternal&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal)"><strong>外部の物理 Connectiontoexternal</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>RegisterSubdevice</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice" data-raw-source="[&lt;strong&gt;PcRegisterSubdevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)"><strong>Pcregisubdevice</strong></a></p></td>
<td align="left"><p>使用可能</p></td>
</tr>
</tbody>
</table>

 

場合によっては、単純な名前の変更ではなく、PortCls に関数が実装されていることを示す修飾子 `Pc` が名前の先頭に挿入されます。 ただし、その他のケースでは、関数の名前に加えて引数リストも変更されています。 前の表の右側の列は、引数が変更されたかどうかを示しています。

引数が変更された場合、portcls のマクロは、古い PortCls 関数の引数リストを新しい PortCls 関数の同等の引数に変換します。 次のマクロには引数の変換が含まれています。

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

 

 





