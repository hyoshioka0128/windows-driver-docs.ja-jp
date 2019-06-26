---
title: リムーバブル デバイスの機能から生成されたコンテナー Id をオーバーライドします。
description: リムーバブル デバイス機能のオーバーライドで生成されるコンテナー ID
ms.assetid: 8b1bf9d4-1aea-4d82-b783-f6dc62b9f8f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4edd1e96631a8a57b2972dc8351c74e686141009
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378857"
---
# <a name="container-ids-generated-from-a-removable-device-capability-override"></a>リムーバブル デバイス機能のオーバーライドで生成されるコンテナー ID


Windows 7 以降、新しいデバイスはバスに固有の一意の ID を提供する必要があります (」の説明に従って[コンテナー Id は、バスに固有の一意の ID から生成された](container-ids-generated-from-a-bus-specific-unique-id.md))。

または、デバイスとバス ドライバーする必要がありますリムーバブル デバイスの機能が正しく設定 (」の説明に従って[コンテナー Id は、リムーバブル デバイスの機能から生成された](container-ids-generated-from-the-removable-device-capability.md))。 リムーバブル デバイスの機能の詳細については、次を参照してください。[リムーバブル デバイスの機能の概要](overview-of-the-removable-device-capability.md)します。

Windows 7 および Windows の以降のバージョンは、報告されたリムーバブル デバイスの機能をオーバーライドするためのメカニズムもサポートします。 このメカニズムは、リムーバブル デバイスの機能の報告する従来のデバイスに適しています。

優先機構はリムーバブル デバイスの機能の値を変更していない、デバイス用のコンテナーの Id を生成するときに、上書きの設定とリムーバブル デバイスの機能の値ではなくを使用する PnP マネージャーを強制します。

このオーバーライド メカニズムでは、レジストリ ベースの方法でコンテナー ID を生成できます。 [デバイス] ノード (親) の最上位のコンテナー ID が生成されるとすぐに (*devnode*) で説明するヒューリスティックを使用して、デバイスの場合は、各子 devnode によって継承が同じコンテナー ID、デバイスの[コンテナー Idリムーバブル デバイスの機能から生成された](container-ids-generated-from-the-removable-device-capability.md)します。

