---
title: デバイス ID
description: デバイス ID は、デバイスの列挙子によって報告された文字列です。 デバイスが 1 つだけのデバイス id。 デバイス ID がハードウェア ID と同じ形式
ms.assetid: a71b64bc-319e-4133-810b-7fd417cf0af8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2ee9b58bd89fba27d4f14933d6ffe2a8a19d447
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558797"
---
# <a name="device-id"></a>デバイス ID


デバイス ID は、デバイスのによって報告された文字列*列挙子*します。 デバイスが 1 つだけのデバイス id。 デバイス ID と同じ形式を持つ、[ハードウェア ID](hardware-ids.md)します。




プラグ アンド プレイ (PnP) マネージャーでは、デバイス ID を使用して、デバイスの列挙子のデバイス レジストリ キーの下のサブキーを作成します。

デバイス ID を取得するには、使用、 [ **IRP_MN_QUERY_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551679)を要求し、設定、 **Parameters.QueryId.IdType**フィールドを**BusQueryDeviceID**します。

 

 





