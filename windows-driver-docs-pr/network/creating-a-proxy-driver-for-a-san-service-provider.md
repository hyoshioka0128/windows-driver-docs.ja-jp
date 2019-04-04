---
title: SAN サービス プロバイダーのプロキシ ドライバーを作成します。
description: SAN サービス プロバイダーのプロキシ ドライバーを作成します。
ms.assetid: 350c21a3-98e3-48a2-8403-68de97314933
keywords:
- Windows ソケットは、WDK をプロキシ ドライバーを直接します。
- プロキシ ドライバー WDK San
- SAN プロキシ ドライバー WDK
- プロキシ ドライバー WDK San、SAN プロキシ ドライバーについて
- SAN プロキシ ドライバーに関するプロキシ ドライバー WDK、SAN
- SAN サービス プロバイダー、WDK プロキシ ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cfabd7a3321436740cab7fe58a95e2bd7323e71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559369"
---
# <a name="creating-a-proxy-driver-for-a-san-service-provider"></a>SAN サービス プロバイダーのプロキシ ドライバーを作成します。





SAN サービス プロバイダーのプロキシ ドライバーは、Windows Sockets スイッチに必要なタスクを実行するカーネル モード ドライバーと SAN サービス プロバイダー。 このようなタスクには、メモリの管理とのネットワーク インターフェイス コント ローラー (Nic)、プロキシ ドライバーの制御下にある IP アドレスの決定が含まれます。 プロキシ ドライバーは、Windows Driver Model (WDM) ドライバーを使用する必要はありません。 つまり、プラグ アンド プレイまたは電源の管理をサポートする必要はありません。 カーネル モード ドライバーの開発に関する詳細については、[カーネル モード ドライバー コンポーネント](https://msdn.microsoft.com/library/windows/hardware/ff553213)を参照してください。

さまざまなベンダーでは、さまざまな基になるテクノロジを使用して、SAN ネットワーク インターフェイス コント ローラー (Nic) を実装する場合があります、ため Windows Sockets ダイレクトで指定されていない SAN サービス プロバイダーとそのプロキシ ドライバー間や、プロキシ インターフェイスドライバーと SAN を転送します。

SAN の NIC ベンダーでは、その基になるテクノロジに適したトランスポート インターフェイスを実装する必要があります。 仕入先は、SAN の NIC、またはその両方のカーネル モード ドライバーで、SAN NIC で、このインターフェイスを実装できます。 SAN サービス プロバイダーは、このインターフェイスをユーザー モード プロセスのアドレス空間に直接マップします。 仕入先は、このインターフェイスの間で渡されるすべてのバッファーをロック ダウンされているし、SAN の NIC に登録されていることを確認する必要があります。

次のセクションでは、SAN サービス プロバイダーの DLL のプロキシ ドライバーを作成する方法について説明します。

[初期化と SAN プロキシ ドライバーをアンロード](initializing-and-unloading-a-san-proxy-driver.md)

[割り当てと SAN プロキシ ドライバーのメモリを解放](allocating-and-releasing-memory-for-a-san-proxy-driver.md)

[セキュリティで保護して、仮想アドレスの所有権を解放します。](securing-and-releasing-ownership-of-virtual-addresses.md)

[SAN の NIC の通知を登録します。](registering-for-san-nic-notifications.md)

[SAN のネイティブ アドレスに変換します。](translating-to-a-san-native-address.md)

[SAN サービス プロバイダーの Ioctl を実装します。](implementing-ioctls-for-a-san-service-provider.md)

 

 





