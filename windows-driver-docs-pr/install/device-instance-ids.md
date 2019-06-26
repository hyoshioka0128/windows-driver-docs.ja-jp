---
title: デバイス インスタンス ID
description: デバイス インスタンス ID は、システムでデバイスを一意に識別するシステム提供のデバイスの識別文字列です。
ms.assetid: 578973f4-463f-4707-8dc3-dff27b3d3052
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9857ee9a7e697cf14153f7b39e6ca74228edd81
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387129"
---
# <a name="device-instance-id"></a>デバイス インスタンス ID


デバイス インスタンス ID は、システムでデバイスを一意に識別するシステム提供のデバイスの識別文字列です。 プラグ アンド プレイ (PnP) マネージャーでは、デバイスの各ノードにデバイス インスタンス ID が割り当てられます (*devnode*) システムの[デバイス ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)します。




この文字列の形式では、[インスタンス ID](instance-ids.md)に連結して、[デバイス ID](device-ids.md)、次のように。

`<device-ID>\<instance-specific-ID>`

デバイス インスタンス ID、NULL 終端文字を除くの文字数は、MAX_DEVICE_ID_LEN 未満である必要があります。 この制約が適用されるすべてのフィールドの長さの合計と"\\"フィールドの区切り記号の間、*デバイス ID*と*インスタンス固有 ID*フィールド。

デバイス インスタンス ID は、システムの再起動の間で永続的です。

PCI デバイスのデバイス ID を連結したインスタンス ID ("1 & 08") の例を次に示します。

`PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02\1&08`

 

 





