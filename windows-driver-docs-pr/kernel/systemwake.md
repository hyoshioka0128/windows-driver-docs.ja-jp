---
title: SystemWake
description: SystemWake
ms.assetid: 77390637-bb92-4634-a407-9a409a8a8acd
keywords:
- SystemWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72c5f9af3d512d091bd40e475467d41adf17ea9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836126"
---
# <a name="systemwake"></a>SystemWake





[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の**systemwake**メンバーには、デバイスがシステムをスリープ解除できる最も低い (電源が最も低い) システム電源の状態が含まれています。また、デバイスがシステムをスリープ解除できない場合は、 **powersystemunspecified**を含みます。

バスドライバーは、デバイスを列挙するときにこの値をに設定します。 上位レベルのドライバーは、値をより高い電力の状態に変更できますが、それを低電力の状態に変更することはできません。 たとえば、バスドライバーによって**Systemwake**が S3 に設定されているにもかかわらず、デバイススタックの上にあるドライバーが s2 からのウェイクアップのみをサポートしている場合は、上位レベルのドライバーによって値が s2 に変更される可能性があります。 ドライバーが**Systemwake**を変更した場合は、次のセクションで説明するように、 [**devicewake**](devicewake.md)を変更することが必要になる場合もあります。

ドライバーは、変更された値をデバイススタックの逆方向に伝達する必要はほとんどありません。 変更によってデバイスの機能が制限されるため、下位のドライバーには処理できない要求は表示されません。 前の例では、上位レベルのドライバーが、S2 よりも低い電力状態からシステムをウェイクアップするよう要求していないので、低いドライバーはそのような要求を認識しません。 ただし、下位のドライバーが変更を認識しなければならない場合は、 [ **\_\_irp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)の処理中に[ **\_の\_クエリ機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)を使用して、そのデバイススタックに PnP IRP\_送信できます。

**Systemwake**と**devicewake**の両方のメンバーが0以外 (つまり、 **powersystemunspecified**) の場合、デバイスとそのドライバーはこのシステムでのウェイクアップをサポートします。

非 ACPI ハードウェアでは、このメンバーには常にゼロ (**Powersystemunspecified**) が含まれます。

 

 




