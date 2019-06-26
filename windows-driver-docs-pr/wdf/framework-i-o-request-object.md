---
title: フレームワーク I/O 要求オブジェクト
description: フレームワーク I/O 要求オブジェクト
ms.assetid: e48437ee-597d-45b1-9093-8d5921356af5
keywords:
- UMDF オブジェクト WDK、I/O 要求オブジェクトします。
- フレームワークは、WDK UMDF、I/O 要求オブジェクトをオブジェクトします。
- I/O 要求オブジェクト WDK UMDF
- IWDFIoRequest
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85fd159c2d0473d3de748df0eb0c9cd7395f84d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384469"
---
# <a name="framework-io-request-object"></a>フレームワーク I/O 要求オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework I/O 要求オブジェクトが、ドライバーに公開される、 [IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest)インターフェイス。 I/O 操作の詳細情報がカプセル化します。 すべての I/O 要求は、framework の I/O 要求のオブジェクトとして表されます。 リフレクター通知ドライバーのホスト プロセス、reflector は、I/O 要求パケット (IRP) を受信すると、Microsoft Win32 への呼び出しなど、アプリケーションの I/O 操作の結果として[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)または**ReadFile**関数。 Reflector の通知への応答として、フレームワークでは、新しい要求オブジェクトを構築し、適切な I/O キューに配置されます。 キューの構成とユーザー モード ドライバーによって選択されたロックのモデルは、ドライバーに要求を提示する場合を決定します。 詳細については、次を参照してください。 [I/O キューのディスパッチ モードを構成する](configuring-dispatch-mode-for-an-i-o-queue.md)と[コールバックの同期モードを指定する](specifying-a-callback-synchronization-mode.md)します。

 

 





