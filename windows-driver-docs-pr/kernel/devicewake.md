---
title: DeviceWake
description: DeviceWake
ms.assetid: 3b82c095-1ee7-41e9-991e-ac0bcf959024
keywords:
- DeviceWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0324877a14b1b560aa01d5e113740bad398c330
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530846"
---
# <a name="devicewake"></a>DeviceWake





**DeviceWake**のメンバー [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)最低 (最小電力) デバイス電源の状態、デバイスが、ウェイクを通知が含まれていますイベント、または**PowerDeviceUnspecified**デバイスは、外部からの信号に対してスリープ解除できない場合。

バス ドライバーでは、この値を設定します。 高度なドライバーは、パワー状態に値を変更できます。 たとえば、バス ドライバー設定**DeviceWake** D3 には、デバイス スタック サポート ウェイク アップのみ D2 からのドライバーをさらより高度なドライバーは、D2 に値を変更できます。

ドライバーの変更された場合に注意してください**DeviceWake**、変更する必要がありますも[ **SystemWake** ](systemwake.md)システムからデバイスへのマッピングとの競合を回避するために、 **DeviceState**配列。 たとえば、バス ドライバー、次の設定を想定します。

-   **DeviceState**\[**PowerSystemSleeping1**\] = **PowerDeviceD1**

-   **DeviceState**\[**PowerSystemSleeping2**\] = **PowerDeviceD3**

-   **DeviceWake** = **PowerDeviceD3**

-   **SystemWake** = **PowerSystemSleeping2**

D3、システムのスリープを解除できません、デバイス D2 からのみまたはそれ以降は変更できますより高度なドライバーが判断した場合**DeviceWake** D2 にします。 ただし、この変更は、ことは不可能な D3 に S2 からマッピングをさせます。 注意、 **DeviceState**配列には、特定のシステム電源の状態のデバイスをサポートできる最も高いデバイスの電源状態が一覧表示されます。 場合の例では、システム電源の状態が**PowerSystemSleeping2**、デバイスの電源状態にすることはできません**PowerDeviceD2**します。 この問題を排除するために、ドライバーを変更する必要がありますも**SystemWake**に**PowerSystemSleeping1**します。 場合も同様、**WakeFromD * * * x*と **DeviceD * * * x*設定します。 ドライバーのいずれかの変更されることになりますことを確認する必要があります**SystemWake**または**DeviceWake**と競合していない、**WakeFromD * * * x*と **DeviceD * * *x*値。 値*WakeFromDx*と **DeviceD * * * x*ドライバーを変更することはできません、ハードウェアの特性を反映します。

両方、 **SystemWake**と**DeviceWake**メンバーは、0 以外の場合 (つまり、いない**PowerSystemUnspecified**)、後、デバイスとそのドライバーのサポート、ウェイク アップのこのシステムで。

非 ACPI のハードウェア上で、 **DeviceWake**メンバーに 0 が含まれています (**PowerSystemUnspecified**)。

 

 




