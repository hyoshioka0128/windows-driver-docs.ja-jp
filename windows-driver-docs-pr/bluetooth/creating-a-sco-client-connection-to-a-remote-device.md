---
title: リモート デバイスに SCO クライアント接続を作成します。
description: リモート デバイスに SCO クライアント接続を作成します。
ms.assetid: e5a4ed14-1fb0-4a5f-b388-5e536d674c23
keywords:
- 同期接続指向の WDK Bluetooth
- SCO プロファイル ドライバー WDK Bluetooth
- SCO 接続の開始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19bcc017d23799c5c4af684d476dad10b91c4984
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528743"
---
# <a name="creating-a-sco-client-connection-to-a-remote-device"></a>リモート デバイスに SCO クライアント接続を作成します。


SCO クライアント プロファイル ドライバーは、リモート デバイスへの接続を Synchronous Connection-Oriented (SCO) を要求するプロファイルのドライバーです。 デバイスが接続を受け入れる場合、SCO クライアント プロファイル ドライバー接続への変更が通知されます。 など SCO クライアント プロファイル ドライバーは、リモート ヘッドセットへの接続を要求でき、ヘッドセットには、接続要求が承諾、Bluetooth ドライバー スタックはヘッドセットはオフにすると、プロファイルのドライバーに通知できますまたは削除します。

SCO 接続は 2 つの Bluetooth デバイス間のポイント ツー ポイント接続であるために、SCO クライアント プロファイル ドライバーに接続するリモート デバイスの Bluetooth アドレスのみが必要があります。

リモート デバイスへの接続を SCO を開始するプロファイルのドライバーがする必要があります[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_SCO\_オープン\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536626)要求。

リモート デバイスが、プロファイルのドライバーの SCO 接続要求を受け入れる場合、プロファイルのドライバー、コマンドを実行できます追加 BRB 新しく接続されたチャネル経由で IOCTL を使用して\_内部\_両方\_送信\_BRB など。

-   [**BRB\_SCO\_取得\_チャネル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff536624)

-   [**BRB\_SCO\_取得\_システム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff536625)

-   [**BRB\_SCO\_転送**](https://msdn.microsoft.com/library/windows/hardware/ff536629)

**注**  プロファイル ドライバーにする必要があります[をビルドし、送信](building-and-sending-a-brb.md)、 **BRB\_SCO\_取得\_システム\_情報**中に要求そのため、どのようなグローバル SCO 設定は場合と、基になるハードウェア SCO をサポートしている場合を判断する初期化します。

 

プロファイルのドライバーには、リモート デバイスへの接続を SCO 必要なくなる、[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_SCO\_閉じる\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536622)要求。

 

 





