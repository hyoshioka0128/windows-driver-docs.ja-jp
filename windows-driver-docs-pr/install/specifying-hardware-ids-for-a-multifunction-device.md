---
title: 多機能デバイス用のハードウェア ID の指定
description: 多機能デバイス用のハードウェア ID の指定
ms.assetid: e45f7564-89a7-49c0-8011-69e5da3d5651
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c381d226c4dea840c7a26f511fbec2a4861548e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385883"
---
# <a name="specifying-hardware-ids-for-a-multifunction-device"></a>多機能デバイス用のハードウェア ID の指定


1 つ以上指定できます[ **HardwareID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))物理デバイスの要素。 これは、複数指定することで**HardwareID**親内の要素の値[ **HardwareIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))要素。 それぞれの値を一意に指定する必要があります[ハードウェア ID](hardware-ids.md)デバイス。

たとえば、Contoso, Ltd. という会社から単一関数の USB プリンター次**HardwareID**要素は、デバイスを定義するために使用できます。

```cpp
<HardwareIDList>
  <HardwareID>DOID:USB\VID_1234&PID_1234&REV_0000</HardwareID>
  <HardwareID>DOID:USB\VID_1234&PID_1234</HardwareID>
  <HardwareID>DOID:USBPRINT\Contoso_Ltd_Co9999/HardwareID>
</HardwareIDList>
```

デバイスが多機能デバイスの場合は、デバイス コンテナーは、すべてのハードウェア Id を組み合わせた) デバイス上の各ハードウェア関数。 デバイスのコンテナーとコンテナー Id の詳細については、次を参照してください。[コンテナー Id](container-ids.md)します。

次の図は、多機能デバイスの devnode とデバイスのコンテナー間の関係を示します。

![説明する図を 1 つのデバイス コンテナーに複数の devnode からハードウェア id を組み合わせること](images/hardwareid.png)

、多機能デバイスに応じて、これを決定できます[ハードウェア ID](hardware-ids.md)個別を使用して値が指定されて[ **HardwareID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))内の要素、 [**HardwareIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))要素。 任意の順序で複数のハードウェア Id を指定することができます、 **HardwareIDList**要素。 ただしの次の点に注意する必要があります。

-   特定の devnode、内で、オペレーティング システムでは、ハードウェア Id の順位付けは決定的です。 たとえば、前の図で*HardwareID1 1*は常にランク付けされたよりも高い*HardwareID1 2*と*HardwareID1 3*します。

-   オペレーティング システムは一貫してから 1 つ devnode 別 devnode からハードウェア ID よりも高いハードウェア ID を順位されません。 たとえば、前の図では、オペレーティング システム可能性がありますいない常にランク*HardwareID1 1*よりも高い*HardwareID2 1*します。

メタデータ パッケージは、順序またはランクには依存しないため、必ず[ハードウェア Id](hardware-ids.md)デバイス devnode 全体。 多機能デバイスのすべての関連するハードウェア Id を使用する必要があります、 [ **HardwareIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))デバイス メタデータ パッケージの要素。 これは、オペレーティング システムがハードウェア Id の順位付けに関係なく、メタデータ パッケージを選択することが保証されます。

に基づいて、 *devnode*の前の図に示すトポロジは、次の推奨事項を検討してください。

-   指定*HardwareID1 1*、 *HardwareID2-1*と*1-ハードウェア ID3*新しいデバイス メタデータ パッケージを指定する別のメタデータ パッケージが既にパブリッシュされている場合にのみ*HardwareID2 1*します。

    場合は、オペレーティング システムをランク付け*HardwareID2 1*よりも高い*HardwareID1 1*を検出および*HardwareID2 1*両方、古いマスター_キーと新しいメタデータ パッケージで指定された、オペレーティング システムの値に基づくメタデータ パッケージの選択、 [ **LastModifiedDate** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548624(v=vs.85)) XML 要素。 この場合、オペレーティング システムは、新しいメタデータ パッケージを選択します。

-   新しいメタデータ パッケージだけを表示する場合*HardwareID1 1*、ユーザーは場合は、オペレーティング システムには、新しいパッケージは選択しません*HardwareID2 1*ランク付けされてよりも高い*HardwareID1-1。*

メタデータ パッケージの選択と順位付けの詳細については、次を参照してください。 [、DMRC デバイス メタデータ パッケージを選択する方法](how-the-dmrc-selects-a-device-metadata-package.md)します。

 

 





