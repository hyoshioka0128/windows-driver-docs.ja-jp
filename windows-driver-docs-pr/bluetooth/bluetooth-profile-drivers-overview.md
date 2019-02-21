---
title: Bluetooth プロファイル ドライバーの概要
description: Bluetooth プロファイル ドライバーの概要
ms.assetid: 86806113-28b6-470c-883c-506ac1205f85
keywords:
- Bluetooth の WDK、Bluetooth について
- WDK の Bluetooth のリモート接続
- WDK の Bluetooth の接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 811734c706f25cedaddd03e929ad398456a83cc6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528732"
---
# <a name="bluetooth-profile-drivers-overview"></a>Bluetooth プロファイル ドライバーの概要


このセクションでは、ワイヤレスの Bluetooth プロトコルの Microsoft が提供するサポートについて説明します。 Bluetooth は、コンピューター、携帯電話、ハンドヘルド デバイス、マウス、キーボード、およびプリンターなどのデバイスのさまざまなワイヤレス接続が可能で業界標準プロトコルです。 このセクションでは、Bluetooth 対応デバイスの Bluetooth プロファイル ドライバーを開発する方法のガイドラインも提供します。 Bluetooth のプロトコルの詳細については 使用可能な[Bluetooth](https://go.microsoft.com/fwlink/p/?linkid=26268) web サイト。

Microsoft では、Microsoft Windows XP Service Pack 2 (SP2) 以降で Bluetooth のプロトコルのサポートを提供します。 プロファイルのドライバーと呼ばれる、Bluetooth ドライバーは、独立系ハードウェア ベンダー (Ihv) Bluetooth 仕様で定義されているさまざまなプロトコルをサポートするで記述されます。 プロファイルのドライバーは、Windows Driver Model (WDM) アーキテクチャに従う必要があります。

Bluetooth のプロトコルをサポートするためには、Microsoft は、いくつかのドライバーとサポート ファイルを含むは指定します。

-   *BthPort.sys*

-   *BthEnum.sys*

-   *BthUsb.sys*

-   *BthProps.cpl*

Ihv は、Windows Vista を使用する必要がありますまたはなどの Windows XP SP2、Windows の以前のバージョンでは、プロファイルのドライバーの開発をサポートしていないために、そのプロファイルのドライバーを開発するには、後でします。

Bluetooth ドライバー スタックは、プロファイル ドライバー Synchronous Connection-Oriented (SCO) へのリンクと論理リンク コント ローラーと適応プロトコル (L2CAP) 間のリンク ローカルのシステムとリモート アクセスを有効にするデバイス ドライバー インターフェイス (Ddi) を提供します。Bluetooth デバイス。

### <a name="span-idscospanspan-idscospansco"></a><span id="sco"></span><span id="SCO"></span>**SCO**

同期接続指向 (SCO) リンクは、2 つの Bluetooth デバイス間のポイント ツー ポイント接続です。 音声のように、期限付きの情報をサポートするには、主に定義されます。

SCO カーネル モード Ddi を提供する、Windows Vista の Bluetooth ドライバー スタックが強化されました。 これらのインターフェイスを使用すると、プロファイルのドライバーは、開く、更新、および、SCO 接続を閉じるだけでなく読み取りを実行および SCO に対して開いている接続経由での書き込み操作を SCO Ddi を使用できます。

SCO の詳細については、次を参照してください。 [SCO リモート デバイスにクライアント接続を作成する](creating-a-sco-client-connection-to-a-remote-device.md)と[、Bluetooth プロファイル ドライバー SCO 接続を受け入れる](accepting-sco-connections-in-a-bluetooth-profile-driver.md)します。

### <a name="span-idl2capandsdpspanspan-idl2capandsdpspanl2cap-and-sdp"></a><span id="l2cap_and_sdp"></span><span id="L2CAP_AND_SDP"></span>**L2CAP と SDP**

L2CAP は非同期コネクションレス リンク (ACL) の Bluetooth のリンクをサポートするために設計されています。 Bluetooth ドライバー スタックは、サービスの接続指向のサポートを提供します。 プロファイル ドライバーでは、Bluetooth の L2CAP Ddi を使用して、開き、更新、および読み取りを実行し、開いている L2CAP 接続経由での書き込み操作に関して L2CAP 接続を閉じます。

サービス探索プロトコル (SDP) は、サービスの提供や、管理対象デバイスによって提供されるサービスを検出するためのプロファイル ドライバーの方法を提供します。

SDP レコードは、複雑なバイト ストリームにアドバタイズされます。 プロファイル ドライバーは、SDP Ddi を使用して、SDP のレコードを検索し、解析をより簡単に解釈される、ツリー ベースの形式に変換します。 プロファイルのドライバーでは、SDP Ddi を使用しても、SDP のレコードのツリー ベースの表現を構築でき、それを提供するストリームに変換することができます。

L2CAP と SDP の詳細については、次を参照してください[L2CAP リモート デバイスにクライアント接続を作成する](creating-a-l2cap-client-connection-to-a-remote-device.md)、 [、Bluetooth プロファイル ドライバー L2CAP 接続を受け入れる](accepting-l2cap-connections-in-a-bluetooth-profile-driver.md)と[との通信。SDP サーバー](communicating-with-sdp-servers.md)します。

Bluetooth ドライバー スタックの詳細については、次を参照してください。 [Bluetooth ドライバー スタック](bluetooth-driver-stack.md)します。

 

 





