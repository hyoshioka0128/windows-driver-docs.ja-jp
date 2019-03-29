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
ms.openlocfilehash: 30232cb65c87e3442d3dde6d99c43460bd74eb4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582280"
---
# <a name="framework-io-request-object"></a>フレームワーク I/O 要求オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework I/O 要求オブジェクトが、ドライバーに公開される、 [IWDFIoRequest](https://msdn.microsoft.com/library/windows/hardware/ff558985)インターフェイス。 I/O 操作の詳細情報がカプセル化します。 すべての I/O 要求は、framework の I/O 要求のオブジェクトとして表されます。 リフレクター通知ドライバーのホスト プロセス、reflector は、I/O 要求パケット (IRP) を受信すると、Microsoft Win32 への呼び出しなど、アプリケーションの I/O 操作の結果として[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)または**ReadFile**関数。 Reflector の通知への応答として、フレームワークでは、新しい要求オブジェクトを構築し、適切な I/O キューに配置されます。 キューの構成とユーザー モード ドライバーによって選択されたロックのモデルは、ドライバーに要求を提示する場合を決定します。 詳細については、次を参照してください。 [I/O キューのディスパッチ モードを構成する](configuring-dispatch-mode-for-an-i-o-queue.md)と[コールバックの同期モードを指定する](specifying-a-callback-synchronization-mode.md)します。

 

 