上書きのメカニズムは、特定のデバイスにマップするレジストリ キーで構成されるレジストリ ベースの参照テーブルです。 このオーバーライド テーブルは、管理は、、 [DeviceOverrides レジストリ キー](deviceoverrides-registry-key.md)、次のレジストリ キーとサブキーで構成されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">テーブル レベル</th>
<th align="left">レジストリ キーとサブキーの名前</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p><a href="deviceoverrides-registry-key.md" data-raw-source="[DeviceOverrides](deviceoverrides-registry-key.md)">DeviceOverrides</a></p></td>
<td align="left"><p>すべてのリムーバブル デバイスの機能の親キーをオーバーライドします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><a href="hardwareid-registry-subkey.md" data-raw-source="[HardwareID](hardwareid-registry-subkey.md)">HardwareID</a></p></td>
<td align="left"><p>指定します、<a href="hardware-ids.md" data-raw-source="[hardware ID](hardware-ids.md)">ハードウェア ID</a>リムーバブル デバイスの機能をオーバーライドするデバイスが適用されます。</p>
<p>このサブキーの名前は実際のハードウェア ID で、すべての円記号 (") 文字に置き換えられます ('#') の数文字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p><a href="compatibleid-registry-subkey.md" data-raw-source="[CompatibleID](compatibleid-registry-subkey.md)">CompatibleID</a></p></td>
<td align="left"><p>指定します、<a href="compatible-ids.md" data-raw-source="[compatible ID](compatible-ids.md)">互換性 ID</a>リムーバブル デバイスの機能をオーバーライドするデバイスが適用されます。</p>
<p>このサブキーの名前は実際のハードウェア ID で、すべての円記号 (") 文字に置き換えられます ('#') の数文字。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p><a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a></p></td>
<td align="left"><p>デバイスの親デバイス ノードの場所のパスのみを指定します (<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-devnode" data-raw-source="&lt;em&gt;devnode&lt;/em&gt;"><em>devnode</em></a>)、リムーバブル デバイスの機能上書きを適用する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><a href="childlocationpaths-registry-subkey.md" data-raw-source="[ChildLocationPaths](childlocationpaths-registry-subkey.md)">ChildLocationPaths</a></p></td>
<td align="left"><p>デバイスの子 devnode の場所のパスが、リムーバブル デバイス機能上書きの適用を持つことを指定します。</p>
<div class="alert">
<strong>注</strong>、指定されたデバイスの親 devnode の影響を受けない、リムーバブル デバイス機能上書きしない限り、 <a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a>レジストリ サブキーが指定されても、または<strong>ChildLocationPaths</strong>親 devnode のレジストリ サブキーが指定されています。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p><a href="locationpath-registry-subkey.md" data-raw-source="[LocationPath](locationpath-registry-subkey.md)">LocationPath</a></p></td>
<td align="left"><p>リムーバブル デバイスの機能をオーバーライドする devnode の不連続のロケーション パスの適用を指定します。</p>
<p>このサブキーの名前は、コンピューターにインストールされているデバイスの 1 つ devnode インスタンスの実際の場所のパスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p><a href="--registry-subkey.md" data-raw-source="[*](--registry-subkey.md)">*</a></p></td>
<td align="left"><p>リムーバブル デバイスの機能の上書きがすべて devnode、指定されたデバイスに適用されることを指定します。</p></td>
</tr>
</tbody>
</table>

 

内で、 [LocationPath](locationpath-registry-subkey.md)と[ \* ](--registry-subkey.md)レジストリ サブキー、DWORD 値 (**リムーバブル**) 該当する devnode はリムーバブルと見なさいるかどうかを指定します。(1) または削除不可 (0)。

### <a href="" id="example-1"></a> 例 1

一致する devnode のデバイスのオーバーライドを次に示します、 [HardwareID](hardwareid-registry-subkey.md)で指定された場所のパスだけでなくレジストリ サブキー、 [LocationPaths](locationpaths-registry-subkey.md)レジストリ サブキー。

この例で、上書き、リムーバブル デバイスの機能を無効になります、持つすべての devnode に適用される、[ハードウェア ID](hardware-ids.md) USB の\\VID_1234 & PCIROOT(0) ロケーション パスで PID_5678\#PCI (102)\#USBROOT(0)\#USB(1) します。

次は、この上書きのレジストリの表形式の例です。

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceOverrides
    USB#VID_1234&PID_5678
        LocationPaths
            PCIROOT(0)#PCI(102)#USBROOT(0)#USB(1)
                Removable=0
```

この例で`USB#VID_1234&PID_5678 `の名前を指定します、 [HardwareID](hardwareid-registry-subkey.md)のレジストリ サブキーと`PCIROOT(0)#PCI(102)#USBROOT(0)#USB(1)`の名前を指定します、 [LocationPath](locationpath-registry-subkey.md)レジストリ サブキー。

この上書きは、デバイスのトポロジのプラグ アンド プレイ (PnP) マネージャーの解釈を変更します。 いることを確認で devnode、[ハードウェア ID](hardware-ids.md) USB の値\\VID_1234 & PID_5678 としてマークされていないリムーバブル レジストリにします。 PnP マネージャーがその親から削除されていないとして devnode を解釈するため、この devnode の新しいコンテナー ID は生成されません。 代わりに、USB\\VID_1234 & PID_5678 (およびそのすべての子) は、その親のコンテナー ID (ContainerID {A}) を継承します。

このオーバーライドの結果は、ツリー内のすべての devnode 同じコンテナー ID があるために、1 つのデバイスのグループです。 USB デバイス\\VID_1234 & PID_5678 がコンピューターに統合されていると解釈されます。

次の図は、結果として得られるデバイス トポロジを示しています、コンテナー ID の割り当てに関連付けられています。

![リムーバブル デバイスの機能を示すダイアグラムを上書き devnode 削除不可としてマークします。](images/containerid-4.png)

前の例では、頻繁に発生 devnode トポロジを示しています。 デバイスが誤って報告自体リムーバブルとして特定のバスの場所に配線で接続されたポータブル コンピューター。 Web カメラまたは生体認証 (指紋) のセンサーなど、コンピューターに物理的に統合されているデバイスは必要がありますユーザーできません物理的に分離するので、それらのコンピューターからリムーバブルと報告されません。 リムーバブルのオーバーライドにより、独立系ハードウェア ベンダー (IHV) または供給 (OEM) の変更方法 PnP マネージャーは、リムーバブル デバイスの機能を解釈し、それによって、デバイスのコンテナーの ID の割り当てに影響します。

### <a name="example-2"></a>例 2

特定の一致する、すべて devnode のリムーバブル デバイス機能オーバーライドを次に示します[ハードウェア ID](hardware-ids.md)値。

オーバーライドは、この例で、リムーバブル デバイスの機能が有効になり、USB のハードウェア ID の値を持つ devnode に、上書きが適用される\\VID_062A & PID_0000 します。

このオーバーライドのレジストリ テーブル形式の概要を説明を次に示します。

```cpp
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceOverrides
    USB#VID_062A&PID_00001
        LocationPaths
            *
                Removable=1
```

1 の名前、 [HardwareID](hardwareid-registry-subkey.md)レジストリ サブキー。

Devnode で、この例では、[ハードウェア ID](hardware-ids.md) USB の\\VID_1234 & PID_5678 リムーバブル デバイスの機能を正しく報告します。 PnP マネージャーでは、し、そのすべての子 devnode コンテナー ID (ContainerID {B}) が生成されます。

ただしで子 devnode、[ハードウェア ID](hardware-ids.md) USB の\\VID_062A & PID_0000 オーバーライドに一致します。 その結果、PnP マネージャーでは、この devnode とそのすべての子 devnode、含まれている別の ID (ContainerID {c}) が生成されます。

前に、として、この上書きは変更デバイス トポロジの PnP マネージャーの解釈します。 物理デバイスでは、2 つのコンテナー Id が割り当てられているし、Windows によって 2 つのデバイスと見なされます。 注意を devnode、[ハードウェア ID](hardware-ids.md) USB の\\VID_062A & PID_0000 がデバイスに、devnode をグループ化にはリムーバブルと解釈されます。 リムーバブル デバイスの機能の devnode によって報告された値は変わりません。

さらに、\*がコンピューター上のすべての devnode にこの上書きが適用されることを示すレジストリ サブキーが指定されて、[ハードウェア ID](hardware-ids.md) USB の\\VID_062A & PID_0000 します。

次の図は、結果として得られるデバイス トポロジを示しています、コンテナー ID の割り当てに関連付けられています。

![リムーバブル デバイスの機能を示すダイアグラムを上書きとしてリムーバブル devnode をマークします。](images/containerid-5.png)

 

 





