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
ms.openlocfilehash: e5a8a9ffd7a78d2f5d436a1a0eba3f478208e8de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388171"
---
# <a name="determining-when-to-send-a-waitwake-irp"></a>待機/ウェイク IRP を送信するタイミングの決定





デバイスの電源ポリシー送信待機/ウェイク Irp に代わって、デバイスを所有しているドライバーです。 このようなドライバーは、次のいずれかが発生すると待機/ウェイク IRP を送信する必要があります。

-   ドライバーがスリープ状態にデバイスを配置することが、デバイスは、外部のウェイク アップ シグナルへの応答でウェイク アップできる必要があります。

-   システムがスリープ状態になると、デバイスは、それがスリープ解除できる必要があります。

電源ポリシー所有者は、このような条件が迫っていないか前に待機/ウェイク IRP を送信する必要があります。 いつ D0、そのデバイスが IRP を送信できますが、それが別のセットの電源を処理中に IRP またはクエリ power IRP が送信する必要があります。 一般的な規則として、ドライバーは、プラグ アンド プレイの上司の処理中に、IRP を送信する必要があります[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)を要求した後初期化され、デバイスを開始します。

 

 




