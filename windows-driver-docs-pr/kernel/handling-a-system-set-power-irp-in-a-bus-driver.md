---
title: バス ドライバーでのシステム電源設定 IRP の処理
description: バス ドライバーでのシステム電源設定 IRP の処理
ms.assetid: e88344bd-4223-4cd5-9428-201d46c6dbb4
keywords:
- セット power Irp WDK の電源管理
- バス ドライバー WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 482e495e7806b24659e43b0aeade26094e8b883c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359825"
---
# <a name="handling-a-system-set-power-irp-in-a-bus-driver"></a>バス ドライバーでのシステム電源設定 IRP の処理





バス ドライバーがシステムを受信するとセット power IRP を次の手順を実行にする必要があります。

1.  呼び出す[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776) IRP の [次へ] のパワーを開始します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ。)

2.  設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。 ドライバーは、システムをフェールバックできません IRP の出力を設定します。

3.  呼び出す[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)、IO を指定する\_いいえ\_IRP の完了をインクリメントします。

パワー デバイスの電源状態を要求する IRP を受信するまで、バス ドライバーによるデバイスの電源設定は変わりません。

 

 




