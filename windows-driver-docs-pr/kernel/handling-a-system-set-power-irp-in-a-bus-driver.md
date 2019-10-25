---
title: バス ドライバーでのシステム電源設定 IRP の処理
description: バス ドライバーでのシステム電源設定 IRP の処理
ms.assetid: e88344bd-4223-4cd5-9428-201d46c6dbb4
keywords:
- パワー Irp WDK 電源管理の設定
- バスドライバーの WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e37faf79a6a14a03a95933b60c99bc0c09d58ac6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838678"
---
# <a name="handling-a-system-set-power-irp-in-a-bus-driver"></a>バス ドライバーでのシステム電源設定 IRP の処理





バスドライバーがシステムセット-電源 IRP を受信する場合、次の手順を実行する必要があります。

1.  [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して、次の電源 IRP を開始します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)。

2.  **Irp-&gt;iostatus. status**を STATUS\_SUCCESS に設定します。 ドライバーがシステム設定-電源 IRP を失敗させることはできません。

3.  [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出し、IRP を完了するための IO\_\_の増分値を指定します。

バスドライバーは、デバイスの電源状態を要求する電源 IRP を受信するまで、デバイスの電源設定を変更しません。

 

 




