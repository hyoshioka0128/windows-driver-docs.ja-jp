---
title: フレームワーク要求オブジェクト
description: フレームワーク要求オブジェクト
ms.assetid: 564f3600-4784-4a37-ac13-38338c38a9d2
keywords:
- I/O 要求の WDK KMDF、要求オブジェクト
- 要求オブジェクト WDK KMDF
- 要求の WDK KMDF、要求オブジェクトの処理
- フレームワークは、WDK KMDF、I/O 要求オブジェクトをオブジェクトします。
- 要求オブジェクト WDK KMDF、要求オブジェクトの概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d933a75c746dc341df1a3663f813d76616cd6cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384445"
---
# <a name="framework-request-objects"></a>フレームワーク要求オブジェクト





Framework 要求オブジェクトは、I/O マネージャーがドライバーに送信 I/O 要求を表します。 フレームワーク ベースのドライバーでは、各 I/O 要求を処理を呼び出して[framework 要求オブジェクトのメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/)します。

I/O 要求ごとに、WDM が含まれています*I/O 要求パケット*([**IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)構造)、framework ベースのドライバーが IRP 構造体にアクセスする必要はありません通常します。

## <a name="in-this-section"></a>このセクションの内容


-   [Framework 要求オブジェクトを作成します。](creating-framework-request-objects.md)
-   [要求オブジェクトのコンテキストを使用](using-request-object-context.md)
-   [所有権を要求](request-ownership.md)
-   [I/O 要求の処理](processing-i-o-requests.md)
-   [I/O 要求に関する情報を取得します。](obtaining-information-about-an-i-o-request.md)
-   [WDF ドライバー (KMDF または UMDF) 内のデータ バッファーへのアクセス](accessing-data-buffers-in-wdf-drivers.md)
-   [UMDF ドライバーでバッファーへのアクセス方法の管理](managing-buffer-access-methods-in-umdf-drivers.md)
-   [フレームワークの要求オブジェクトを再利用](reusing-framework-request-objects.md)

 

 





