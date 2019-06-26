---
title: デバイス ID
description: デバイス ID は、デバイスの列挙子によって報告された文字列です。 デバイスが 1 つだけのデバイス id。 デバイス ID がハードウェア ID と同じ形式
ms.assetid: a71b64bc-319e-4133-810b-7fd417cf0af8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 565b64f9f27540cf0468b98847bc44300d4b8c00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387133"
---
# <a name="device-id"></a>デバイス ID


デバイス ID は、デバイスのによって報告された文字列*列挙子*します。 デバイスが 1 つだけのデバイス id。 デバイス ID と同じ形式を持つ、[ハードウェア ID](hardware-ids.md)します。




プラグ アンド プレイ (PnP) マネージャーでは、デバイス ID を使用して、デバイスの列挙子のデバイス レジストリ キーの下のサブキーを作成します。

デバイス ID を取得するには、使用、 [ **IRP_MN_QUERY_ID** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)を要求し、設定、 **Parameters.QueryId.IdType**フィールドを**BusQueryDeviceID**します。

 

 





