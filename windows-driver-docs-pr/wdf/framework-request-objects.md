---
title: フレームワーク要求オブジェクト
description: フレームワーク要求オブジェクト
ms.assetid: 564f3600-4784-4a37-ac13-38338c38a9d2
keywords:
- I/o 要求 WDK KMDF、要求オブジェクト
- 要求オブジェクト WDK KMDF
- 要求処理 WDK KMDF、要求オブジェクト
- フレームワークオブジェクト WDK KMDF、i/o 要求オブジェクト
- 要求オブジェクト WDK KMDF、要求オブジェクトについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9c117b7a199c61ee5a40ec2c6e463a12623fadd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845130"
---
# <a name="framework-request-objects"></a>フレームワーク要求オブジェクト





フレームワーク要求オブジェクトは、i/o マネージャーがドライバーに送信した i/o 要求を表します。 フレームワークベースのドライバーは、[フレームワークの要求オブジェクトメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/)を呼び出すことによって、各 i/o 要求を処理します。

各 i/o 要求には WDM *i/o 要求パケット*([**irp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)構造体) が含まれていますが、通常、フレームワークベースのドライバーは、irp 構造体にアクセスする必要はありません。

## <a name="in-this-section"></a>このセクションの内容


-   [フレームワークの要求オブジェクトの作成](creating-framework-request-objects.md)
-   [要求オブジェクトコンテキストの使用](using-request-object-context.md)
-   [所有権の要求](request-ownership.md)
-   [I/o 要求の処理](processing-i-o-requests.md)
-   [I/o 要求に関する情報の取得](obtaining-information-about-an-i-o-request.md)
-   [WDF ドライバー (KMDF または UMDF) でのデータバッファーへのアクセス](accessing-data-buffers-in-wdf-drivers.md)
-   [UMDF ドライバーでのバッファーアクセスメソッドの管理](managing-buffer-access-methods-in-umdf-drivers.md)
-   [フレームワークの要求オブジェクトの再利用](reusing-framework-request-objects.md)

 

 





