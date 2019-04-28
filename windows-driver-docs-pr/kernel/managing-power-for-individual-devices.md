---
title: 個々のデバイスの電源の管理
description: 個々のデバイスの電源の管理
ms.assetid: 95c7e900-5d51-4eb7-8780-1c40befa3599
keywords:
- 電源管理の WDK カーネル、デバイスの管理
- デバイスの電源管理の WDK カーネル
- システム電源の状態の WDK カーネル
- WDK カーネルの電源を節約します。
- 電源の状態の WDK カーネルを変更します。
- Irp WDK の電源管理
- I/O 要求パケット WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d7df6d5266e19b0d8cde98506123533e13183eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380264"
---
# <a name="managing-power-for-individual-devices"></a>個々のデバイスの電源の管理





ドライバーが応答することで、デバイスの電源を管理[システムの電源状態](system-power-states.md)変更を検出し、アイドル状態のデバイスをシャット ダウンと、必要なときにデバイスの電源を投入します。

このセクションでは、デバイスの電源管理に関連する次のトピックについて説明します。

[デバイスの電源の状態](device-power-states.md)

[アイドル状態のデバイスを検出します。](detecting-an-idle-device.md)

[デバイスの電源ポリシーを管理します。](managing-device-power-policy.md)

[IRP の処理\_MN\_設定\_電源状態のデバイスの電源](handling-irp-mn-set-power-for-device-power-states.md)

[IRP の処理\_MN\_クエリ\_電源状態のデバイスの電源](handling-irp-mn-query-power-for-device-power-states.md)

[IRP を送信する\_MN\_クエリ\_電源や IRP\_MN\_設定\_電源状態のデバイスの電源](sending-irp-mn-query-power-or-irp-mn-set-power-for-device-power-states.md)

[アイドル状態のデバイスを検出します。](detecting-an-idle-device.md)

[ドライバーで D3cold のサポート](supporting-d3cold-in-a-driver.md)

 

 




