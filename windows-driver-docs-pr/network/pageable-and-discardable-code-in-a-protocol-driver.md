---
title: プロトコル ドライバーのページ可能で破棄可能なコード
description: プロトコル ドライバーのページ可能で破棄可能なコード
ms.assetid: acc27690-cdc3-433c-85c4-489501ea3d26
keywords:
- プロトコルドライバー WDK ネットワーク、ページング可能で破棄可能なコード
- NDIS プロトコルドライバー WDK、ページング可能で破棄可能なコード
- ページング可能かつ破棄不可能なコード (WDK NDIS プロトコル)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae5aa75a6611d953ce40f1708fae594ffb4dcf96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843704"
---
# <a name="pageable-and-discardable-code-in-a-protocol-driver"></a>プロトコル ドライバーのページ可能で破棄可能なコード





ドライバーの開発者は、可能な限りコードをページング可能として指定する必要があり、メモリ常駐型である必要があるコードのシステム領域が解放されます。 関数は、 [**NDIS\_ページング可能\_関数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557121(v=vs.85))マクロを使用して、ページング可能としてマークできます。 IRQL、リソース管理機能、および関数のその他の特性により、関数がページング不可能になる場合があります。

すべての*Protocolxxx*関数は、パッシブ\_レベルから\_レベルをディスパッチする範囲の IRQL で実行されます。 IRQL = パッシブ\_レベルで排他的に実行される関数は、ページング可能としてマークする必要があります。

IRQL = パッシブ\_レベルで実行されるドライバー関数は、を呼び出さない限り、または、スピンロックを取得する関数など、IRQL &gt;= ディスパッチ\_レベルで実行される関数によって呼び出されない限り、ページング可能にすることができます。 スピンロックを取得すると、獲得しているスレッドの IRQL が\_レベルにディスパッチされます。 IRQL = パッシブ\_レベルで実行されるドライバー関数 ( [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)など) では、そのドライバー関数がページング可能なコードとしてマークされている場合、irql &gt;= ディスパッチ\_レベルで実行される**Ndis * Xxx*** 関数を呼び出すことはできません。 各**ndis * Xxx*** 関数の IRQL の詳細については、「 [ndis Library Functions](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557039(v=vs.85))」を参照してください。

Ndis プロトコルドライバーの[**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数、および**driverentry**からのみ呼び出されるコードは、 [**ndis\_INIT\_function**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557007(v=vs.85))マクロを使用して初期化専用コードとして指定する必要があります。 このマクロで識別されるコードは、システムの初期化時に1回だけ実行されることを前提としています。その結果、この時間内にのみマップされます。 初期化としてマークされた関数は、を返すだけで、破棄されます。

 

 





