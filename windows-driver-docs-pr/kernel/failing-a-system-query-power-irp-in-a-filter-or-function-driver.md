---
title: フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の失敗
description: フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の失敗
ms.assetid: 7c4ceb8e-94f4-4ff7-9d45-1094e9a861fd
keywords:
- クエリ-電源 Irp の WDK 電源管理
- フィルタードライバーの WDK 電源管理
- 関数ドライバー WDK の電源管理
- クエリの失敗-電源 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7362d8487c4611e0a257903e384770f19ce1dedc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836718"
---
# <a name="failing-a-system-query-power-irp-in-a-filter-or-function-driver"></a>フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の失敗





次のいずれかに該当する場合は、フィルターまたは関数ドライバー (デバイスの電源ポリシーの所有者ではない) が、 [**IRP\_\_クエリ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)要求に失敗する可能性があります。

-   デバイスでウェイクアップが有効になっていて、要求されたシステム電源の状態が[**Systemwake**](systemwake.md)の値を下回っている。これは、デバイスがシステムをスリープ解除できる最小電力状態を指定します。 たとえば、S3 からではなく S2 からシステムをウェイクアップできるデバイスでは、S3 のクエリは失敗しますが、S2 のクエリは成功します。

-   要求された状態に対応するデバイスの電源状態を入力すると、開いているモデム接続など、データを失う可能性のある操作がドライバーによって強制的に破棄されます。 ドライバーがこの理由でクエリに失敗することはめったにありません。ほとんどの場合、アプリケーションはこのような状況を処理します。

システムの電源状態に対する**電源要求\_の IRP\_\_** を失敗させるには、次の手順を実行する必要があります。

1.  [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出して、ドライバーが次の電源 IRP を処理できるように準備されていることを示します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)

2.  **Irp-&gt;iostatus. Status**をエラー状態に設定し、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。 IO\_\_増分を指定します。 IRP をデバイススタックの下位に渡すことはできません。

3.  [**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)を呼び出して、以前に取得したロックを解放します。

4.  [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンからエラー状態を返します。

 

 




