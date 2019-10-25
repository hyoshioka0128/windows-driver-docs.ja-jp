---
title: MB ミニポート ドライバー IP アドレス通知のガイドライン
description: MB ミニポート ドライバー IP アドレス通知のガイドライン
ms.assetid: 23d74bc4-5648-45e3-a603-350d71bb16e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0ed78296b22f46cbc6dd8b6ebbfbdaa17d7821a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842470"
---
# <a name="guidelines-for-mb-miniport-driver-ip-address-notifications"></a>MB ミニポート ドライバー IP アドレス通知のガイドライン


INF ファイル内で*Enabledhcp*が0に等しいことを指定する、MB のミニポートドライバーは、 [ip ヘルパー](ip-helper.md)および関連する[関数](https://docs.microsoft.com/windows-hardware/drivers/network/ip-helper)をカーネルモードで使用して、ip アドレスの作成、変更、および削除を行うことができます。

IP ヘルパー関数をカーネルモードで使用するには、ミニポートドライバーに Netioapi ヘッダーファイルをインクルードし、Netio に対してリンクする必要があります。

ミニポートドライバーで*Enabledhcp*が0に等しいと指定されている場合、次の操作を実行して、次のいずれかのイベントについて MB サービスに通知する必要があります。

-   MB インターフェイスの IP アドレスを設定します

-   既定のゲートウェイアドレスの設定

-   DNS アドレスを更新する

IP ヘルパー API を使用して設定された IP アドレスと既定のゲートウェイは、ネットワーク接続イベントまたは切断イベント、あるいはその両方を保持します。 したがって、新しい IP アドレスまたはデフォルトゲートウェイ、またはその両方が現在設定されている値と異なる場合は、ネットワーク接続イベントで新しい値を設定する前に、ミニポートドライバーで前の値をクリアする必要があります。

**注**  ミニポートドライバーは、 [**NDIS\_ミニポート\_INIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)構造体の**netluid**または**IfIndex**メンバーから、MB インターフェイスの**LUID**と**インデックス**を見つけることができます。ミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数に渡されます。

 

### <a name="resetting-the-ip-address-and-gateway-address"></a>IP アドレスとゲートウェイアドレスのリセット

TCP/IP スタックに対する特定の変更 (必須のフィルタードライバーの読み込みなど) では、IP ヘルパー関数によって設定された IP アドレスとゲートウェイアドレスを削除できます。 TCP/IP スタックの変更によって設定が削除された場合は、ミニポートドライバーで IP アドレスとゲートウェイアドレスをリセットする必要があります。

ミニポートドライバーは、アドレスが削除されたときに通知されるように、次の手順を使用する必要があります。再設定する必要があります。

1.  **ドライバーの初期化**中に、ミニポートドライバーでは、 [**NotifyIpInterfaceChange**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568805(v=vs.85))を使用して、IP インターフェイスの変更通知に登録するコールバック関数を指定する必要があります。 Windows は、IP インターフェイスが追加、削除、または変更された場合でも、関数を呼び出します。

2.  **アダプターの初期化**中に、ミニポートドライバーはミニポートドライバーのローカルアダプターコンテキストに保存する必要があります。これは、ミニポートに渡される[**NDIS\_ミニポート\_INIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)構造からの**LUID**値です。ドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数。 値には、通知コールバックで使用されるアダプターのインターフェイスを識別する*Netluid*が含まれます。

3.  **通知コールバック**で、Windows は次のパラメーターを[**NotifyIpInterfaceChange**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568805(v=vs.85))に登録されている通知関数に渡します。

    -   \_行構造の[**MIB\_IPINTERFACE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85))へのポインター。これには、ミニポートアダプターのインターフェイスの*netluid*が含まれます。
    -   通知の種類。 **Mibaddinstance**、 **mibdeleteinstance** 、 **mibaddinstance**を指定できます。

    ミニポートドライバーは、アダプターが接続状態であり、通知の種類が**Mibaddinstance**で、MIB の*NETLUID* [ **\_ipinterface\_行**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85))がいずれかの値に対応している場合に、IP アドレスとゲートウェイアドレスをリセットする必要があります。アダプターの初期化中に保存されたミニポートドライバーのアダプター。

    ミニポートドライバーは、MB インターフェイスの IP アドレスを設定し、既定のゲートウェイアドレスを設定する手順に従って、各アドレスをリセットする必要があります。

