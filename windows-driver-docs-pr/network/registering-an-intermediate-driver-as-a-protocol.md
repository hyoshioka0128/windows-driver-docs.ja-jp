---
title: 中間ドライバーをプロトコルとして登録する
description: 中間ドライバーをプロトコルとして登録する
ms.assetid: 79707f6b-0e31-46a8-a763-fa2669ce9635
keywords:
- 中間ドライバーの登録
- 中間ドライバー WDK ネットワーク、登録
- NDIS 中間ドライバー WDK、登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 991abf74ad9edc31d0e8c04317ba4a7066fbd0de
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842092"
---
# <a name="registering-an-intermediate-driver-as-a-protocol"></a>中間ドライバーをプロトコルとして登録する





中間ドライバーは、 [**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)を呼び出すことによって、 [**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数のコンテキストで*protocolxxx*関数を NDIS に登録します。

中間ドライバーをプロトコルとして登録することは、プロトコルドライバーとして登録することとほぼ同じです。 詳細については、「[プロトコルドライバーの初期化](initializing-a-protocol-driver.md)」を参照してください。

接続指向のエッジを持つ中間ドライバーは、接続指向のクライアントとして登録する必要があります。 接続指向クライアントは、コールマネージャーまたは統合されたミニポート呼び出しマネージャー (MCM) の呼び出しセットアップおよび破棄サービスを使用します。 また、接続指向クライアントは、接続指向ミニポートドライバーまたは MCM の送受信機能を使用してデータを送受信します。 詳細については、「[クライアントによって実行される接続指向の操作](connection-oriented-operations-performed-by-clients.md)」を参照してください。

中間ドライバーでは、実装固有の他の*Protocolxxx*関数が必要になる場合があります。 オプションの*Protocolxxx*関数の登録の詳細については、「[オプションのプロトコルドライバーサービスの構成](configuring-optional-protocol-driver-services.md)」を参照してください。

 

 





