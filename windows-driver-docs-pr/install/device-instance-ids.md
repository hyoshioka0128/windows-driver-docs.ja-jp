---
title: デバイス インスタンス ID
description: デバイス インスタンス ID は、システムでデバイスを一意に識別するシステム提供のデバイスの識別文字列です。
ms.assetid: 578973f4-463f-4707-8dc3-dff27b3d3052
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce4f37a4f3fecfb35c3e6ae952af9492fc737601
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536186"
---
# <a name="device-instance-id"></a>デバイス インスタンス ID


デバイス インスタンス ID は、システムでデバイスを一意に識別するシステム提供のデバイスの識別文字列です。 プラグ アンド プレイ (PnP) マネージャーでは、デバイスの各ノードにデバイス インスタンス ID が割り当てられます (*devnode*) システムの[デバイス ツリー](https://msdn.microsoft.com/library/windows/hardware/ff543194)します。




この文字列の形式では、[インスタンス ID](instance-ids.md)に連結して、[デバイス ID](device-ids.md)、次のように。

`<device-ID>\<instance-specific-ID>`

デバイス インスタンス ID、NULL 終端文字を除くの文字数は、MAX_DEVICE_ID_LEN 未満である必要があります。 この制約が適用されるすべてのフィールドの長さの合計と"\\"フィールドの区切り記号の間、*デバイス ID*と*インスタンス固有 ID*フィールド。

デバイス インスタンス ID は、システムの再起動の間で永続的です。

PCI デバイスのデバイス ID を連結したインスタンス ID ("1 & 08") の例を次に示します。

`PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02\1&08`

 

 





