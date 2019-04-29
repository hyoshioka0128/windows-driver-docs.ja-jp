---
title: リモート デバイスへの L2CAP クライアント接続の作成
description: リモート デバイスへの L2CAP クライアント接続の作成
ms.assetid: b279db4b-3a4e-407e-ae9b-7330af1905b4
keywords:
- SDP WDK Bluetooth
- サービス探索プロトコルの WDK Bluetooth
- 非同期接続のない WDK Bluetooth
- ACL の WDK Bluetooth
- L2CAP プロファイル ドライバー WDK Bluetooth
- 論理リンク コント ローラーとプロトコルの適応 WDK Bluetooth
- 接続 WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c65b3495e988217221753546a2a76c26b683f99a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328236"
---
# <a name="creating-a-l2cap-client-connection-to-a-remote-device"></a>リモート デバイスへの L2CAP クライアント接続の作成


L2CAP クライアント プロファイル ドライバーは、リモート デバイスへの接続を非同期コネクションレス リンク (ACL) を要求するプロファイルのドライバーです。 デバイスが接続を受け入れる場合、L2CAP クライアント プロファイル ドライバー接続への変更が通知されます。 たとえば、L2CAP クライアント プロファイル ドライバーは、リモート プリンターへの接続を要求できますでき、Bluetooth ドライバー スタックが、プリンターがオフにすると、プロファイルのドライバーに通知できますまたは削除、プリンターが要求を受け入れた後。

L2CAP クライアント プロファイル ドライバー、プロトコル/サービス マルチプレクサー (PSM)、デバイスへの接続を要求するには、デバイスを使用するなど、リモート デバイスに関する情報が必要です。 プロファイルのクライアント ドライバーでは、サービスの探索プロトコル (SDP) Ddi、またはサービスの固定 PSM を通じてこの情報を取得できます。 この情報を取得する方法の詳細については、次を参照してください。 [SDP サービスの情報へのアクセス](accessing-sdp-service-information.md)します。

クライアント プロファイルのドライバーが必要な情報、デバイスの詳細については、リモート デバイスへの接続を L2CAP を開始するには[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_L2CA\_開いている\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536615)要求。

クライアント プロファイルのドライバーが、要求を作成する際へのポインターを提供する[  **\_BRB\_L2CA\_オープン\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536860) で構造体**Parameters.Others.Argument1** IRP のメンバーは、要求に関連付けられています。 この構造体には、リモート デバイスの Bluetooth のアドレスが含まれています、PSM 登録デバイス、および追加の構成パラメーター。

リモート デバイスが開かれているチャネルの要求を受け入れる場合、 **OutResults**と**InResults**のメンバー、 \_BRB\_L2CA\_開く\_チャネル構造体は、新しく作成された接続に関する情報を格納します。 **OutResults**メンバーは、チャネルの送信の半分のパラメーターを指定し、 **InResults**メンバーは、チャネルの受信の半分のパラメーターを指定します。

渡された構成値のいくつか、 \_BRB\_L2CA\_オープン\_など、構造体のチャネル、 **Mtu**メンバー、リモートで接続をネゴシエートするために使用デバイスです。 プロファイルのクライアント ドライバーは、ネゴシエーションの成功したチャネルの可能性を高めをできるだけ全体を範囲として提供する必要があります。 最小メッセージの転送単位を指定する基本的な Bluetooth 最小 MTU サイズより大きい (MTU) サイズのみ行ってくださいどうしても必要な場合。 ネゴシエーションに失敗した場合、接続は失敗します。

**IncomingQueueDepth**のメンバー、 \_BRB\_L2CA\_オープン\_チャネルの構造は、Bluetooth ドライバー スタックを受信してに蓄積する Mtu の最大数を指定します破棄するには Bluetooth ドライバー スタックの前に接続を開始します。 非常に小さい数増加データの可能性をこの値を設定、損失を非常に多数の設定中に増加メモリ要件。 このメンバーを 10 に設定することをお勧めします。

プロファイルのドライバーには、リモート デバイスへの接続を L2CAP 必要なくなる、[をビルドし、送信](building-and-sending-a-brb.md)、 [ **BRB\_L2CA\_閉じる\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff536614)要求。

 

 





