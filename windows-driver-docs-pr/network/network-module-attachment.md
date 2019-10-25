---
title: ネットワーク モジュールのアタッチ
description: ネットワーク モジュールのアタッチ
ms.assetid: 4b3602dd-a9cf-4cb6-bfeb-d2d74d2f391d
keywords:
- ネットワークモジュール WDK ネットワークモジュールレジストラー、添付ファイル
- プロバイダーモジュール WDK ネットワークモジュールレジストラー、添付ファイル
- クライアントモジュール WDK ネットワークモジュールレジストラー、添付ファイル
- ネットワークモジュールの接続
- 登録 (ネットワークモジュールを)
- ネットワークモジュールレジストラー WDK、ネットワークモジュールの接続
- NMR WDK、アタッチ (ネットワークモジュールを)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1d86f2fe4581a80741f48ef1c2b4782d5d3d54d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827210"
---
# <a name="network-module-attachment"></a>ネットワーク モジュールのアタッチ


[クライアントモジュール](client-module.md)と[プロバイダーモジュール](provider-module.md)を相互に接続できるようにするには、それぞれを NMR に登録する必要があります。 クライアントモジュールは、 [**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient)関数を呼び出して NMR に登録します。また、 [**NmrRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider)関数を呼び出して、プロバイダーモジュールが NMR に登録します。 次の図は、ネットワークモジュールの登録を示しています。

![ネットワークモジュールの登録を示す図](images/nmrattach1.png)

クライアントモジュールとプロバイダーモジュールの両方で、NMR に登録するときに同じ[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)が指定されている場合、NMR は2つのネットワークモジュールの接続を開始します。 NMR は、クライアントモジュールの[*Clientattachprovider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数を呼び出すことによって、添付ファイルの処理を開始します。 次の図は、添付ファイルを開始するネットワークモジュールレジストラー (NMR) を示しています。

![添付ファイルを開始するネットワークモジュールレジストラー (nmr) を示す図](images/nmrattach2.png)

クライアントモジュールの[*Clientattachprovider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_attach_provider_fn)コールバック関数は、プロバイダーモジュールの登録データを調べて、プロバイダーモジュールに接続するかどうかを判断できます。 クライアントモジュールによってプロバイダーモジュールにアタッチされると判断された場合、 [**NmrClientAttachProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientattachprovider)関数を呼び出すことによって添付ファイルの処理を続行します。 クライアントモジュールが**NmrClientAttachProvider**関数を呼び出すと、NMR はプロバイダーモジュールの[*providerattachclient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数を呼び出します。 次の図は、クライアントモジュールが添付ファイルを続行するようすを示しています。

![クライアントモジュールが添付ファイルを続行することを示す図](images/nmrattach3.png)

プロバイダーモジュールの[*Providerattachclient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_attach_client_fn)コールバック関数は、クライアントモジュールの登録データを調べて、クライアントモジュールに接続するかどうかを判断できます。 プロバイダーモジュールによってクライアントモジュールにアタッチされることが判断された場合、プロバイダーモジュールとクライアントモジュールはそれぞれの NPI ディスパッチテーブル構造へのポインターを交換します。 クライアントモジュールとプロバイダーモジュールをアタッチした後は、NMR に依存しない NPI 関数を使用して相互に対話できます。 次の図は、接続されているネットワークモジュールを示しています。

![接続されているネットワークモジュールを示す図](images/nmrattach4.png)
