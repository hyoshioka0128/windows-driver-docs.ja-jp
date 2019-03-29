---
title: MB プロビジョニング済みコンテキスト操作
description: MB プロビジョニング済みコンテキスト操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b472c9c19d2299ecb08f7df3999b9570e8328cec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573325"
---
# <a name="mb-provisioned-context-operations"></a>MB プロビジョニング済みコンテキスト操作

各携帯電話会社にそのネットワークの別の APN 構成があるために、プロビジョニングは携帯電話接続可能なデバイスに不可欠です。 APN の構成は、2 つのカテゴリに一般的に分割できます。

1. アプリケーションまたはそれらの接続を必要とする OS 上のクライアントがあるため、OS に認識されている APN 構成します。
2. いないに加えられた既知、OS は、OS およびそのクライアントは、まだ活用していない接続用モデムによって内部的に利用されますので、APN 構成します。

理想的には、モデムは、OS が認識する必要はありません、APN 構成をのみ格納する必要があります。 ただし、IHV および OEM のパートナーが通例、インターネットと購入の APNs、既知のモデムでのオペレーティング システムを構成します。 Windows 10 バージョン 1703 のリリースでは、前に Windows は、インターネットと購入の APN の構成のインターネット接続を確立するために、モデムからのみ読み取ることにします。 以降では、Windows 10 バージョン 1703 である可能性がありますをモデムの APN 構成する必要があります、Windows によって管理される携帯電話の設定を変更するユーザー設定など、OS や OMA DM 内のクライアントがある場合に特にケースを追加します。 これは、さらに可能性がありますもモデムの APN の構成に影響します。 たとえば、ある可能性があります、IMS スタック IMS 経由で sms IMS APN を使用されているモデムでします。 通常、特定のシナリオにおける IMS APN 構成を変更する必要がありますが、os、それらの接続は公開されません。 この変更は、OS から実行できます。 これをサポートするために、OS を Windows 10 バージョン 1703 以降、モデムに APNs のさまざまな種類を構成できます。

