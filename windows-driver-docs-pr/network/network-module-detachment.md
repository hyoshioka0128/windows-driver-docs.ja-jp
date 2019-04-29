---
title: ネットワーク モジュールのデタッチ
description: ネットワーク モジュールのデタッチ
ms.assetid: f41ac030-0bfc-47e2-9840-2c3550bc7d33
keywords:
- ネットワーク モジュール WDK ネットワーク モジュールの登録、デタッチできません。
- プロバイダー モジュール WDK ネットワーク モジュールの登録、デタッチできません。
- ネットワーク モジュールのデタッチ
- クライアント モジュール WDK ネットワーク モジュールの登録、デタッチできません。
- ネットワーク モジュールの登録を解除
- ネットワーク モジュールをデタッチするネットワーク モジュールのレジストラー WDK
- ネットワーク モジュールのデタッチ、NMR WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a677d9076f871cbeb69760f0d0bf8aba4793e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331885"
---
# <a name="network-module-detachment"></a>ネットワーク モジュールのデタッチ


ネットワーク モジュールの接続のペアは、クライアント モジュールまたはプロバイダー モジュールとネットワーク モジュール レジストラー (NMR) の登録を解除するときに、互いからデタッチされます。 呼び出すことによって、NMR でクライアント モジュールの登録を解除、 [ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)関数およびプロバイダー モジュールの登録を解除、NMR で呼び出すことによって、 [ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)関数。 次の図は、登録解除のモジュールを開始するネットワークを示しています。

![登録解除の開始ネットワーク モジュールを示す図](images/nmrdetach1.png)

ネットワーク モジュールのいずれかが、NMR で登録を解除、NMR 呼び出し両方クライアント モジュールの[ *ClientDetachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544908)コールバック関数とプロバイダー、モジュールの[ *ProviderDetachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570397)ネットワーク モジュールのデタッチを開始するコールバック関数。 次の図は、デタッチを開始する NMR を示しています。

![デタッチを開始する nmr を示す図](images/nmrdetach2.png)

呼び出すクライアント モジュールは、すぐに、プロバイダー モジュールから自身のデタッチにできない場合、 [ **NmrClientDetachProviderComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568772)関数自体、プロバイダーからのデタッチが完了した後モジュール。 同様の場合、プロバイダー モジュールからデタッチできません自体クライアント モジュールすぐに、呼び出し、 [ **NmrProviderDetachClientComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568781)関数自体からのデタッチが完了した後、クライアントのモジュール。 次の図は、完了のデタッチをネットワーク モジュールを示します。

![ネットワーク モジュールのデタッチの完了を示す図](images/nmrdetach3.png)


クライアント モジュールとプロバイダー、モジュールの両方には、互いからのデタッチが完了したら、NMR 呼び出してクライアント モジュールの[ *ClientCleanupBindingContext* ](https://msdn.microsoft.com/library/windows/hardware/ff544904)コールバック関数およびプロバイダーモジュールの[ *ProviderCleanupBindingContext* ](https://msdn.microsoft.com/library/windows/hardware/ff570396)コールバック関数のネットワーク モジュールは、添付ファイルの場合は、そのそれぞれバインド コンテキストをクリーンアップできるようにします。 次の図は、NMR 発信側のクリーンアップを示します。

![nmr 発信側のクリーンアップを示す図](images/nmrdetach4.png)


クライアント モジュールがすべてを以前にアタッチされてし、プロバイダー モジュールのすべてのプロバイダー モジュールからデタッチされて完全にまでには、クライアントのモジュールの登録解除は完了しませんクライアント モジュールが、NMR で登録を解除する場合完全にクライアント モジュールからデタッチします。 クライアント モジュールは登録解除を呼び出すことによって完了の待機、 [ **NmrWaitForClientDeregisterComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568786)関数。 同様に、プロバイダー モジュールは、NMR で登録解除、プロバイダー モジュールの登録解除は完了しませんプロバイダー モジュールに以前にアタッチされているクライアント モジュールのすべてとすべてのこれらのクライアント モジュールからデタッチされて完全にまでプロバイダー モジュールから完全に切り離されます。 プロバイダー モジュールが登録解除を呼び出すことによって完了の待機、 [ **NmrWaitForProviderDeregisterComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568787)関数。 次の図は、ネットワークを完了するを待機しているモジュールの登録解除します。

![登録解除を完了するを待機しているネットワーク モジュールを示す図](images/nmrdetach5.png)
