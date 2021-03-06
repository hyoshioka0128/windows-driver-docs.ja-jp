---
title: Wi-Fi ホット スポット オフロード アーキテクチャ
description: Wi-Fi ホット スポット オフロード アーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28e848f5f4c92eb741c7dc023964d5952a2d9600
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365755"
---
# <a name="wi-fi-hotspot-offloading-architecture"></a>Wi-Fi ホット スポット オフロード アーキテクチャ

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

次の図は、Wi-fi オフロード Framework の主要なコンポーネントを示します。

![Wi-fi ホット スポット オフロード Framework](images/WiFi_Hotspot_Offload-1.png "Wi-fi ホット スポット フレームワークをオフロードします。")

## <a name="hotspot-offload-service"></a>ホット スポットのオフロード サービス

ホット スポットのオフロード サービスでは、次の関数を実行します。

* ホット スポット ネットワーク、Wi-fi ネットワークを識別します。
* 作成と保守のホット スポット ネットワークへの接続を監視します。
* ホット スポット ネットワークの接続状態の変更を監視し、応答
* 監視し、有効化または Wi-fi ホット スポットのオフロードを無効にするために応答するユーザー設定の変更

ホット スポットのオフロード サービスを特定し、ホット スポット ネットワークの認証には、携帯電話会社や Oem によって作成されたホット スポットのプラグインに依存します。

## <a name="hotspot-plugin-host"></a>ホット スポットのプラグインのホスト

ホット スポットのプラグインのホストでは、ホット スポットの間のインターフェイスがサービスとパートナー実装のホット スポットのプラグインをオフロードします。 たとえば、ネットワークの一覧からのホット スポット ネットワークを識別するために、ホット スポット プラグインへのクエリは、ホット スポットのプラグインのホストを通じて行われます。 プラグインのホストでは、特に、送信し WinHTTP または WinInet API を使用して HTTP メッセージを受信およびユーザーに SMS アラートと通知を送信する、ホット スポット プラグインも可能です。

ホット スポットのオフロード サービスは、ホット スポットのプラグインごとのホット スポット プラグインのホストを作成します。

## <a name="hotspot-plugin"></a>ホット スポットのプラグイン

ホット スポットのプラグインは、次の関数を実行します。

* 使用可能なネットワークの一覧からのホット スポット ネットワークを識別します。
* OEM または携帯電話会社によって指定された EAP-SIM/別名および HTTP ベースの認証を使用してネットワークに自動接続にします。
* WinHTTP または WinInet API を使用して HTTP メッセージの送信/受信します。
* ユーザーに SMS 通知を送信します。
* 移動体通信ネットワーク経由でメッセージを送受信する HTTP 要求のベアラー トークンを選択します。

また、次の外部コンポーネントと直接対話します。

* WinInet/WinHTTP

携帯電話会社や Oem が実装し、Wi-fi オフロードを有効にするには、独自のホット スポット プラグインをインストールする必要があります。 プラグインのインストール パッケージには、次の項目が含まれます。

* プラグイン DLL
* Ssid、暗号化された資格情報などのリストなどの特定の接続情報を含むファイル。
  * **注:** これらのファイルは、省略可能なほとんどのプラグインではありません。
* レジストリの構成

## <a name="hotspot-user-interface"></a>ホット スポットのユーザー インターフェイス

ホット スポットのユーザー インターフェイスは、Wi-fi のコントロール パネルに表示されます。 ユーザー インターフェイスから、ユーザーことができます。

* 自動 Wi-fi ホット スポットのオフロードを有効または無効にします。
* ホット スポット ネットワークへの自動接続中に、接続の状態を表示します。
* 手動でホット スポット ネットワークに接続します。
  * ホット スポットをオフロードする場合、デバイスの機能が有効になっている、サービスの負荷を軽減する、ホット スポット ネットワークへのユーザーが開始した接続が検出されたホット スポット ネットワークは、Wi-fi ホット スポット ネットワークに自動接続として処理されます。 それ以外の場合、手動の接続は、標準の Wi-fi 接続として処理されます。
* 通信事業者のホット スポットの接続がユーザーによって無効になっている場合は、ホット スポット ネットワークに接続するための通常の Wi-fi プロファイルを構成します。

ホット スポットのユーザー インターフェイスは、少なくとも 1 つのプラグインが構成されている場合にのみ表示されます。

## <a name="example-automatic-connection-to-a-hotspot-network"></a>以下に例を示します。ホット スポット ネットワークへの自動接続

ホット スポット ネットワークへの自動接続中に発生したコンポーネントの相互作用のシーケンスの非常に大まかな説明を次に示します。

1. Wi-fi 接続サービスは、ホット スポットのオフロード サービスに接続されていないネットワークの一覧を送信します。
2. ネットワークの一覧で、各エントリのホット スポットのオフロード サービス クエリ (ランク付けされて、プラグインの順序) でホット スポットのプラグインを実行するは、ホット スポット ネットワーク。 ネットワークを識別する最初のプラグインは接続時にそのネットワークの認証を求められます。
3. (サービスは HTTP ベース、または EAP SIM ベース、または特定の SIM が必要としない) かどうかを使用する認証方法は、そのネットワークに関連付けられている優先度の値を返しますとホット スポットのプラグインでは、ホット スポット ネットワークとネットワークを識別、および、必要に応じて、ネットワークマスクを表示します。 優先度の値は、接続を試行する順序を示します。 高い値を持つネットワークに接続する前に、低い優先順位の値を持つネットワークへの接続が試行されます。
4. ホット スポットのオフロード サービスでは、選択したネットワークの接続マネージャー プロファイルを作成します。
5. ホット スポットのオフロード サービス プロファイルは、接続マネージャーをアプリケーション ブロックを承認するまでのネットワークに接続できない原因となる初期のポリシー設定を構成も可能性があります。
6. ホット スポットのオフロード サービスは、ホット スポット ネットワークとして選択したネットワークをマークします。
7. ホット スポットのオフロード サービスがホット スポットのプラグインのホストをホット スポット プラグインを呼び出す、行ういずれかの接続前の接続処理が必要な場合。
8. ホット スポットのプラグインが完了した後は、事前処理を接続、ホット スポットのオフロード サービスがホット スポット ネットワークに接続し、接続完了または失敗の通知を提供する接続マネージャーを待機します。
9. ホット スポットのオフロード サービスが要求を送信する接続完了時に、ホット スポットに必要なを実行するためのプラグイン接続後 HTTPS exchange などのアクション。
10. それまでは、ホット スポットのオフロード サービスは、次を行います。
    * 完了のタイマーを開始します (現在、5 分後に起動に設定する) アクティビティを接続後に実行
    * 適切なユーザー インターフェイスのセットの状態を表示します。
11. ホット スポットのプラグイン接続が成功した場合、ホット スポットのオフロード サービスは、接続のブロックを解除し、アプリケーションに通知するには、接続マネージャーを呼び出します。
12. 後の接続要求がタイムアウトした場合。
    * ホット スポットのオフロード サービスは、ホット スポット プラグインの状態をリセットします。
    * 再試行がない場合がホット スポットのオフロード サービスを開始し再接続しようと、それ以外の場合、ネットワークのホット スポットのプロファイルを削除します。
13. それ以外の場合、ホット スポットのプラグインでは、エラーと再試行が可能であれば、再接続しようとすると、サービスの開始をオフロードする、ホット スポットを示している場合、ネットワークのホット スポットのプロファイルを削除します。