USB フォーラムの MBIM 1.0 と Microsoft NDIS、既存の CID OID それぞれできるようになり、モデムの APN 構成の照会や設定を OS があります。 MBIM 1.0 は MBIM_CID_PROVISIONED_CONTEXT はこれを NDIS の[OID_WWAN_PROVISIONED_CONTEXTS](https://msdn.microsoft.com/library/windows/hardware/ff569831)します。 ただし、既存の CID と OID に設計されていません、モデムの電源を入れまたは SIM スワップなど、さまざまな状況で動作が予想される方法の明確なガイダンスとします。 OS の構成をサポートするデバイスをモデム プロビジョニングのコンテキストの今後の更新で Windows 10 バージョン 1703 OID、CID の新しいバージョンを実装する必要があります。 Ihv と Oem の OS バージョン 1703 より前に新しいハードウェアをサポートする下位互換性を確保できるように、既存 MBIM_CID_PROVISIONED_CONTEXT OID_WWAN_PROVISIONED_CONTEXTS をサポートするために続行する必要があります。  以降 Windows 10 では、バージョン 1703、デバイスは、OID OS し、CID の新しいバージョンをサポートしている場合はのみを使用して、コマンドの新しいバージョンを照会して、モデムの APN コンテキスト構成を設定します。 

## <a name="mb-interface-update-for-provisioned-context-operations"></a>プロビジョニングされたコンテキスト操作 MB インターフェイスの更新

MBIM には、コマンドを取得し、モデムに格納されているコンテキストを交換するため、フィールドを「無効」または「有効」プロファイルがありません。  そのため、Windows 10 バージョン 1703 をこの機能を含めるの既存の MBIM_CID_PROVISIONED_CONTEXT を更新する必要があります。 MBIM はバージョン管理メカニズムがあるないために、新しい MSFT 独自 CID が MBIM_CID_MS_PROVISIONED_CONTEXT_V2 として定義されます。

サービス名 = **Basic 拡張機能の接続**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 値 = **3d01dcc5 fef5-4 d 05-0d3abef7058e9aaf**

| CID | コマンド コード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_MS_PROVISIONED_CONTEXT_V2 | 1 | Windows 10 Version 1703 |

### <a name="mbimcidmsprovisionedcontextv2"></a>MBIM_CID_MS_PROVISIONED_CONTEXT_V2

#### <a name="description"></a>説明

MBIM 1.0 に MBIM_CID_PROVISIONED_CONTEXT が定義されている場合、従来、モデム、Windows 内のプロビジョニングのコンテキストを管理するには、OS とその上のクライアントのみモデムのコンテキストのクエリが、OS から設定できませんでした。 増え続けるニーズ、モデムのコンテキストを構成できるように、os は Windows 10 バージョン 1703 以降します。 たとえば、モデム、OS に対して非透過的ですに、IMS スタックがある場合、OS は IMS APN モデムを使用する必要がありますを指定することのようになります。 各モデムの IHV、モデムにコンテキストを格納する独自の独自の方法を持てないため、os ContextId レベル MBIM_CID_PROVISIONED_CONTEXT が示している可能性が方法でプロファイルを管理することはできません。 代わりに、OS の観点からコンテキストの種類ごとに使用するには、どのコンテキストを規定する必要があります。 IMS 例に戻って、既存プロビジョニングされているコンテキストの数は、モデムに関係なく、OS が MBIM_CONTEXT_TYPE を備えているコンテキストを設定している場合 = IMS モデムで開始されたすべての IM トラフィックは、そのコンテキストでのみ実行する必要があります。

MBIM 1.0 では、MBIM_CID_PROVISIONED_CONTEXT が挿入された SIM カードのプロバイダー ID (MCC/mnc もペア) に一致するコンテキストでクエリを呼び出すことができますのみことを指定します。 要求のセット、MBIM_CID_PROVISIONED_CONTEXT は格納するコンテキストのプロバイダー ID を指定できます。  MBIM_CID_MS_PROVISIONED_CONTEXT_V2 は、MBIM 1.0 から似ていますが、異なる動作を指定します。 各クエリでは、OS が継続だけ挿入 SIM カードのプロバイダー ID に一致するコンテキストを返し、モデムを期待します。 セットに、そのコマンドは不要になったセット コンテキスト SIM カードでは、現在のプロバイダー ID と一致しない OS を有効になります。 セットの要求が提示された SIM カードの現在のプロバイダー ID のコンテキストを作成することが期待されます。 たとえば、ユーザーのスワップを SIM 1 SIM 2 を再び、SIM 1 にします。 最初の SIM スワップ中に、モデムを解決する、すべてのコンテキスト SIM 2 のコンテキストを読み込む前に必要です。 ユーザーを入れ替えます SIM 1 に戻すとき、は、SIM 1 の工場出荷時の既定の構成を復元する必要があります。  モデム SIM スワップのランタイム構成を保存するには必要ありません。

次の図は、1 つ目にし、別、1 つの SIM からユーザーが交換する場合のサンプル フローを示しています。

![SIM のスワップの例をプロビジョニングするモデム コンテキスト](images/Context_Provision_modem_context_1.png "SIM スワップの例をプロビジョニングするモデム コンテキスト")

Oem および Ihv、モデムが事前構成されているは、OS またはユーザーが元の設定に、モデムでコンテキストの設定を復元する場合、工場出荷時の元の構成を保持する必要があります。 挿入された現在 SIM のプロバイダー ID の元のファクトリ コンテキストのみを復元する必要があります。 元のファクトリ構成済みのコンテキストを設定は、OS の構成で上書きするかことはありません。 次の図は、出荷時の設定を復元するユーザーが選択したときのフローの例を示します。

![ファクトリのプロビジョニング モデム コンテキストの例のリセット](images/Context_Provision_modem_context_2.png "ファクトリのプロビジョニング モデム コンテキストの例のリセット")

モデムがロックされている、SIM が存在しないか、プロバイダー ID にアクセスできないときに、クエリまたはセットの要求を失敗と想定されます。 モデムはプロバイダーの id。 あたりコンテキスト タイプごとの 1 つだけのコンテキストを持ちます IHV および OEM は、モデムのモデムのコンテキストを事前に構成を決定したら場合、は、そのためには、選択の各プロバイダーのコンテキストが正しく構成されていることを確認するために重要です。 事前構成済みのコンテキストを挿入 SIM カードに IHV がない場合、モデムには、OS の構成を行わなくても、コンテキストはありません。 Ihv と Oem MBIM_MS_CONTEXT_SOURCE ことを確認する必要があります。 OS が存在する場合は、接続、モデムのコンテキストを使用して Windows の APN データベースから上書きしないように MbimMsContextSourceModemProvisioned を = です。

モデムのマップのコンテキストを処理および既存 MBIM_CID_PROVISIONED_CONTEXT でもう一度表示は、各 IHV まではあり、このドキュメントのスコープ外です。

新しい MBIM_CID_MS_PROVISONED_CONTEXT_V2 コマンドはほぼ同じ MBIM 1.0 の既存の MBIM_CID_PROVISIONED_CONTEXT コマンドがいくつか追加します。 1 つ目は、有効またはモデムでコンテキストの種類に関連付けられているコンテキストを無効にすることができます、OS を提供します。 モデムのコンテキストが無効の場合は、いない認識、OS にも含め、ネットワーク接続が任意の格納されたコンテキストを使用しないように、モデムが必要です。 OS では、モデムで無効になっているコンテキストと一致する接続を要求している場合、モデムが要求即座に失敗、ネットワークに通知なし。 照合プロセスは、MBIM_MS_CONTEXT_V2 構造体のすべてのフィールドと一致する必要があります。

MBIM 1.0 から MBIM_CONTEXT_IP_TYPE 構造は MBIM_CID_CONNECT のみ使用します。 MBIM_CID_MS_PROVISIONED_CONTEXT_V2、Microsoft が各コンテキストのパラメーターの 1 つとして、IP の種類を追加します。 特定のコンテキストで構成されていない場合、モデムは MBIMContextIPTypeDefault を報告する必要があります。 

Windows 10 バージョン 1703、MBIM_CID_MS_PROVISIONED_CONTEXT_V2 をサポートする新しいハードウェアにレガシ MBIM_CID_PROVISIONED_CONTEXT はパーティのコンポーネントを最初から使用されません。 MBIM_CID_PROVISIONED_CONTEXT を送信するその他のレガシ クライアントの OS コンポーネントがある場合は、Windows 10 バージョン 1703 より前のバージョンの Windows でのように結果を返す、モデムが必要です。

##### <a name="query"></a>Query

MBIM_MS_PROVISIONED_CONTEXTS_INFO、InformationBuffer でクエリとセットの両方の完全なメッセージが返されます。 

クエリの場合、InformationBuffer が null です。

##### <a name="set"></a>Set

セットには、InformationBuffer には MBIM_MS_SET_PROVISIONED_CONTEXT_V2 構造体が含まれます。 設定操作で各モデムの IHV に独自のコンテキストの記憶域の管理方法があるため、不要になった OS が ContextId フィールドを指定し、コンテキストを適切なスロットにマップするモデムが必要です。 ときに、OS のセットのコンテキストが必要で、モデムに指定されたコンテキストの MBIM_CONTEXT_TYPE に一致するすべての接続に使用します。 MBIM_CONTEXT_TYPE がモデムが認識されない場合でもを格納することがそれに接続できない場合でもです。

##### <a name="unsolicited-event"></a>要請されていないイベント

イベント InformationBuffer には MBIM_MS_PROVISIONED_CONTEXTS_INFO_V2 構造体が含まれています。 場合によっては、プロビジョニングのコンテキストの一覧は、ネットワークによって、Over-The-Air (OTA) を更新またはでショート メッセージ サービス (SMS) を MBIM_CID_MS_PROVISIONED_CONTEXT_V2 を経由しませんが、OS からコマンドします。 関数は、する必要がありますプロビジョニングのコンテキストの一覧を更新および MBIM_MS_CONTEXT_SOURCE をタグ付け MbimMsContextSourceOperatorProvisioned を適宜 =。 その後、関数が更新された一覧で、このイベントを使用して更新プログラムについて、ホストに通知する必要があります。

#### <a name="parameters"></a>パラメーター

|  | Set | Query | Notification |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_MS_PROVISIONED_CONTEXT_V2 | 適用なし | 適用なし |
| 応答 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 |

#### <a name="data-structures"></a>データ構造体

##### <a name="query"></a>Query

InformationBuffer は NULL にするものとし、InformationBufferLength を 0 にする必要があります。

##### <a name="set"></a>Set

次の MBIM_SET_MS_PROVISIONED_CONTEXT_V2 データ構造は、InformationBuffer で使用されます。


| Offset | サイズ |       フィールド        |              型               |                                                                                                                                                                                                                                                                                                   説明                                                                                                                                                                                                                                                                                                   |
|--------|------|--------------------|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |     操作      |   MBIM_MS_CONTEXT_OPERATIONS    |                                             SET コマンドを使用する対象の操作の種類を指定します。 場合 MbimMsContextOperationDelete し、指定されたコンテキストに設定 MBIM_CONTEXT_TYPES が削除する必要がありますされ MBIM_SET_MS_PROVISIONED_CONTEXT_V2 で他のすべてのフィールドを無視する必要があります。  MbimMsContextOperationRestoreFactory に設定と、すべての OS が作成または変更されたコンテキストを削除するか、既定のファクトリ事前構成済みのコンテキストを読み込む必要がと MBIM_SET_MS_PROVISIONED_CONTEXT_V2 の他のすべてのフィールドを無視する必要があります。、                                              |
|   4    |  16  |    ContextType     |       MBIM_CONTEXT_TYPES        |                                                                                                                                                                                                表される; コンテキストの種類を指定しますインターネット接続、VPN (企業ネットワークに接続)、またはボイス オーバー IP など (VOIP)。 詳細については、MBIM_CONTEXT_TYPES テーブルを参照してください。                                                                                                                                                                                                |
|   20   |  4   |       IPType       |      MBIM_CONTEXT_IP_TYPES      |                                                                                                                                                                                               表される; コンテキストの種類を指定しますインターネット接続、VPN (企業ネットワークに接続)、またはボイス オーバー IP など (VOIP)。 詳細については、MBIM_CONTEXT_IP_TYPES テーブルを参照してください。                                                                                                                                                                                               |
|   24   |  4   |       Enable       |     MBIM_MS_CONTEXT_ENABLE      |                                                                                                                                                                     コンテキスト、モデムで使用できるかどうかを指定します。 MbimMsContextDisabled に設定されている場合、ネットワークに通知せず、コンテキストに一致するすべての OS 接続要求を失敗する必要があります。 詳細については、MBIM_MS_CONTEXT_ENABLE テーブルを参照してください。                                                                                                                                                                     |
|   28   |  4   |      Roaming       | MBIM_MS_CONTEXT_ROAMING_CONTROL |                                                                                                                                                                                                                                       このコンテキストではなくまたはローミングが許可されているかどうかを指定します。 詳細については、MBIM_MS_CONTEXT_ROAMING_CONTROL テーブルを参照してください。                                                                                                                                                                                                                                        |
|   32   |  4   |     MediaType      |   MBIM_MS_CONTEXT_MEDIA_TYPE    |                                                                                                                                                                                                                                         コンテキストでの使用は、メディアの輸送の種類を指定します。 詳細については、MBIM_MS_CONTEXT_MEDIA_TYPE テーブルを参照してください。                                                                                                                                                                                                                                         |
|   36   |  4   |       ソース       |     MBIM_MS_CONTEXT_SOURCE      |                                                                                                                                                                                                                                                    コンテキストの作成のソースを指定します。 詳細については、MBIM_MS_CONTEXT_SOURCE テーブルを参照してください。                                                                                                                                                                                                                                                    |
|   40   |  4   | AccessStringOffset |             オフセット              | 文字列、AccessString、ネットワークにアクセスするデータ バッファーのオフセットします。 GSM ベースのネットワークでは、"data.thephone company.com"など、アクセス ポイント名 (APN) 文字列になります。 CDMA ベースのネットワークでは、これがあります「#777」またはネットワーク アクセスの識別子 (NAI) などの特殊なダイヤル コードなど"foo@thephone-company.com"。 このメンバーは、APN の既定のネットワークを割り当てることを要求する NULL を指定できます。 注:すべてのネットワークは、ため、無効な APN によって発生した接続エラー、考えられる結果のこの NULL APN 規則をサポートします。 文字列のサイズは 100 文字を超えない必要があります。 |
|   44   |  4   |  AccessStringSize  |          SIZE(0..200)           |                                                                                                                                                                                                                                                                                           AccessString に使用するサイズ。                                                                                                                                                                                                                                                                                           |
|   48   |  4   |   UserNameOffset   |             オフセット              |                                                                                                                                                                                                                         計算される、この構造体の先頭から、ユーザー名、認証するユーザー名を表す文字列へのバイト オフセットします。 このメンバーは、NULL を指定できます。                                                                                                                                                                                                                         |
|   52   |  4   |    UserNameSize    |          SIZE(0..510)           |                                                                                                                                                                                                                                                                                            ユーザー名に使用するサイズ。                                                                                                                                                                                                                                                                                             |
|   56   |  4   |   PasswordOffset   |             オフセット              |                                                                                                                                                                                                                           ユーザー名のパスワードを表すオフセット (バイト)、文字列、パスワードに、この構造体の先頭から計算されます。 このメンバーは、NULL を指定できます。                                                                                                                                                                                                                            |
|   60   |  4   |    PasswordSize    |          SIZE(0..510)           |                                                                                                                                                                                                                                                                                             パスワードを使用するサイズ。                                                                                                                                                                                                                                                                                             |
|   64   |  4   |    圧縮     |        MBIM_COMPRESSION         |                                                                                                                                                                         ヘッダーとデータのデータ接続に使用する圧縮形式を指定します。 このメンバーは、GSM ベースのデバイスにのみ適用されます。 ホストは、CDMA ベースのデバイス、MBIMCompressionNone にこのメンバーを設定します。 詳細については、MBIM_COMPRESSION テーブルを参照してください。                                                                                                                                                                          |
|   68   |  4   |    AuthProtocol    |       MBIM_AUTH_PROTOCOL        |                                                                                                                                                                                                                                                   PDP ライセンス認証を使用する認証の種類。 詳細については、MBIM_AUTH_PROTOCOL テーブルを参照してください。                                                                                                                                                                                                                                                    |
|   72   |  4   |     DataBuffer     |           DATABUFFER            |                                                                                                                                                                                                                                                                       AccessString、UserName、およびパスワードを格納しているデータ バッファー。                                                                                                                                                                                                                                                                       |

上記の表に、次のデータ構造が使用されます。

MBIM_MS_CONTEXT_ROAMING_CONTROL は、コンテキストごとの移動ポリシーを指定します。 OS は、かどうかをローミング中に指定されたコンテキストを有効にできるかどうかを指定できます。 モデム セルフ アクティブにしないでください OS の介入なしコンテキスト ローミングの状態が、指定された条件を満たしていない場合。 モデムは、パートナーをサポートしていませんし、すべてのパートナーの構成の場合は、同等として扱う必要があるホームにします。

| 型 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextRoamingControlHomeOnly | 0 | コンテキストは、ホーム ネットワークで使用するかにのみ使用できるかどうかを示します。 |
| MbimMsContextRoamingControlPartnerOnly | 1 | コンテキストがパートナー ローミング ネットワークで使用するかにのみ使用できるかどうかを示します。 |
| MbimMsContextRoamingControlNonPartnerOnly | 2 | コンテキストが非パートナー ローミング ネットワークで使用するかにのみ使用できるかどうかを示します。 | 
| MbimMsContextRoamingControlHomeAndPartner | 3 | コンテキストがホーム ネットワークをローミングするパートナーで使用できるかどうかを示します。 |
| MbimMsContextRoamingControlHomeAndNonPartner | 4 | コンテキストがローミング ホームと非パートナーのネットワークで使用できるかどうかを示します。 |
| MbimMsContextRoamingControlPartnerAndNonPartner | 5 | コンテキストがパートナーおよびパートナーではないローミング ネットワークで使用できるかどうかを示します。 |
| MbimMsContextRoamingControlAllowAll | 6 | コンテキストが、ローミングの条件で使用できるかどうかを示します。 |

今後のプラットフォームでサポートされている携帯電話のコンテキストを使用または iWLAN Wi-fi オフロードとなるのかどうかを指定できる MBIM_MS_CONTEXT_MEDIA_TYPE が追加されました。 などの携帯電話としてコンテキストを設定し、モデムは、現在 Wi-fi をオフロードしする必要がありますいない接続を開始そのコンテキストを使用しています。

| 型 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextMediaTypeCellularOnly | 0 | コンテキストが移動体通信で登録されているときに使用されるのみ許可されているかどうかを示します。 |
| MbimMsContextMediaTypeWifiOnly | 1 | コンテキストが iWLAN (Wi-fi オフロード) 経由で登録されているときに使用されるのみ許可されているかどうかを示します。 |
| MbimMsContextMediaTypeAll | 2 | 携帯電話または Wifi を介して登録されているときに使用される、コンテキストが許可されているかどうかを示します。 |

MBIM_MS_CONTEXT_ENABLE では、コンテキストが有効になっているかどうかを指定します。

| 型 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextDisabled | 0 | プロビジョニングのコンテキストが無効です。 モデムには、OS 自体から、このコンテキストでアクティブ化が有効にする必要があります。 |
| MbimMsContextEnabled | 1 | プロビジョニングのコンテキストが有効になっているとします。 その他の条件が満たされる場合、コンテキストが有効にすることができます。たとえば、ローミングが許可されていない場合コンテキストする必要がありますいない有効にするローミング中に。 |

モデムのコンテキストの作成方法は、OS の可視性を提供する MBIM_MS_CONTEXT_SOURCE が追加されました。 これにより、出荷時の設定などのさまざまな状況の後に正しく動作する OS、何が保持され、さまざまな演算子の要件に基づいて既定の状態を返すべき内容かが分かるようにします。

| 型 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextSourceAdmin | 0 | コンテキストは、OS から企業の IT 管理者によって作成されました。 |
| MbimMsContextSourceUser | 1 | コンテキストは、OS の設定を使用して、ユーザーによって作成されました。 | 
| MbimMsContextSourceOperator | 2 | コンテキストは、OMA-DM またはその他のチャネルを通じて演算子によって作成されました。 |
| MbimMsContextSourceModem | 3 | コンテキストは、モデムのファームウェアに含まれていた OEM、IHV によって作成されました。 |
| MbimMsContextSourceDevice | 4 | コンテキストは、OS の APN データベースによって作成されました。 |

MBIM_MS_CONTEXT_OPERATIONS では、モデムでコンテキストを構成する実行できる操作、OS を指定します。

| 型 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextOperationDefault | 0 | 既定の操作などの追加またはモデムで既存のコンテキストを交換します。 |
| MbimMsContextOperationDelete | 1 | 削除操作では、モデムの既存のコンテキストを削除するモデムが必要です。 | 
| MbimMsContextOperationRestoreFactory | 2 | SIM の挿入を現在のプロバイダー ID のファクトリの事前構成済みのコンテキストを復元します。 置換または OS によって作成されたすべてのコンテキストは削除されを交換する必要があります。 ある場合、既定の事前構成済みなし OS コンテキスト挿入された現在の SIM プロバイダー id し、モデムでプロビジョニングされたコンテキストを削除する必要があります。 |

MBIM 1.0 から元の MBIM_CONTEXT_TYPES は引き続き有効です。 Microsoft では、MBIM 1.0 が定義されているために、コンテキストの種類が導入として、追加のコンテキストの種類を追加です。 次の表では、導入される新しい種類を定義します。 Ihv と Oem は、独自の目的で、OS によって認識できないがあるその他の一意の UUID 値をその他の独自のコンテキスト型を定義できます。

| 型 | [値] | 説明 |
| --- | --- | --- |
| MBIMMsContextTypeAdmin | 5f7e4c2e-e80b-40a9-a239-f0abcfd11f4b | コンテキストは、デバイスの管理などの管理の目的で使用されます。 |
| MBIMMSContextTypeApp | 74d88a3d-dfbd-4799-9a8c-7310a37bb2ee | コンテキストは、特定のアプリケーションのホワイト リストに登録の携帯電話会社によって使用されます。 |
| MBIMMsContextTypeXcap | 50d378a7-baa5-4a50-b872-3fe5bb463411 | IMS サービスで XCAP のプロビジョニングのコンテキストが使用されます。 |
| MBIMMsContextTypeTethering | 5e4e0601-48dc-4e2b-acb8-08b4016bbaac | モバイル ホット スポット テザリングのコンテキストが使用されます。 |
| MBIMMsContextTypeEmergencyCalling | 5f41adb8-204e-4d31-9da8-b3c970e360f2 | IMS 緊急通話にコンテキストが使用されます。 |

##### <a name="response"></a>応答

次の MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 構造、InformationBuffer で使用されます。

| Offset | サイズ | フィールド | 型 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | 後に、DataBuffer にカウントの MBIM_MS_CONTEXT_V2 構造体。 |
| 4 | 8 * EC | MsProvisionedContextV2RefList | OL_PAIR_LIST | ペアの最初の要素は、4 バイトのオフセット (バイト単位) (詳細についてを参照してください、MBIM_MS_CONTEXT_V2 テーブル) の MBIM_MS_CONTEXT_V2 構造体をこの MBIM_MS_PROVISIONED_CONTEXTS_INFO_V2 構造体の先頭 (オフセット 0) から計算されます。 ペアの 2 番目の要素は、対応する MBIM_MS_CONTEXT_V2 構造へのポインターのサイズが 4 バイトです。 |
| 4 + 8 * EC |  | DataBuffer | DATABUFFER | MBIM_MS_CONTEXT_V2 structuers の配列。 |

MBIM_MS_CONTEXT_V2、前の表では、使用は、特定のコンテキストに関する情報を提供します。


| Offset | サイズ |       フィールド        |              型               |                                                                                                                                                                                                                                                                                                 説明                                                                                                                                                                                                                                                                                                  |
|--------|------|--------------------|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |     ContextId      |             UINT32              |                                                                                                                                                                                                                                                                                        このコンテキストの一意の ID。                                                                                                                                                                                                                                                                                         |
|   4    |  16  |    ContextType     |       MBIM_CONTEXT_TYPES        |                                                                                                                                                      表される; コンテキストの種類を指定しますインターネット接続、VPN (企業ネットワークに接続)、またはボイス オーバー IP など (VOIP)。 デバイスは、空またはプロビジョニングされていないコンテキスト MBIMContextTypeNone を指定する必要があります。 詳細については、MBIM_CONTEXT_TYPES テーブルを参照してください。                                                                                                                                                       |
|   20   |  4   |       IPType       |      MBIM_CONTEXT_IP_TYPES      |                                                                                                                                                                                                                                                                         詳細については、MBIM_CONTEXT_IP_TYPES テーブルを参照してください。                                                                                                                                                                                                                                                                          |
|   24   |  4   |       Enable       |     MBIM_MS_CONTEXT_ENABLE      |                                                                                                                                                                   コンテキスト、モデムで使用できるかどうかを指定します。 MbimMsContextDisabled に設定されている場合、ネットワークに通知せず、コンテキストに一致するすべての OS 接続要求を失敗する必要があります。 詳細については、MBIM_MS_CONTEXT_ENABLE テーブルを参照してください。                                                                                                                                                                    |
|   28   |  4   |      Roaming       | MBIM_MS_CONTEXT_ROAMING_CONTROL |                                                                                                                                                                                                                                      このコンテキストではなくまたはローミングが許可されているかどうかを指定します。 詳細については、MBIM_MS_CONTEXT_ROAMING_CONTROL テーブルを参照してください。                                                                                                                                                                                                                                      |
|   32   |  4   |     MediaType      |   MBIM_MS_CONTEXT_MEDIA_TYPE    |                                                                                                                                                                                                                                       コンテキストでの使用は、メディアの輸送の種類を指定します。 詳細については、MBIM_MS_CONTEXT_MEDIA_TYPE テーブルを参照してください。                                                                                                                                                                                                                                        |
|   36   |  4   |       ソース       |     MBIM_MS_CONTEXT_SOURCE      |                                                                                                                                                                                                                                                  コンテキストの作成のソースを指定します。 詳細については、MBIM_MS_CONTEXT_SOURCE テーブルを参照してください。                                                                                                                                                                                                                                                   |
|   40   |  4   | AccessStringOffset |             オフセット              | 文字列、AccessString、ネットワークにアクセスするデータ バッファーのオフセットします。 GSM ベースのネットワークでは、"data.thephone company.com"など、アクセス ポイント名 (APN) 文字列になります。 CDMA ベースのネットワークでは、これがあります「#777」またはネットワーク アクセスの識別子 (NAI) などの特殊なダイヤル コードなど"foo@thephone-company.com"。 このメンバーには、APN の既定のネットワークを割り当てることを要求する、NULL を指定できます。 注:すべてのネットワークは、ため、無効な APN によって発生した接続エラー、考えられる結果のこの NULL APN 規則をサポートします。 文字列のサイズは 100 文字を超えない必要があります。 |
|   44   |  4   |  AccessStringSize  |          SIZE(0..200)           |                                                                                                                                                                                                                                                                                         AccessString に使用するサイズ。                                                                                                                                                                                                                                                                                          |
|   48   |  4   |   UserNameOffset   |             オフセット              |                                                                                                                                                                                                                       計算される、この構造体の先頭から、ユーザー名、認証するユーザー名を表す文字列へのバイト オフセットします。 このメンバーは、NULL を指定できます。                                                                                                                                                                                                                        |
|   52   |  4   |    UserNameSize    |          SIZE(0..510)           |                                                                                                                                                                                                                                                                                           規模のユーザー名に使用します。                                                                                                                                                                                                                                                                                           |
|   56   |  4   |   PasswordOffset   |             オフセット              |                                                                                                                                                                                                                          ユーザー名のパスワードを表すオフセット (バイト)、文字列、パスワードに、この構造体の先頭から計算されます。 このメンバーは、NULL を指定できます。                                                                                                                                                                                                                          |
|   60   |  4   |    PasswordSize    |          SIZE(0..510)           |                                                                                                                                                                                                                                                                                           パスワードを使用するサイズ。                                                                                                                                                                                                                                                                                            |
|   64   |  4   |    圧縮     |        MBIM_COMPRESSION         |                                                                                                                                                                        ヘッダーとデータのデータ接続に使用する圧縮形式を指定します。 このメンバーは、GSM ベースのデバイスにのみ適用されます。 ホストは、CDMA ベースのデバイス、MBIMCompressionNone にこのメンバーを設定します。 詳細については、MBIM_COMPRESSION テーブルを参照してください。                                                                                                                                                                        |
|   68   |  4   |    AuthProtocol    |       MBIM_AUTH_PROTOCOL        |                                                                                                                                                                                                                                                  PDP ライセンス認証を使用する認証の種類。 詳細については、MBIM_AUTH_PROTOCOL テーブルを参照してください。                                                                                                                                                                                                                                                  |
|   72   |      |     DataBuffer     |           DATABUFFER            |                                                                                                                                                                                                                                                                     AccessString、UserName、およびパスワードを格納しているデータ バッファー。                                                                                                                                                                                                                                                                      |

##### <a name="notification"></a>Notification

詳細については、MBIM_MS_PROVISIONED_CONTEXT_V2 テーブルを参照してください。

#### <a name="status-codes"></a>状態コード

クエリおよびセットの操作。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | デバイスがプロビジョニングされているコンテキストを取得できなかったため、操作が失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスは、操作をサポートしていないため、操作が失敗しました。 |

セット操作の場合のみ。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーターのため、操作が失敗しました。 |
| MBIM_STATUS_WRITE_FAILURE | 更新の要求が成功した操作が失敗しました。 |


