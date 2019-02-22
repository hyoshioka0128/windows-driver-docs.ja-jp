---
title: SAN のネイティブ アドレスに変換します。
description: SAN のネイティブ アドレスに変換します。
ms.assetid: 959c66f2-4801-47d5-9e80-f18f17057e23
keywords:
- プロキシ ドライバー WDK San、ネイティブのアドレス変換
- SAN プロキシ ドライバー WDK、ネイティブのアドレス変換
- WDK San、ネイティブのアドレス変換
- ネイティブ アドレス WDK San を翻訳します。
- AF_INET は、WDK San をアドレスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2be766a660589b90be56a962363caf3523fc9952
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536897"
---
# <a name="translating-to-a-san-native-address"></a>SAN のネイティブ アドレスに変換します。





Windows Sockets 切り替える使用では常に、 [WSK アドレス ファミリ](https://msdn.microsoft.com/library/windows/hardware/ff571151)SAN サービス プロバイダーは、SAN のネイティブのアドレス ファミリではないと対話します。 そのため、SAN サービス プロバイダー用のドライバーをプロキシする必要があります間で変換 WSK アドレス ファミリとネイティブのアドレスに応じて。

プロキシ ドライバー」の説明に従って、その管理下にある各 NIC に割り当てられた IP アドレスの一覧を維持するために TDI プラグ アンド プレイ (PnP) 通知を使用して[SAN NIC の通知を登録する](registering-for-san-nic-notifications.md)します。 プロキシ ドライバーでは、この一覧を使用して、ネイティブの SAN アドレスと IP アドレスの間で変換します。

プロキシ ドライバーは、IP アドレスを含む SAN サービス プロバイダーからの要求を受信します。 これらの要求などが、特定の NIC にバインドする要求およびリモート ピアに接続する要求。 プロキシ ドライバーは、これらの要求を完了するネイティブの SAN アドレスに変換する必要があります。 プロキシ ドライバーは、それらのリモート ピアの SAN のネイティブ アドレスが含まれているリモート ピアからも受信接続要求を受信します。 プロキシ ドライバーは、これらの要求を完了するリモート ピアの IP アドレスに変換する必要があります。

**注**  Windows Vista の後に、TDI が Microsoft Windows のバージョンでサポートされません。 使用[Windows フィルタ リング プラットフォーム](https://msdn.microsoft.com/library/windows/hardware/ff571067)または[Winsock Kernel](https://msdn.microsoft.com/library/windows/hardware/ff571083)代わりにします。

 

 

 





