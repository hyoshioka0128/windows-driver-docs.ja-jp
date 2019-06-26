---
title: デバイスの停止
description: デバイスの停止
ms.assetid: 65a47e7b-aabd-4b55-8fa6-c3482da1cc84
keywords:
- PnP WDK カーネルでは、デバイスを停止しています
- プラグ アンド プレイ WDK カーネル、デバイスを停止しています
- PnP デバイスを停止しています
- Irp WDK PnP 停止します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8b77eb3f3efd71dad0bea08d7fa1125c4eb599b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382977"
---
# <a name="stopping-a-device"></a>デバイスの停止





PnP マネージャーでは、次の状況でのデバイスを停止するドライバーが送信されます。

-   デバイスで使用されているハードウェア リソースを再調整します。 再調整する方法は、既に使用されているリソースを必要とする新しいデバイスが列挙されたときに通常必要があります。

-   デバイス マネージャーの要求に対する応答でデバイスを無効にする (Windows 98/自分のみ)。 Windows 2000 および Windows の送信の以降のバージョンでこのような状況は; Irp を削除します。参照してください[理解するときに削除 Irp が発行](understanding-when-remove-irps-are-issued.md)します。

-   失敗後[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求 (Windows 98/自分のみ)

このセクションでは、次のトピックについて説明します。

[リソースを再調整するデバイスを停止しています](stopping-a-device-to-rebalance-resources.md)

[無効にするデバイスを停止する (Windows 98/Me)](stopping-a-device-to-disable-it--windows-98-me-.md)

[失敗した開始後にデバイスを停止する (Windows 98/Me)](stopping-a-device-after-a-failed-start--windows-98-me-.md)

[停止 Irp の処理 (Windows 2000 以降)](handling-stop-irps--windows-2000-and-later-.md)

[停止 Irp の処理 (Windows 98/Me)](handling-stop-irps--windows-98-me-.md)

 

 




