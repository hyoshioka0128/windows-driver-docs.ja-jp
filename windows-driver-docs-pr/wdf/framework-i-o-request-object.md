---
title: フレームワーク I/O 要求オブジェクト
description: フレームワーク I/O 要求オブジェクト
ms.assetid: e48437ee-597d-45b1-9093-8d5921356af5
keywords:
- UMDF オブジェクト WDK、i/o 要求オブジェクト
- フレームワークオブジェクト WDK UMDF、i/o 要求オブジェクト
- I/o 要求オブジェクト WDK UMDF
- IWDFIoRequest
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e449622937df9c028b3ca5d8b91ac85ab336870
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210372"
---
# <a name="framework-io-request-object"></a>フレームワーク I/O 要求オブジェクト


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

フレームワークの i/o 要求オブジェクトは、 [IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)インターフェイスによってドライバーに公開されます。 I/o 操作の詳細をカプセル化します。 すべての i/o 要求は、フレームワーク i/o 要求オブジェクトとして表されます。 リフレクタは、Microsoft Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)または**ReadFile**関数の呼び出しなど、アプリケーションの i/o 操作の結果として、リフレクターが I/O 要求パケット (IRP) を受信すると、ドライバーホストプロセスに通知します。 フレームワークは、リフレクター通知に応答して、新しい要求オブジェクトを構築し、適切な i/o キューに配置します。 要求がドライバーに提示されるタイミングは、ユーザーモードドライバーによって選択されたキュー構成とロックモデルによって決まります。 詳細については、「 [I/o キューのディスパッチモードの構成](configuring-dispatch-mode-for-an-i-o-queue.md)」および「[コールバック同期モードの指定](specifying-a-callback-synchronization-mode.md)」を参照してください。

 

 





