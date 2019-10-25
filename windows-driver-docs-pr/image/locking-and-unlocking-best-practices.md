---
title: ロックおよびロック解除のベスト プラクティス
description: ロックおよびロック解除のベスト プラクティス
ms.assetid: cfa45c0d-4e92-4455-a8f6-17d4806f9c36
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 01853b5ffdb3005670e1f88f5c93d7884adf13d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840790"
---
# <a name="locking-and-unlocking-best-practices"></a>ロックおよびロック解除のベスト プラクティス





WIA ドライバーの STI 部分のロックには、特に注意が必要です。 アプリケーションが公開された STI インターフェイスに直接アクセスできる場合でも、デバイスへの直接アクセスは誤用される可能性があります。 正しく実装されていないロック手法を使用すると、デバイスをサービス拒否 (DoS) 攻撃に対して開いたままにすることができます。

### <a name="for-sti-applications"></a>STI アプリケーションの場合

次の一覧には、STI アプリケーションを使用する際に従う必要がある予防策とガイドラインが記載されています。

-   長時間にわたってロックを保持しない。

-   デバイスに直接アクセスする必要がない場合は、WIA インターフェイスメソッドを使用して同じ情報を取得できる可能性があります。 これは、WIA サービスによってロックが制御されるため、お勧めします。

-   STI を使用する TWAIN ドライバーは、 [**Ib usd:: lockdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice)メソッドを使用してデバイスへのアクセスを制御します。 TWAIN ドライバーで STI を使用する場合、TWAIN ドライバーはロック時間を制御します。

-   これを作成して、 **iと usd**のインターフェイスメソッドのみを実装することができます。 この方法の欠点は、アプリケーションが**iexclusive usd:: LockDevice**を直接呼び出して、アプリケーションが排他的に使用できるようにデバイスをロックできることです。 Windows Hardware Quality Lab は、この手法を使用するドライバーを認定していません。このようなドライバーは、署名されていないドライバーとしてのみインストールできます。

### <a name="for-wia-drivers"></a>WIA ドライバーの場合

次の一覧には、WIA ドライバーを使用する際に従う必要がある予防策とガイドラインが記載されています。

-   長時間ロック期間中にデバイスのアクティビティを監視します。 アクティビティがない場合は、ドライバーによってデバイスのロックが解除され、他のクライアントが接続できるようになります。 ドライバーはデバイスのロックを解除しないでください。たとえば、非常に大きなイメージをスキャンする場合や、イメージを取得するのに非常に長い時間がかかっている場合などです。 これにより、現在のセッションが中断されます。 デバイスとそれが動作するバスによっては、非常に大きなイメージは 10 mb からギガバイトまでの範囲で、長時間にわたって500ミリ秒から1分以上かかることがあります。 デバイスとそれが動作するバスをベンチマークし、デバイスに対してこれらの特定の値がどのようなものであるかを把握しておく必要があります。

-   WIA を使用するアプリケーションは、ドライバーのロック方法である[**IWiaMiniDrv::D rvlockwiadevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)と[**IWiaMiniDrv::d rvunlockwiadevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)にはアクセスしません。 これらのロックメソッドを呼び出すのは、WIA サービスのみです。この場合、WIA サービスは**ib usd:: LockDevice**メソッドを使用して、ロックされた呼び出しを**ib ドル**に伝達します。

-   アプリケーションが**Ib usd:: LockDevice**メソッドを使用して wia デバイスを排他的にロックする場合、そのアプリケーションが[**ib Usd:: UnLockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice)メソッドを呼び出すまで、wia サービスはデバイスにアクセスできません。 WIA サービスがデバイスをロックできない場合、そのデバイスは、WIA サービスに依存しているアプリケーションやドライバーでは使用できません。

-   [**IWiaMiniDrv::D rvlockwiadevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvlockwiadevice)メソッドは常に[**i Device:: lockdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-lockdevice)メソッドを呼び出す必要があります。 [**IWiaMiniDrv::d Rvunlockwiadevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvunlockwiadevice)メソッドは常に[**i device:: UnLockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unlockdevice)メソッドを呼び出す必要があります。 これにより、WIA サービスがデバイスの適切なロック管理を実行できるようになります。 [**IIWiaMiniDrv::D rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)メソッドの呼び出しで、 **iのデバイス**インターフェイスがドライバーに渡されます。 このインターフェイスはキャッシュし、 **ib device:: lockdevice**メソッドを呼び出すために使用する必要があります。 このメソッドは、ドライバーの**ib usd:: LockDevice**メソッドを呼び出します。

-   ブール値を使用してロックを制御する場合は、複数のスレッドからこの値を保護します。 2つのドライバーが同時に1つのデバイスをロックしようとすると、1つのドライバーだけが成功します。

 

 




