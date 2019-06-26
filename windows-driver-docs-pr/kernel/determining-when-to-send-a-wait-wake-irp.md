---
title: 待機/ウェイク IRP を送信するタイミングの決定
description: 待機/ウェイク IRP を送信するタイミングの決定
ms.assetid: a56cfccc-b44b-4ec5-836b-3a9711ef5f1f
keywords:
- タイミング待機/ウェイク Irp WDK 電源管理
- 送信待機/ウェイク Irp
- Irp WDK の電源管理のウェイク/待機を送信します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13bcd0548c378c0d47aad223cd2f363198fc636b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371264"
---
# <a name="determining-when-to-send-a-waitwake-irp"></a>待機/ウェイク IRP を送信するタイミングの決定





デバイスの電源ポリシー送信待機/ウェイク Irp に代わって、デバイスを所有しているドライバーです。 このようなドライバーは、次のいずれかが発生すると待機/ウェイク IRP を送信する必要があります。

-   ドライバーがスリープ状態にデバイスを配置することが、デバイスは、外部のウェイク アップ シグナルへの応答でウェイク アップできる必要があります。

-   システムがスリープ状態になると、デバイスは、それがスリープ解除できる必要があります。

電源ポリシー所有者は、このような条件が迫っていないか前に待機/ウェイク IRP を送信する必要があります。 いつ D0、そのデバイスが IRP を送信できますが、それが別のセットの電源を処理中に IRP またはクエリ power IRP が送信する必要があります。 一般的な規則として、ドライバーは、プラグ アンド プレイの上司の処理中に、IRP を送信する必要があります[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を要求した後初期化され、デバイスを開始します。

 

 




