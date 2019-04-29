---
title: Bluetooth ドライバー スタック
description: Bluetooth ドライバー スタック
ms.assetid: fb13c300-f8ed-4d82-8625-79db4d7feac5
keywords:
- Bluetooth の WDK、ドライバー スタック
- ドライバーは、WDK Bluetooth をスタックします。
- WDK Bluetooth スタック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c144d01f08e51cc218917c93b8dc6c8c5bc2d2f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328320"
---
# <a name="bluetooth-driver-stack"></a>Bluetooth ドライバー スタック


Bluetooth ドライバー スタックは、Bluetooth プロトコルの Microsoft によって提供されるサポートのコア部分で構成されます。 このスタックと Bluetooth 対応デバイスはお互いを検索し、接続を確立します。 このような接続を介して、デバイスがデータを交換し、さまざまなアプリケーションを通じて互いにやり取りできます。

次の図は、可能なカスタムのユーザー モードとカーネル モード ドライバーが Windows Vista 以降に含まれていない、Bluetooth ドライバー スタック内のモジュールを示します。 これらのカスタム ドライバーは、プロファイルのドライバーと呼ばれます。

![bluetooth ドライバー スタックを示す図](images/bluetooth-architecture.png)

-   **ユーザー モード**
    -   **ユーザー モード アプリケーション**-公開 Api を通じて、Bluetooth ドライバー スタックにアクセスするユーザー モード アプリケーション。 詳細については、次を参照してください。[について Bluetooth](https://go.microsoft.com/fwlink/p/?linkid=50712) Windows SDK のドキュメント。

        **注**  に対してユーザー モード アプリケーションをリンクする必要があります*BthProps.lib*の代わりに*IrProps.lib*などの Api を使用するために、 [ **BluetoothSetLocalServiceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff536580)します。

         

-   **プロファイルのドライバーの例**
    -   **カーネル モード ドライバーの WAP**-ワイヤレス アプリケーション プロトコル (WAP) のコンポーネントは、Windows ネットワーク スタックと L2CAP インターフェイスと、必要に応じて、SDP インターフェイスにアクセスする BthPort 間の通信をプロファイル ドライバーの例に示しますL2CAP に含まれます。 可能なその他のプロファイルは、A の高度なオーディオ配布プロファイル (A2DP)/V リモート_コントロール プロファイル (AVRCP) ジェネリック A/V 配布プロファイル (GAVDP) と共通 ISDN アクセス (CIP) プロファイルです。
    -   **オーディオのカーネル モード ドライバー**- プロファイル ドライバー、Windows オーディオ スタックと BthPort、後者に含まれている SCO インターフェイスへのアクセスとの通信の例です。 可能なプロファイルには、自在プロファイル (HFP)、ヘッドセット プロファイル (HSP)、コードレス テレフォニー プロファイル (CTP)、およびインターコム プロファイル (ICP) が含まれます。
        **注**  このプロファイルのドライバーが Windows 8 以降の Windows に含まれています。

         

    -   **Bluetooth LE 心拍数モニター プロファイル**- で、Bluetooth 低エネルギー (LE) API と通信する Bluetooth LE プロファイル ドライバーの例です。
-   **Bluetooth ドライバー スタック コンポーネント**
    -   **IrProps**-Bluetooth ドライバー スタックの最初のバージョンに対して作成されるプロファイルのドライバーの旧バージョンと互換性のために使用されるコンポーネント。

        **注**  **IrProps**旧バージョンと互換性のためだけに提供されます。 使用して、 **BthProps**新規の開発コンポーネント。

         

    -   **BthProps**-Bluetooth ユーザーの実装を含むコンポーネント インターフェイスの Bluetooth Api の実装と共にユーザー モード アプリケーションがアクセスします。 このコンポーネントは、リモート プロシージャ コール (RPC) を介して BthServ に問い合わせを送信します。 さらに、BthProps プライベート Ioctl を BthPort との交換を暗証番号 (pin) を実行します。 BthProps が bluetooth 無線と任意のシステムで実行されるに注意してください。
    -   **BthServ**-キャッシュおよび Bthport へ照会データの転送を担当するサービス。
    -   **BthCi**-Bluetooth クラス インストーラー。
    -   **WshBth**-、Bluetooth Windows ソケット ヘルパー コンポーネント。 WshBth はソケット操作を実行する Windows ソケット レイヤーによって呼び出されます。 WshBth は、主に、TDI インターフェイスを通じて RfComm を呼び出します。 リモート デバイスの照会を実行する BthServ とローカル ラジオの照会を実行する BthPort にも WshBth を呼び出します。
    -   **FSquirt**-ユーザーが Bluetooth 接続を開いているファイルを送受信できる nonextensible オブジェクト交換 (OBEX) コンポーネントです。 OBEX は、RFCOMM WshBth コンポーネントを使用して使用してリモート デバイスと通信します。
    -   **BthPrint**-ハードコピー ケーブル置換プロファイル (HCRP) を実装するコンポーネント。 このコンポーネントは、データを送信し、Bluetooth 対応プリンターからデータを受信する印刷システムを使用できます。 BthPrint リモート プリンターを照会する BthPort で SDP インターフェイスとデータを送受信する BthPort で L2CAP インターフェイスと通信します。
    -   **HidBth**-ヒューマン インターフェイス デバイス (HID) プロファイルを実装するコンポーネント。 HidBth は BthPort L2CAP、SDP のインターフェイスとも通信します。 USB HID モジュールと同様に、HidBth は HID スタックに接続します。
    -   **BthPan**-Bluetooth 接続を開いている TCP 接続を提供する、パーソナル エリア ネットワーク (PAN) プロファイルを実装するコンポーネント。 Windows Vista および Windows XP では、BthPan は発信接続のみをサポートします。 BthPan が BthPort コンポーネントのクライアントでもあり L2CAP と SDP の両方のインターフェイスを使用します。
    -   **RfComm**-Bluetooth シリアル ケーブル エミュレーションのプロトコルを実装するコンポーネント。 RfComm は BthPort で見つかった L2CAP および SDP インターフェイスも使用します。 RfComm の上端は、ネットワーク トランスポートを表示するには、このコンポーネントを許可する、TDI インターフェイスを公開します。 これは、ユーザー モード Api からデータを送受信する Bluetooth に WshBth が接続する方法です。

        ユーザー モード アプリケーションでは、Windows SDK で説明されている Winsock インターフェイスを使用して RfComm をアクセスできます。

    -   **BthModem**-仮想 COM ポートとダイヤルアップ ネットワーク (DUN) を実装するコンポーネント。 BthModem は、RfComm に位置している I/O とコントロールのすべての操作に、TDI インターフェイスを通じてを指示します。 BthModem の上端と通信*スタック*ワイヤレスの COM ポートの外観にします。
        **注**  このコンポーネントは Windows RT. で使用できません

         

    -   **BthEnum**-Bluetooth バス ドライバー。 BthEnum を作成し、Bluetooth サービスを有効にするために使用するデバイス オブジェクトを破棄するには、プラグ アンド プレイ (PnP) マネージャーと通信します。 BthEnum では、接続されているリモート デバイスをサポートするすべてのサービスの PDO を作成します。 たとえば、ユーザーは、Bluetooth 対応マウスを接続するときに、マウスが非表示に Bluetooth サービスをサポートしているし、HID サービスが原因で読み込む HidBth PnP マネージャーの PDO を作成の Windows では検出します。

        **注**  BthEnum に表示されるサービスの Pdo を作成できませんが、 **UnsupportedServices**レジストリ キーで指定されている*Bth.inf*します。

         

    -   **BthLEEnum**-Bluetooth 低エネルギー (LE) バス ドライバー。 BthLEEnum は、ATT プロトコルと GATT プロファイルを実装します。 リモート デバイスとその主要なサービスを表すための Pdo を作成する責任を負いますもできます。

    -   **BthPort**-BthUsb ミニポートによって、ミニドライバーが読み込まれます。 BthPort では、4 つのコンポーネントを提供します。
        -   HCI コンポーネントは、ローカル bluetooth ラジオ Bluetooth 仕様で定義されているホスト コント ローラー インターフェイス (HCI) を介して通信します。 Bluetooth 対応のすべてのラジオは HCI の仕様を実装するため、BthPort は、製造元またはモデルに関係なく、Bluetooth が有効なオプションと通信できるようにします。
        -   SCO コンポーネントは、Synchronous Connection-Oriented (SCO) プロトコルを実装します。 このプロトコルは、リモート デバイスへの作成のポイント ツー ポイント接続をサポートします。 SCO クライアントと通信して SCO インターフェイス[のビルドと送信](building-and-sending-a-brb.md)Bluetooth 要求のブロック (BRBs)。
        -   L2CAP では、Bluetooth の論理リンク コントロールと適応プロトコルを実装します。 このプロトコルは、リモート デバイスにロスレス チャネルの作成をサポートします。 L2CAP クライアントは、構築して Bluetooth の要求のブロック (BRBs) を送信することで、L2CAP インターフェイスと通信します。
        -   SDP では、Bluetooth サービスの探索プロトコルを実装します。
    -   **BthUsb.sys**-からバスのインターフェイスを抽象化するミニポート**BthPort**します。

 

 





