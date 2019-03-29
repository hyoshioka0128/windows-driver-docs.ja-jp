---
title: Microsoft OS ContainerID 記述子の使用
description: Microsoft OS ContainerID 記述子の使用
ms.assetid: e51b1bc8-fd9d-40f9-b2ae-9f5886f57c7b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 194c94c2516d6083a40d6339d2626ef99f426b35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578408"
---
# <a name="using-microsoft-os-containerid-descriptors"></a>Microsoft OS ContainerID 記述子の使用


Microsoft のオペレーティング システム (OS) **ContainerID**記述子は、複数のシステム バスを使用して、デバイスの同時接続をサポートするデバイスで使用できます。 明示的に定義された Microsoft OS **ContainerID**記述子により、デバイスのすべてのノード (*devnode*)、USB バスでデバイスが同じデバイス コンテナーにグループ化されたを列挙します。

**注**  Microsoft OS を実装する場合**ContainerID**記述子、記述子の値は、コンテナー ID の競合を回避するためにすべてのデバイス上で一意である必要があります。

 

Microsoft OS **ContainerID**記述子は、デバイスは、1 つ以上のバスを使用して、デバイスへの同時接続をサポートしている場合に便利です。 この方法では、同じコンテナー ID は、デバイスでサポートされている各バスで使用されます。 これにより、オペレーティング システムが各バス上の関数が同じデバイス コンテナーの一部であるかどうかを判断できます。

Microsoft OS を使用する場合**ContainerID** USB デバイス内おく必要がある、次の点に注意してくださかった。

-   コンピューター (つまり、すべて外部デバイス) に統合されていないデバイスの場合は、これは Microsoft OS を常に提供するベスト プラクティス**ContainerID**記述子と、USB デバイスのハードウェアでのシリアル番号。 これにより、Windows のプラグ アンド プレイ (PnP) インフラストラクチャが正しく、デバイスによって公開されているすべてのデバイス機能をグループ化できることが保証されます。 Windows 7 以降のオペレーティング システムのコンポーネントは、デバイスの機能の適切なグループ化に依存します。 このプラクティスに従うと、Windows プラットフォーム上のデバイスの最適なユーザー エクスペリエンスが提供されます。

-   コンピューターが統合された USB デバイスが Microsoft OS を提供することはありません**ContainerID**記述子。 統合デバイスが正しく、コンピューターのデバイスのコンテナーをグループ化されていることを確認するをする場合、統合デバイスを ACPI BIOS の設定または USB ハブ既述子に依存する必要があります**DeviceRemovable**ポートのビットします。

 

 