4.  **ドライバーのアンロード**中、ミニポートドライバーは、 [**CancelMibChangeNotify2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544864(v=vs.85)) IP ヘルパー関数を使用して通知コールバック関数の登録を解除する必要があります。

### <a name="setting-the-ip-address-for-the-mb-interface"></a>MB インターフェイスの IP アドレスの設定

IPv4 アドレスを設定するには、次の手順を使用します。 同様の IP ヘルパー機能を使用して、IPv6 アドレスを設定できます。

1.  [**GetUnicastIpAddressTable**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552594(v=vs.85)) ip ヘルパー関数を使用して、システム内のすべての ip アドレスエントリを検索します。

2.  **InterfaceLuid**値が MB インターフェイスの**InterfaceLuid**と一致するエントリごとに、次のように入力します。
    1.  前の接続で使用した IP アドレスと一致する IP アドレスエントリを探します。 初回接続では、以前の IP アドレスは保持されません。
    2.  新しい IP アドレスが以前の IP アドレスと異なる場合は、 [**DeleteUnicastIpAddressEntry**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546370(v=vs.85)) ip ヘルパー関数を使用して、以前の接続 ip アドレスの ip アドレスエントリを削除します。
    3.  新しい IP アドレスが以前の IP アドレスと同じ場合は、目的のエントリが既に存在することを確認します。

3.  ミニポートドライバーが前のループで目的の IP アドレスエントリを見つけられなかった場合は、新しいエントリを追加する必要があります。
    1.  [**InitializeUnicastIpAddressEntry**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554886(v=vs.85)) IP ヘルパー関数を使用して、 [ **\_行構造\_MIB**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85))を初期化し、構造体の次のメンバーを設定します。
        1.  必要に応じて、 **InterfaceLuid**メンバーまたは**InterfaceIndex**メンバーを設定します。
        2.  オンラインの**プレフィックス**メンバーを設定します。 これは、サブネットマスクの値が1であるビットの数です。 たとえば、サブネットマスクが255.255.255.0 の場合、**オンラインのプレフィックス**は24にする必要があります。
        3.  **アドレス**メンバーを設定します。
        4.  **PrefixOrigin**メンバーを**IpPrefixOriginManual**に設定します。

    2.  IP アドレスエントリを作成するために、初期化された MIB\_\_行構造体を[**CreateUnicastIpAddressEntry**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546227(v=vs.85)) IP ヘルパー関数に渡します。

### <a name="setting-default-gateway-address"></a>既定のゲートウェイアドレスを設定しています

IPv4 ゲートウェイアドレスを設定するには、次の手順を使用します。 同様の IP ヘルパー機能を使用して、IPv6 ゲートウェイアドレスを設定できます。

1.  [**GetIpForwardTable2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552536(v=vs.85)) IP ヘルパー関数を使用して、システム内のすべてのルーティングエントリを取得します。

2.  **InterfaceLuid**値が MB インターフェイスの**InterfaceLuid**値に一致し、 **destinationprefix**が "0.0.0.0/0" である各エントリについて、 [**DeleteIpForwardEntry2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546365(v=vs.85)) IP ヘルパー関数を呼び出してルートを削除します (NextHop の場合)。が新しいゲートウェイアドレスと等しくありません。 それ以外の場合、ルーティングエントリはシステム内に既に存在します。

3.  ミニポートドライバーが、前のループで必要なルーティングエントリを見つけられなかった場合は、ROW2 構造体[ **\_の MIB\_IPFORWARD**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85))を初期化するために、初期化機能を[**使用して**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554882(v=vs.85))新しいエントリを追加する必要があります。 構造体の次のメンバーを初期化します。

    **InterfaceLuid**または**InterfaceIndex** 。

    既定のゲートウェイの**Destinationprefix**を 0.0.0.0/0 に設定します。 (プレフィックス = 0.0.0.0、プレフィックス = 0)

    **NextHop**をデフォルトゲートウェイの IP アドレスに設定します。

    その他のメンバーは初期化時に既定値に設定されます。 ミニポートドライバーは、これらのメンバーに既定値を使用する必要があります。

4.  [**MIB\_IPFORWARD\_ROW2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85))構造体を[**CreateIpForwardEntry2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546209(v=vs.85)) IP ヘルパー関数に渡して、新しいデフォルトゲートウェイアドレスを設定します。

### <a name="to-set-dns-addresses"></a>DNS アドレスを設定するには

-   「 [MB の Dns 更新](mb-dns-updates.md)」で説明されているように**NameServer**レジストリキーを設定して、更新された dns アドレスについて Windows に通知します。

 

 





