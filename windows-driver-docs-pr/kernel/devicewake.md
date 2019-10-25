---
title: DeviceWake
description: DeviceWake
ms.assetid: 3b82c095-1ee7-41e9-991e-ac0bcf959024
keywords:
- DeviceWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68f6aec1b46d96c20635ea2a384fc38a9e90b921
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828322"
---
# <a name="devicewake"></a>DeviceWake





[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の**devicewake**メンバーには、デバイスがウェイクアップイベントに信号を送ることができる最も低い (最も電力が少ない) デバイスの電源状態が含まれます。また、デバイスがに応答してスリープ解除できない場合は、 **powerdeviceunspecified**外部シグナル。

バスドライバーは、この値を設定します。 上位レベルのドライバーは、値をより高い電力状態に変更できます。 たとえば、バスドライバーで**Devicewake**をに設定しても、デバイススタックの上位にあるドライバーが d2 からのウェイクアップのみをサポートしている場合は、上位レベルのドライバーによって値が d2 に変更される可能性があります。

ドライバーが**Devicewake**を変更した場合は、 **devicewake**配列内のシステムからデバイスへのマッピングとの競合を避けるために[**systemwake**](systemwake.md)を変更することが必要になる場合もあります。 たとえば、バスドライバーが次のように設定しているとします。

-   **Devicestate**\[**PowerSystemSleeping1**\] = **PowerDeviceD1**

-   **Devicestate**\[**PowerSystemSleeping2**\] = **PowerDeviceD3**

-   **Devicewake** = **PowerDeviceD3**

-   **Systemwake** = **PowerSystemSleeping2**

上位レベルのドライバーによって、デバイスが D3 からシステムをウェイクアップできないと判断された場合、D2 以上の場合にのみ、 **Devicewake**を d2 に変更できます。 ただし、この変更により、S2 から D3 へのマッピングが不可能になります。 **Devicestate**配列は、デバイスが特定のシステム電源の状態に対してサポートできるデバイスの最大電源状態を一覧表示することに注意してください。 この例のシステム電源の状態が**PowerSystemSleeping2**である場合、デバイスの電源状態を**PowerDeviceD2**にすることはできません。 この問題を回避するには、ドライバーは**Systemwake** to **PowerSystemSleeping1**も変更する必要があります。 \* WakeFromD * **x*と **デバイス * * x*の設定にも同じことが当てはまります。 ドライバーは、 **systemwake**または**devicewake**に対して行われたすべての変更が、**WakeFromD * * x*および **デバイス * * x*値と競合しないようにする必要があります。 *WakeFromDx*と **デバイス * * x*の値には、ドライバーが変更できないハードウェアの特性が反映されます。

**Systemwake**と**devicewake**の両方のメンバーが0以外 (つまり、 **powersystemunspecified**) の場合、デバイスとそのドライバーはこのシステムでのウェイクアップをサポートします。

非 ACPI ハードウェアでは、 **Devicewake**メンバーにゼロ (**powersystemunspecified**) が含まれています。

 

 




