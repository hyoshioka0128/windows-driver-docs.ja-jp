---
title: LocationPath レジストリのサブキー
description: LocationPath レジストリのサブキー
ms.assetid: 3b6f3501-5969-453c-a04b-5559761c3222
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeb81115900f3f99571552a9c7b9fa57e4aad86f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559387"
---
# <a name="locationpath-registry-subkey"></a>LocationPath レジストリのサブキー


Windows 7 以降、 **LocationPath**レジストリ サブキーをいずれかで識別される 1 つのデバイスのリムーバブル デバイス機能の上書きの場所のパスを指定します、 [HardwareID](hardwareid-registry-subkey.md)または[CompatibleID](compatibleid-registry-subkey.md)レジストリ サブキー。 リムーバブル デバイスの機能の詳細を上書きするを参照してください。 [DeviceOverrides レジストリ キー](deviceoverrides-registry-key.md)します。

**LocationPath**レジストリ サブキーには、デバイス ノードのみに、リムーバブル デバイスの機能の値が適用されます (*devnode*)、指定した場所のパスに存在します。 これにより、リムーバブル デバイスの機能、システムにインストールされているデバイスの 1 つのインスタンスに上書きを適用します。 その他のデバイスで、同じ**HardwareID**または**CompatibleID**他の場所のパスは受けませんリムーバブル デバイス機能オーバーライドします。

場所のパス文字列の形式は慣例により、 *ServiceName(BusSpecificLocation)* します。 たとえば、PCI デバイスを使用して、PCI (*XXYY*) ここで、 *XX*デバイス番号と*YY*関数の数です。 文字列は、そのバス関連デバイスに固有です。 プラグ アンド プレイ (PnP) マネージャーでは、devnode ツリー内の各ノードの場所のパスをアセンブルします。 各 devnode ツリーでは、その親 devnode 指定場所のパス文字列の末尾にそのサービス名の文字列を連結します。 そのため、場所のパスをツリー内の任意の devnode の位置を一意に識別できます。

次の表形式およびの要件の定義、 **LocationPath**レジストリ サブキー。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レジストリ サブキーの名前</th>
<th align="left">必須/省略可能</th>
<th align="left">形式の要件</th>
<th align="left">親のサブキー</th>
<th align="left">子のサブキー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>有効な&quot; <em>LocationPath</em> &quot;値</p></td>
<td align="left"><p>省略可能な (* または有効な場所のパスは、リムーバブル デバイスの機能のスコープのオーバーライドを指定するために必要)</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p><a href="locationpaths-registry-subkey.md" data-raw-source="[LocationPaths](locationpaths-registry-subkey.md)">LocationPaths</a>または<a href="childlocationpaths-registry-subkey.md" data-raw-source="[ChildLocationPaths](childlocationpaths-registry-subkey.md)">ChildLocationPaths</a></p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

いずれか、 **LocationPath**または[ \* ](--registry-subkey.md)レジストリ サブキーをリムーバブル デバイスの機能のスコープのオーバーライドを示すために存在する必要があります。

**LocationPath**サブキーを含める必要があります、**リムーバブル**かどうか、デバイスがリムーバブルであるかどうかを指定する DWORD の値。 次の表は、有効な定義**リムーバブル**値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リムーバブル値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>Devnode 削除不可と見なされます</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>Devnode をリムーバブルと見なす</p></td>
</tr>
</tbody>
</table>

 

指定された devnode の場所のパス文字列を次の手順でデバイス マネージャーを使用表示できます。

1.  デバイス マネージャーを開き、レジストリの上書きの適用を devnode を探します。 これを行うには、する必要がありますのビューを変更**接続によってデバイス**します。

2.  Devnode を右クリックし、をクリックして**プロパティ** をクリックし、**詳細**タブ。

3.  **プロパティ**ドロップダウン リストでは、検索、 **LocationPaths**プロパティ。 このプロパティでこの devnode の場所のパス文字列を表す、値のために使用する必要があります、 **LocationPath**レジストリ サブキー。

**注**  devnode がないことは、 **LocationPaths**値。 これは、この devnode またはその親のいずれかのドライバーが実装していないため、 [GUID_PNP_LOCATION_INTERFACE](https://msdn.microsoft.com/library/windows/hardware/ff546564)インターフェイス。 この場合は、親 devnode を確認する必要があります、 **LocationPaths**プロパティ。

 

**LocationPaths**固定バスの場所に配線で接続されているデバイスのリムーバブル デバイスの機能をオーバーライドするために使用するレジストリ サブキーが対象としています。 これは通常、ポータブル コンピューターでが発生し、次のデバイスが含まれています。

-   ワイヤレス ネットワーク アダプター

-   Bluetooth アダプター

-   キーボードまたはポインティング デバイス

これらのデバイスは、ユーザーが変更できない固定の場所で異なる内部バス上に存在します。 **LocationPaths**上書きリムーバブル デバイスの機能によって、特定のバスの場所にあるデバイスのみが影響を受けることを指定することができますをオーバーライドします。 オーバーライドは、これにより、同じを共有できる他のバスの場所でのデバイスに影響を与える[HardwareID](hardwareid-registry-subkey.md)または[CompatibleID](compatibleid-registry-subkey.md)サブキーを上書きターゲットとしての値。 これは、一般的なデバイスのみを指定するとき、 **CompatibleID**サブキーを受信トレイのドライバーと一致する値。

使用すると、 [ChildLocationPaths](childlocationpaths-registry-subkey.md)子 devnode のリムーバブル デバイスの機能をオーバーライドするレジストリ サブキーがデバイスの種類に関係なく、特定の場所にある子 devnode のみを対象とすると便利です。

たとえば、ラップトップには、内部と外部の両方のポートで内部の USB ハブがあります。 この USB ハブは、その内部のポートの外部にあるとして誤って報告される原因は場合、リムーバブルとして内部的にこれらのポートには、任意のデバイスが誤って認識されません。 同様に、内部のものとしては、すべてのポートが誤って報告され場合、は、任意の外部に接続されているデバイスは、ラップトップの nondetachable の一部である場合に扱われます。

外部 USB ポートに接続されているデバイスの場所のパス値を検出するには、任意のデバイスをポートに接続し、その場所のパスのプロパティを確認できます。 同じポートに接続されている他の USB デバイスは、親バスとポートを内部的に識別する方法を変更しないため、同じ場所のパスの値を受信する必要があります。

 

 





