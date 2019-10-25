---
title: ネットワーク モジュールのデタッチ
description: ネットワーク モジュールのデタッチ
ms.assetid: f41ac030-0bfc-47e2-9840-2c3550bc7d33
keywords:
- ネットワークモジュール WDK ネットワークモジュールレジストラー、デタッチ
- プロバイダーモジュール WDK ネットワークモジュールレジストラー、デタッチ
- ネットワークモジュールの切断
- クライアントモジュール WDK ネットワークモジュールレジストラー、デタッチ
- ネットワークモジュールの登録解除
- ネットワークモジュールレジストラー WDK、ネットワークモジュールのデタッチ
- NMR WDK、デタッチ (ネットワークモジュールを)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8acf93c3b32757f40ba1ca062a56382bc1bb4566
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827160"
---
# <a name="network-module-detachment"></a>ネットワーク モジュールのデタッチ


接続されているネットワークモジュールのペアは、クライアントモジュールまたはプロバイダーモジュールがネットワークモジュールレジストラー (NMR) と解除したときに相互に切り離されます。 クライアントモジュールは、 [**NMR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider)関数を呼び出して[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)関数とプロバイダーモジュール解除を呼び出して、NMR を解除します。 次の図は、登録解除を開始するネットワークモジュールを示しています。

![登録解除を開始するネットワークモジュールを示す図](images/nmrdetach1.png)

どちらかのネットワークモジュールが NMR と解除すると、NMR はクライアントモジュールの[*ClientDetachProvider*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_detach_provider_fn) callback 関数とプロバイダーモジュールの[*ProviderDetachClient*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_detach_client_fn) callback 関数の両方を呼び出して、ネットワークモジュールのデタッチを開始します。 次の図は、デタッチを開始する NMR を示しています。

![デタッチを開始する nmr を示す図](images/nmrdetach2.png)

クライアントモジュールがプロバイダーモジュールから自身を直ちにデタッチできない場合は、プロバイダーモジュールからのデタッチが完了した後で、 [**NmrClientDetachProviderComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrclientdetachprovidercomplete)関数を呼び出します。 同様に、プロバイダーモジュールがクライアントモジュールから自身を直ちにデタッチできない場合、クライアントモジュールからのデタッチが完了した後に、 [**NmrProviderDetachClientComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrproviderdetachclientcomplete)関数が呼び出されます。 次の図は、デタッチを完了するネットワークモジュールを示しています。

![デタッチを完了するネットワークモジュールを示す図](images/nmrdetach3.png)


クライアントモジュールとプロバイダーモジュールの両方が相互にデタッチを完了した後、NMR は、クライアントモジュールの[*ClientCleanupBindingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_client_cleanup_binding_context_fn)コールバック関数とプロバイダーモジュールの[*ProviderCleanupBindingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nc-netioddk-npi_provider_cleanup_binding_context_fn)を呼び出します。ネットワークモジュールが添付ファイルの各バインドコンテキストをクリーンアップできるように、コールバック関数。 次の図は、NMR のクリーンアップを示しています。

![nmr のクリーンアップを示す図](images/nmrdetach4.png)


クライアントモジュールが NMR で登録解除されている場合、クライアントモジュールが以前にアタッチされていたすべてのプロバイダーモジュールから完全にデタッチされるまで、クライアントモジュールの登録解除は完了しません。また、すべてのプロバイダーモジュールには、クライアントモジュールから完全にデタッチされます。 クライアントモジュールは、 [**NmrWaitForClientDeregisterComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrwaitforclientderegistercomplete)関数を呼び出すことによって、登録解除が完了するまで待機します。 同様に、プロバイダーモジュールが NMR で登録解除された場合、プロバイダーモジュールの登録解除は、以前にアタッチされていたすべてのクライアントモジュールからプロバイダーモジュールが完全にデタッチされるまで完了しません。プロバイダーモジュールから完全にデタッチされている。 プロバイダーモジュールは、 [**NmrWaitForProviderDeregisterComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrwaitforproviderderegistercomplete)関数を呼び出すことによって、登録解除が完了するまで待機します。 次の図は、登録解除の完了を待機しているネットワークモジュールを示しています。

![登録解除の完了を待機しているネットワークモジュールを示す図](images/nmrdetach5.png)
