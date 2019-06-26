---
title: ネットワーク モジュールのアタッチ
description: ネットワーク モジュールのアタッチ
ms.assetid: 4b3602dd-a9cf-4cb6-bfeb-d2d74d2f391d
keywords:
- ネットワーク モジュール WDK ネットワーク モジュールの登録、添付ファイル
- プロバイダー モジュール WDK ネットワーク モジュールの登録、添付ファイル
- クライアント モジュール WDK ネットワーク モジュールの登録、添付ファイル
- ネットワーク モジュールのアタッチ
- ネットワーク モジュールの登録
- ネットワーク モジュール レジストラー WDK は、ネットワーク モジュールのアタッチ
- ネットワーク モジュールのアタッチ、NMR WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a65ef5bba34bc3712b6e3c42834831778a1e049
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386329"
---
# <a name="network-module-attachment"></a>ネットワーク モジュールのアタッチ


前に、[クライアント モジュール](client-module.md)と[プロバイダー モジュール](provider-module.md)関連付けることができます、互いに各登録が必要な自体、NMR とします。 クライアント モジュールを呼び出すことによって、NMR で登録、 [ **NmrRegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterclient)関数とプロバイダーを呼び出すことによって、NMR モジュールに登録、 [ **NmrRegisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrregisterprovider)関数。 次の図は、ネットワーク モジュールの登録を示します。

![ネットワーク モジュールの登録を示す図](images/nmrattach1.png)

クライアントのモジュールとプロバイダー、モジュールの両方は指定と同じでかどうか[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md) NMR が 2 つのネットワーク モジュールをまとめて接続を開始、NMR に登録するとき。 NMR クライアントのモジュールを呼び出すことによってアタッチ プロセスを開始します[ *ClientAttachProvider* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数。 次の図は、ネットワーク モジュール レジストラー (NMR)、添付ファイルの開始を示します。

![添付ファイルを開始するネットワーク モジュール レジストラー (nmr) を示す図](images/nmrattach2.png)

クライアント モジュールの[ *ClientAttachProvider* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数は、確認のかどうかは、プロバイダー モジュールに接続するプロバイダー モジュールの登録データを調べることができます。 呼び出して添付ファイルのプロセスを続行クライアント モジュール プロバイダー モジュールに接続すると判断した場合、 [ **NmrClientAttachProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrclientattachprovider)関数。 クライアント モジュールを呼び出すと、 **NmrClientAttachProvider**関数、NMR はさらに、プロバイダー モジュールの呼び出し[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数。 次の図は、添付ファイルを引き続きクライアント モジュールを示します。

![添付ファイルを引き続きクライアント モジュールを示す図](images/nmrattach3.png)

プロバイダー モジュールの[ *ProviderAttachClient* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数は、確認のかどうかは、クライアント モジュールに接続するクライアント モジュールの登録データを調べることができます。 プロバイダー モジュールがクライアント モジュールに接続すると判断した場合、プロバイダー モジュールとクライアント モジュールは、そのそれぞれ NPI ディスパッチ テーブル構造へのポインターを交換します。 クライアントのモジュールとプロバイダー モジュールをアタッチした後は、NMR の独立した、NPI 関数を使用して相互作用できます。 次の図は、接続されているネットワーク モジュールを示します。

![接続されているネットワーク モジュールを示す図](images/nmrattach4.png)
