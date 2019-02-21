---
title: ロックおよびロック解除のベスト プラクティス
description: ロックおよびロック解除のベスト プラクティス
ms.assetid: cfa45c0d-4e92-4455-a8f6-17d4806f9c36
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7aad91eb5a9cadcc2b7727e6b9c97322d30d71b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537467"
---
# <a name="locking-and-unlocking-best-practices"></a>ロックおよびロック解除のベスト プラクティス





WIA ドライバーの STI 部分のロックには、特に注意する必要があります。 場合でも、アプリケーションは STI インターフェイスを公開に直接アクセスできる、関数の誤用がデバイスへのアクセスなどを指示します。 正しく実装されている手法をロックできます開いたままにデバイスを拒否 (dos) 攻撃にします。

### <a name="for-sti-applications"></a>STI アプリケーション

次の一覧には、予防措置と STI アプリケーションを使用する際に従う必要のガイドラインが含まれています。

-   長時間にわたってロックを保持できません。

-   デバイスへの直接アクセスが不要である場合は、WIA インターフェイスのメソッドを使用して、同じ情報を取得することができる場合があります。 これは、WIA サービス コントロールをロックでは、ためことをお勧めします。

-   STI 使用 TWAIN ドライバー、 [ **IStiUSD::LockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543829)デバイスへのアクセスを制御するメソッド。 TWAIN ドライバー STI を使用する場合は、ロック時間を制御するため、TWAIN ドライバーが担当します。

-   のみを実装するために作成することができます、 **IStiUSD**インターフェイスのメソッド。 このアプローチの欠点は、アプリケーションを呼び出すことができます**IStiUSD::LockDevice**のため、直接アプリケーションで排他的に使用のデバイスをロックします。 Windows ハードウェア品質のラボが; この手法を使用するドライバーを認定できません。このようなドライバーは署名されていないドライバーとしてのみインストールできます。

### <a name="for-wia-drivers"></a>WIA ドライバー

次の一覧には、注意事項とガイドラインが WIA ドライバーを使用する場合に従う必要がありますが含まれています。

-   長いロック期間中に、デバイスのアクティビティを監視します。 アクティビティがない場合は、ドライバーする必要があります、デバイスのロックを解除し、その他のクライアントが接続できるようにします。 ドライバーがロックを解除、デバイスなど非常に大きいイメージの場合は、スキャンが進行している場合、またはイメージを取得するに通常より時間がかかる場合。 これは、現在のセッションを中断します。 によって、デバイス上で動作するバス、非常に大きなイメージを任意の場所から 10 メガバイト 1 ギガバイト以上にあり、長期間でした任意の場所 500 ミリ秒から 1 分以上に。 デバイスとは、デバイスのこれら特定の値を認識できるように上で動作するバスのベンチマークを実行する必要があります。

-   WIA を使用するアプリケーション、ドライバーのロックのメソッドにアクセスしない[ **IWiaMiniDrv::drvLockWiaDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff544995)と[ **IWiaMiniDrv::drvUnLockWiaDevice**](https://msdn.microsoft.com/library/windows/hardware/ff545012). WIA サービスがロックの呼び出しを伝達するだけで、WIA サービス ロック メソッドを呼び出す、 **IStiUSD**を使用して、 **IStiUSD::LockDevice**メソッド。

-   アプリケーションが排他的、WIA を使用してデバイスをロックしている場合、 **IStiUSD::LockDevice**メソッド、WIA サービス デバイスにアクセスできませんそのアプリケーションを呼び出すまで、 [ **IStiUSD::UnLockDevice**](https://msdn.microsoft.com/library/windows/hardware/ff543843)メソッド。 WIA サービスがデバイスをロックできない場合、デバイスはすべてのアプリケーションや、WIA サービスに依存するドライバーを使用できません。

-   [ **IWiaMiniDrv::drvLockWiaDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff544995)メソッドは常に呼び出す必要があります、 [ **IStiDevice::LockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543756)メソッド、および、 [ **IWiaMiniDrv::drvUnLockWiaDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff545012)メソッドは常に呼び出す必要があります、 [ **IStiDevice::UnLockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543770)メソッド。 これにより、WIA サービスが適切なロックの管理、デバイスに対して実行します。 **IStiDevice**インターフェイスがドライバーへの呼び出しに渡される、 [ **IWiaMiniDrv::drvInitializeWia** ](https://msdn.microsoft.com/library/windows/hardware/ff544986)メソッド。 このインターフェイスは、キャッシュを呼び出すために使用する必要があります、 **IStiDevice::LockDevice**メソッド。 このメソッドは、ドライバーの**IStiUSD::LockDevice**メソッド。

-   ロックを制御するブール値を使用する場合は、複数のスレッドからこの値を保護します。 2 つのドライバーが同時に 1 つのデバイスをロックしようとすると、1 つだけのドライバーが成功します。

 

 




