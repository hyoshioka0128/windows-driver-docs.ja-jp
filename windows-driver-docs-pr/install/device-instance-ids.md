---
title: デバイス インスタンス ID
description: デバイスインスタンス ID はシステムによって提供されるデバイス id 文字列で、システム内のデバイスを一意に識別します。
ms.assetid: 578973f4-463f-4707-8dc3-dff27b3d3052
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 714f0771a34091002ebfdf5941c09c55e1f45237
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007625"
---
# <a name="device-instance-id"></a>デバイス インスタンス ID


デバイスインスタンス ID はシステムによって提供されるデバイス id 文字列で、システム内のデバイスを一意に識別します。 プラグアンドプレイ (PnP) マネージャーは、デバイスインスタンス ID をシステムの[デバイスツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)内の各デバイスノード (*devnode*) に割り当てます。




この文字列の形式は、次のように、[デバイス id](device-ids.md)に連結された[インスタンス id](instance-ids.md)で構成されます。

`<device-ID>\<instance-specific-ID>`

NULL ターミネータを除くデバイスインスタンス ID の文字数は、MAX_DEVICE_ID_LEN よりも小さくする必要があります。 この制約は、すべてのフィールドの長さの合計と、*デバイス ID*フィールドと*インスタンス固有 ID*フィールド間の "\\" フィールド区切り記号に適用されます。

デバイスインスタンス ID は、システムの再起動にわたって永続的です。

PCI デバイスのデバイス ID に連結されたインスタンス ID ("1 & 08") の例を次に示します。

`PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02\1&08`

 

 





