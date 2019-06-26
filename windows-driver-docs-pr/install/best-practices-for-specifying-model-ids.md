---
title: モデル ID の指定のベスト プラクティス
description: モデル ID の指定のベスト プラクティス
ms.assetid: ed0cdfb4-1de8-4b4f-8bab-7c5e06cf96f6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0382d8ac10b20f315667855571f715eed15df303
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385295"
---
# <a name="best-practices-for-specifying-model-ids"></a>モデル ID の指定のベスト プラクティス


モデル Id は、物理デバイスのビジネス定義または在庫保管単位 (SKU) に基づいています。 各モデルの ID は、すべての製造元とモデルの物理デバイスに一意である必要があります。

次の一覧には、ハードウェア Id と物理デバイスのモデル Id の違いについて説明します。

-   [ハードウェア Id](hardware-ids.md) 1 つまたは複数を使用して指定[ **HardwareID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))内の XML 要素、 [ **HardwareIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546121(v=vs.85)) XML要素。 各**HardwareID**値は、バスに固有の値に基づくハードウェア関数を指定します。 デバイス インスタンスにデバイス ドライバーをマップするハードウェア Id を使用できます。

    たとえば、同じハードウェア ID を持つ 2 つのデバイスは、同じドライバーによって使用される機能インターフェイスを共有します。

-   モデル Id が 1 つまたは複数を使用して、指定された[ **ModelID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))内の XML 要素、 [ **ModelIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549303(v=vs.85)) XML 要素。 モデル Id は、供給元 (OEM) または独立系ハードウェア ベンダー (IHV) バスまたはインターフェイスのテクノロジの独立した物理デバイスを一意に識別するを許可します。

    たとえば、別のモデル Id を持つ 2 つのデバイスには、そのコンポーネントの同じハードウェア Id があります。

-   [ハードウェア Id](hardware-ids.md)デバイス メタデータ パッケージを特定のバスまたはインターフェイス上のデバイスのインスタンスにマップするために使用します。

-   デバイス メタデータ パッケージをコンピューターにデバイスを接続する方法に関係なく、物理デバイスにマップするモデル Id が使用されます。

[ **ModelIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549303(v=vs.85)) XML 要素は必要な場合にのみ、 [ **HardwareIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))で要素が指定されていない、 [**PackageInfo** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549574(v=vs.85)) XML データ。 指定されている場合、 **ModelIDList**要素は、1 つまたは複数を含める必要があります[ **ModelID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))デバイスをサポートする各関数の一意のモデル ID を指定する要素。

場合、 [ **PackageInfo** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549574(v=vs.85)) XML データを含む、 [ **HardwareIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))と[ **ModelIDList**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549303(v=vs.85))要素、オペレーティング システムを使用して、次の規則のデバイスがデバイス メタデータ パッケージで指定されたかどうかを決定する場合。

-   デバイスにモデル ID がある場合は、オペレーティング システムが内の一致を検索しません、 **HardwareIDList**要素。

-   それ以外の場合、オペレーティング システムの検索、 **HardwareIDList**デバイスのハードウェア ID の一致する要素。

指定できるかどうか、デバイス メタデータ パッケージは、複数のデバイス モデルやモデル Id をサポートする、 [ **ModelID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))各デバイス モデルの要素。

例を次に、 [ **ModelIDList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549303(v=vs.85))要素を複数持つ**ModelID**要素。

```cpp
<ModelIDList>
<ModelID>825AAB98-18EE-4FE2-9472-197D1D00FE31</ModelID>
<ModelID>23F64715-AC4A-4DC4-B554-C8D56E43FE8B</ModelID>
</ModelIDList>
```

形式の要件の詳細については、 **ModelID** 、XML 要素を参照してください[ **ModelID**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))します。

 

 





