---
title: リモート デバイスへの L2CAP クライアント接続の作成
description: リモート デバイスへの L2CAP クライアント接続の作成
ms.assetid: b279db4b-3a4e-407e-ae9b-7330af1905b4
keywords:
- SDP WDK Bluetooth
- サービス検出プロトコル WDK Bluetooth
- 非同期接続-WDK 以外の Bluetooth
- ACL WDK Bluetooth
- L2CAP プロファイルドライバー WDK Bluetooth
- 論理リンクコントローラーとアダプテーションプロトコル WDK Bluetooth
- 接続 WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6982c879c0f31d002c913c6c9dffaef5f361ecfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833859"
---
# <a name="creating-a-l2cap-client-connection-to-a-remote-device"></a>リモート デバイスへの L2CAP クライアント接続の作成


L2CAP client profile driver は、リモートデバイスへの非同期コネクションレスリンク (ACL) 接続を要求するプロファイルドライバーです。 デバイスが接続を受け入れると、L2CAP client profile ドライバーに接続の変更が通知されます。 たとえば、L2CAP client プロファイルドライバーは、リモートプリンターへの接続を要求できます。プリンターが要求を受け入れると、Bluetooth ドライバースタックは、プリンターの電源がオフになっているか削除されたときに、プロファイルドライバーに通知することができます。

L2CAP client profile driver には、デバイスへの接続を要求するために、デバイスが使用するプロトコル/サービスマルチプレクサー (PSM) などのリモートデバイスに関する情報が含まれている必要があります。 クライアントプロファイルドライバーは、サービス検出プロトコル (SDP) DDIs、またはサービスの固定 PSM を介してこの情報を取得できます。 この情報を取得する方法の詳細については、「 [SDP サービス情報へのアクセス](accessing-sdp-service-information.md)」を参照してください。

リモートデバイスへの L2CAP 接続を開始するには、クライアントプロファイルドライバーにデバイスに関する必要な情報が含まれていると、 [**L2CA\_\_** ](https://docs.microsoft.com/previous-versions/ff536615(v=vs.85))を[作成して送信し](building-and-sending-a-brb.md)\_チャネル要求を開く必要があります。

クライアントプロファイルドライバーは、要求をビルドするときに、 [ **\_BRB\_L2CA\_OPEN\_CHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)構造体を、要求に関連付けられている IRP の**引数 1**メンバーに渡します。 この構造体には、リモートデバイスの Bluetooth アドレス、デバイスに登録されている PSM、および追加の構成パラメーターが含まれています。

リモートデバイスが open channel 要求を受け入れると、\_BRB\_L2CA\_開いている\_チャネル構造の**outresults**と**inresults**のメンバーに、新しく作成された接続に関する情報が含まれます。 **Outresults**メンバーはチャネルの送信半分のパラメーターを指定し、 **inresults**メンバーはチャネルの受信半分のパラメーターを指定します。

\_BRB\_L2CA\_OPEN\_CHANNEL 構造体 ( **Mtu**メンバーなど) で渡される構成値のいくつかを使用して、リモートデバイスとの接続をネゴシエートします。 クライアントプロファイルドライバーは、チャネルネゴシエーションが成功する可能性を高めるために、可能な限り広い範囲を提供する必要があります。 基本的な Bluetooth の最小 MTU サイズより大きい最小メッセージ転送単位 (MTU) サイズを指定する必要があるのは、絶対に必要な場合のみです。 ネゴシエーションが失敗した場合、接続は失敗します。

\_BRB\_L2CA\_OPEN\_CHANNEL structure の**IncomingQueueDepth**メンバーは、bluetooth ドライバースタックが受信し、bluetooth ドライバースタックの前に接続でキューに入れられる mtu の最大数を指定します。破棄を開始します。 この値を非常に小さい数に設定すると、データ損失の可能性が高くなります。非常に大きな数値に設定すると、メモリ要件が増加します。 Microsoft では、このメンバーを10に設定することをお勧めします。

プロファイルドライバーは、リモートデバイスへの L2CAP 接続を必要としなくなったときに、 [**Brb\_L2CA\_終了\_チャネル**](https://docs.microsoft.com/previous-versions/ff536614(v=vs.85))要求を[作成して送信](building-and-sending-a-brb.md)する必要があります。

 

 





