---
title: スマート カードのドライバーの環境
description: スマート カードのドライバーの環境
ms.assetid: f1b369c6-84a0-4a0a-9e70-40dd3009c59e
keywords:
- スマート カードのドライバー WDK、環境
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92cc9c9d2fe9b901576b86705ece238aed27c7f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528563"
---
# <a name="smart-card-driver-environment"></a>スマート カードのドライバーの環境


## <span id="_ntovr_smart_card_driver_environment"></span><span id="_NTOVR_SMART_CARD_DRIVER_ENVIRONMENT"></span>


次の図は、スマート カード リーダーのドライバーの標準的な環境を示しています。

![スマート カード リーダーのドライバーの標準的な環境を示す図](images/memp1.png)

さらに、図では、スマート カード環境の次のコンポーネントを示します。

-   アプリケーションは、スマート カード リソース マネージャーを使用して、スマート カード リーダーのドライバーと通信します。 リーダーのドライバーは、カーネルの領域に存在し、ユーザー領域で、スマート カード リソース マネージャーが存在します。

-   リソース マネージャーを使用してディスパッチは I/O コントロールを使用して、リーダーのドライバーと通信して、 [DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=94613)システム呼び出し。 使用する方法については、 [DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=94613)システム呼び出しを参照してください、 [DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=94613) Microsoft Windows SDK のトピックです。

    スマート カード対応のアプリケーションがのスマート カード リーダーのドライバーに指示を送信する同様に、 [DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=94613)、オペレーティング システムは、リーダーのドライバーに示された IOCTL を転送するとします。 リーダーのドライバーが WDM ドライバーの場合は、オペレーティング システムは I/O 要求パケット (IRP) を使用して、要求を転送します。

-   Microsoft 提供の 1 つのリーダー ドライバー サンプル*pscr.sys*PCMCIA のスマート カード リーダーのドライバーであります。 このドライバーのソース コードは、WDK サンプルのコレクションで使用できます。 詳細については、次を参照してください。 [PCMCIA のスマート カード ドライバー](https://github.com/Microsoft/Windows-driver-samples/tree/master/smartcrd)します。 スマート カード リーダー デバイスのベンダーは、システム提供のリソース マネージャーとスマート カードのドライバーのライブラリを使用するように設計されたドライバーを提供する必要があります。

-   両方のネイティブおよびベンダーから提供されたリーダーのドライバーは、セクションで説明したようの重要な操作の多くを実行するスマート カードのドライバー ライブラリを使用する必要があります[スマート カードのドライバー ライブラリ](smart-card-driver-library.md)します。

 

 





