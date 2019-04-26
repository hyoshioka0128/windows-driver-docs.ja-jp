---
title: フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の失敗
description: フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の失敗
ms.assetid: 7c4ceb8e-94f4-4ff7-9d45-1094e9a861fd
keywords:
- クエリ power Irp WDK の電源管理
- フィルター ドライバー WDK の電源管理
- 関数のドライバー WDK の電源管理
- クエリ power Irp の失敗
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c453890a3f68b23cbf02d0ef7fd16fb9dd59684f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359990"
---
# <a name="failing-a-system-query-power-irp-in-a-filter-or-function-driver"></a>フィルター ドライバーまたはファンクション ドライバーでのシステム電源クエリ IRP の失敗





(これは、デバイスの電源ポリシー所有者ではありません)、フィルターまたは関数のドライバーが失敗することが、 [ **IRP\_MN\_クエリ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)かどうかは、次のいずれかの要求true の場合:

-   デバイスを有効にすると、ウェイク アップし、要求されたシステムの電源状態の値より小さい電源の[ **SystemWake**](systemwake.md)デバイスが、システムを wake 最小電源の状態を指定します。 たとえば S2 から、S3 からではなく、システムのスリープを解除するデバイスは、s3 の場合、クエリが失敗するが s2 の場合、クエリは成功します。

-   要求された状態に対応するデバイスの電源状態を入力することにより、開いているモデム接続などのデータが失われます操作を破棄するドライバー。 ドライバーことはほとんどありませんが失敗をクエリします。 このためほとんどの状況では、アプリケーションは、このような場合を処理します。

失敗する、 **IRP\_MN\_クエリ\_POWER**要求のシステム電源の状態をドライバーは、次の手順を実行する必要があります。

1.  呼び出す[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)をドライバーが IRP の [次へ] のパワーを処理する準備が整っているかを示します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ)

2.  設定**Irp -&gt;IoStatus.Status**障害状態と呼び出しに[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)、IO を指定する\_いいえ\_インクリメントします。 さらに、デバイス スタックを IRP を渡さないでください。

3.  呼び出す[ **IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)以前に取得したロックを解除します。

4.  エラー状態を返す、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

 

 




