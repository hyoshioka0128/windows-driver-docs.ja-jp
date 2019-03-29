---
title: MB ミニポート ドライバー IP アドレス通知のガイドライン
description: MB ミニポート ドライバー IP アドレス通知のガイドライン
ms.assetid: 23d74bc4-5648-45e3-a603-350d71bb16e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbf70c2ecb3338ee39a93b905e4c52a1f8975cd1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570799"
---
# <a name="guidelines-for-mb-miniport-driver-ip-address-notifications"></a>MB ミニポート ドライバー IP アドレス通知のガイドライン


MB のミニポート ドライバーを指定する*EnableDhcp* 、INF ファイルにゼロが使用できる、 [IP ヘルパー](ip-helper.md)と関連付けられた[関数](https://msdn.microsoft.com/library/windows/hardware/ff557018)作成、変更、カーネル モードで、IP アドレスを削除します。

IP ヘルパー関数をカーネル モードで使用するには、ミニポート ドライバーは Netioapi.h ヘッダー ファイルを含めるし、Netio.lib に対してリンクをする必要があります。

ミニポート ドライバーを指定すると*EnableDhcp* MB サービスについて、次のイベントのいずれかを通知する次の操作を実行する必要が 0 に等しい。

-   MB インターフェイスの IP アドレスを設定します。

-   既定のゲートウェイ アドレスを設定します。

-   DNS アドレスを更新します。

永続化ネットワークの IP アドレスと IP ヘルパー API を使用して設定されている既定のゲートウェイ接続または切断イベント、またはその両方です。 そのためかどうか、新しい IP アドレスまたは既定のゲートウェイ、またはその両方、値は、値が設定されているものと異なる場合、ミニポート ドライバー ネットワーク接続のイベントに新しい値を設定する前に前の値をクリアする必要があります最初。

**注**  ミニポート ドライバーを見つけることができます、 **LUID**と**インデックス**MB インターフェイスからの**NetLuid**または**IfIndex**のメンバー [ **NDIS\_ミニポート\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565972)ミニポートのドライバーに渡される構造[*MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

 

### <a name="resetting-the-ip-address-and-gateway-address"></a>IP アドレスとゲートウェイのアドレスをリセットします。

必須フィルター ドライバーの読み込みなど、TCP/IP スタックを特定の変更は、IP アドレスとゲートウェイ アドレス IP ヘルパー関数で設定を削除できます。 ミニポート ドライバーは、TCP/IP スタックへの変更の設定を削除する場合、IP アドレスとゲートウェイ アドレスをリセットする必要があります。

ミニポート ドライバーは、次の手順を使用する必要があります、通知アドレスは削除され、もう一度リセットする必要があります。

1.  中に**ドライバーの初期化**、ミニポート ドライバーを使用して IP インターフェイスの変更通知を登録するコールバック関数を指定する必要があります[ **NotifyIpInterfaceChange** ](https://msdn.microsoft.com/library/windows/hardware/ff568805). Windows では、関数 wheneven IP インターフェイスの追加、削除または変更を呼び出します。

2.  中に**アダプターの初期化**、ミニポート ドライバーは、ミニポート ドライバーのローカル アダプターのコンテキストに保存する必要があります、 **LUID**値から、 [ **NDIS\_ミニポート\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565972)ミニポートのドライバーに渡される構造[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 値が含まれています、 *NetLuid*通知コールバックで使用されているアダプターのインターフェイスを識別します。

3.  **通知コールバック**、Windows が登録されている通知の関数に、次のパラメーターを渡します[ **NotifyIpInterfaceChange**](https://msdn.microsoft.com/library/windows/hardware/ff568805):

    -   ポインターを[ **MIB\_IPINTERFACE\_行**](https://msdn.microsoft.com/library/windows/hardware/ff559254)を含む構造、 *NetLuid*ミニポート アダプターのインターフェイス。
    -   通知の種類**MibAddInstance**、 **MibDeleteInstance**または**MibParameterNotification**します。

    アダプターが接続の状態と通知の種類が、ミニポート ドライバーは、IP アドレスとゲートウェイ アドレスをリセットする必要があります**MibAddInstance**、および*NetLuid*で[ **MIB\_IPINTERFACE\_行**](https://msdn.microsoft.com/library/windows/hardware/ff559254)アダプターの初期化中に保存された、ミニポート ドライバーのアダプターのいずれかに対応しています。

    ミニポート ドライバーでは、設定を従う必要がありますし、それぞれのアドレスをリセットする MB インターフェイスと既定のゲートウェイ アドレスの設定手順については、IP アドレス。

4.  中に**ドライバー アンロード**、ミニポート ドライバー、コールバック関数を使用して通知の登録を解除する必要があります、 [ **CancelMibChangeNotify2** ](https://msdn.microsoft.com/library/windows/hardware/ff544864) IP ヘルパー関数。

### <a name="setting-the-ip-address-for-the-mb-interface"></a>MB インターフェイスの IP アドレスの設定

IPv4 アドレスを設定するには、次の手順を使用します。 IP ヘルパーの同様の機能を使用すると、IPv6 アドレスを設定します。

1.  使用して、 [ **GetUnicastIpAddressTable** ](https://msdn.microsoft.com/library/windows/hardware/ff552594) IP ヘルパー関数をすべての IP アドレスのエントリは、システム。

2.  各エントリが**InterfaceLuid**値と一致する、 **InterfaceLuid** MB インターフェイスの。
    1.  前の接続で使用される IP アドレスと一致する IP アドレスのエントリを検索します。 初めて接続では、以前の IP アドレスを必要はありません。
    2.  新しい IP アドレスが以前の IP アドレスと異なる場合を使用して前の接続の IP アドレスの IP アドレスのエントリを削除、 [ **DeleteUnicastIpAddressEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff546370) IP ヘルパー関数。
    3.  新しい IP アドレス、以前の IP アドレスと同じである場合は、目的のエントリが既に存在することを確認します。

3.  ミニポート ドライバーには、前のループ内で目的の IP アドレスのエントリが見つからなかった場合、新しいエントリを追加する必要があります。
    1.  使用して、 [ **InitializeUnicastIpAddressEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554886)初期化するために IP ヘルパー関数を[ **MIB\_UNICASTIPADDRESS\_行**](https://msdn.microsoft.com/library/windows/hardware/ff559308)構造体し、構造体の次のメンバーを設定します。
        1.  設定、 **InterfaceLuid**または**InterfaceIndex**に応じてのメンバー。
        2.  設定、 **OnlinePrefixLength**メンバー。 これは、サブネット マスクのいずれかの値を持つビット数です。 たとえば、サブネット マスクは 255.255.255.0、 **OnlinePrefixLength** 24 にする必要があります。
        3.  設定、**アドレス**メンバー。
        4.  設定、 **PrefixOrigin**メンバー **IpPrefixOriginManual**します。

    2.  初期化の MIB を渡す\_UNICASTADDRESS\_行構造体を[ **CreateUnicastIpAddressEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff546227) IP を作成する IP ヘルパー関数のエントリに対応します。

### <a name="setting-default-gateway-address"></a>既定のゲートウェイ アドレスの設定

IPv4 ゲートウェイ アドレスを設定するには、次の手順を使用します。 IP ヘルパーの同様の機能を使用すると、IPv6 ゲートウェイ アドレスを設定します。

1.  使用[ **GetIpForwardTable2** ](https://msdn.microsoft.com/library/windows/hardware/ff552536) IP ヘルパー関数をシステムのすべてのルーティングのエントリを取得します。

2.  各エントリが**InterfaceLuid**値と一致する、 **InterfaceLuid** MB インターフェイスの値と**DestinationPrefix** 「0.0.0.0/0」、呼び出しが、 [**DeleteIpForwardEntry2** ](https://msdn.microsoft.com/library/windows/hardware/ff546365)場合、ルートを削除する IP ヘルパー関数**NextHop**新しいゲートウェイのアドレスと等しくないです。 それ以外の場合、ルーティングのエントリには、システムで既にです。

3.  使用して新しいエントリを追加する必要があります、ミニポート ドライバーには、前のループ内で必要なルーティング エントリが見つからなかった場合、 [ **InitializeIpForwardEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554882)初期化するために IP ヘルパー関数を[**MIB\_IPFORWARD\_ROW2** ](https://msdn.microsoft.com/library/windows/hardware/ff559245)構造体。 次の構造体のメンバーを初期化します。

    **InterfaceLuid**または**InterfaceIndex**します。

    設定**DestinationPrefix**デフォルト ゲートウェイに対して 0.0.0.0/0 をします。 (プレフィックス = 0.0.0.0 と PrefixLength = 0)

    設定**NextHop**デフォルト ゲートウェイの IP アドレスにします。

    他のメンバーは、初期化中に既定値に設定されます。 ミニポート ドライバーでは、そのメンバーの既定値を使用する必要があります。

4.  渡す、 [ **MIB\_IPFORWARD\_ROW2** ](https://msdn.microsoft.com/library/windows/hardware/ff559245)構造体を[ **CreateIpForwardEntry2** ](https://msdn.microsoft.com/library/windows/hardware/ff546209) IP ヘルパー新しい既定のゲートウェイ アドレスを設定する関数。

### <a name="to-set-dns-addresses"></a>DNS アドレスを設定するには

-   設定、**ネーム サーバー**レジストリ キー」の説明に従って[MB DNS 更新](mb-dns-updates.md)Windows の更新された DNS アドレスを通知します。

 

 





