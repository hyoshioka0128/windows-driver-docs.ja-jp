---
title: デバイス インスタンス ID
description: デバイス インスタンス ID はシステム提供のデバイス ID 文字列で、システム内のデバイスを一意に識別します。
ms.assetid: 578973f4-463f-4707-8dc3-dff27b3d3052
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 714f0771a34091002ebfdf5941c09c55e1f45237
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007625"
---
# <a name="device-instance-id"></a>デバイス インスタンス ID


デバイス インスタンス ID はシステム提供のデバイス ID 文字列で、システム内のデバイスを一意に識別します。 プラグ アンド プレイ (PnP) マネージャーでは、デバイス インスタンス ID が、システムの[デバイス ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)の各デバイス ノード (*devnode*) に割り当てられます。




この文字列の形式は、次のように [デバイス ID](device-ids.md) に連結されている[インスタンス ID](instance-ids.md) で構成されます。

`<device-ID>\<instance-specific-ID>`

NULL ターミネーターを除くデバイス インスタンス ID の文字数は、MAX_DEVICE_ID_LEN 未満にする必要があります。 この制約は、すべてのフィールドの長さと、*デバイス ID* と*インスタンス固有 ID* フィールドの間の "\\" フィールド区切り記号の合計に適用されます。

デバイス インスタンス ID は、システムの再起動にわたって永続的です。

PCI デバイスのデバイス ID に連結されたインスタンス ID ("1&08") の例を次に示します。

`PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02\1&08`

 

 





