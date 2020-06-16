---
title: Wi-fi Direct 印刷の実装
description: Wi-fi Direct 印刷実装のデバイス要件について説明します。
ms.assetid: 03266F8F-4C91-49E7-9CAF-2D08AF5E3E18
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: e1ced3a6dbd2f9371aac25c37f3992448c1b7f5a
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793750"
---
# <a name="wi-fi-direct-printing-implementation"></a>Wi-fi Direct 印刷の実装

## <a name="device-requirements"></a>デバイスの要件

「 [Wi-fi Direct 印刷の概要](wfd-overview.md)」で説明されているように、デバイスがシームレスな接続性を実現するには、デバイスが次の要件を満たしている必要があります。

- デバイスは、縦方向のペアリングをサポートし、関連する DPWS (WSD) データを WPS メッセージに送信する必要があります (以下の「垂直方向のペアリングデータ Blob の実装」で説明されている形式)。

- 物理デバイス内のすべての論理デバイスは、PnP-X 拡張機能で同じ Pnp-x コンテナー ID を使用する必要があります。

  - ネットワークに接続されたデバイスの PnP X コンテナー Id の実装の詳細については、「[コンテナー id の概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-container-ids)」を参照してください。

  - PnP X の拡張機能に関する一般的な情報については、「 [pnp-x: プラグアンドプレイ extensions For Windows Specification](https://docs.microsoft.com/previous-versions/gg463082(v=msdn.10))」を参照してください。

WFD コンテナー ID はプリンターの UUID と一致するので、デバイスメタデータには、PnP X コンテナー ID は必要ありません。 ただし、デバイスがデバイスメタデータ内の PnP-X メタデータをサポートし、デバイスメタデータの Pnp-x メタデータの一部として Pnp-x コンテナー ID を提供することをお勧めします。 このコンテナー ID は、WFD コンテナー ID と一致している必要があります。

WFD レイヤーおよび WSD レイヤーで同じコンテナー ID を持つと、次のことが保証されます。

- デバイスの追加ウィザードなどの組み合わせ UI を使用すると、複数の論理デバイスが1つの物理デバイスに共存していることを認識し、より論理的な方法でペアリングを処理することができます。 (たとえば、ユーザーが別の操作で WFD デバイスと印刷デバイスを手動でペアリングする必要はありません)。

- 2つの devnodes がシステムにインストールされている場合でも、デバイス & プリンターでは、デバイスの1つのデバイスアイコンを表示できます (1 セットの WFD devnodes と1セットの WSD devnodes)。

- Windows ハードウェア認定キットのテストを正しく実行するには、適切なコンテナー ID を実装する必要があることに注意してください。 不適切な実装の場合、テストでは各論理デバイスが個別の物理デバイスとして認識されます。

WFD WSD デバイスが上記の要件に準拠していない場合、この実装で説明されている接続エクスペリエンスは、これらのデバイスに適用されません。

デバイスは、wi-fi[アライアンス-Wi-fi Direct 業界のホワイトペーパー](https://www.wi-fi.org)に記載されているように、永続的なグループと同時接続を実装する必要があります。

## <a name="how-to-publish-container-uuid-over-wi-fi-direct-for-printers"></a>プリンター用の Wi-fi ダイレクトを使用してコンテナーの UUID を公開する方法

Windows では、wi-fi アライアンス "Wi-fi ピアツーピア (P2P) Specification v1.1" セクション 3.1.2.1.2 (スキャンフェーズ) ごとに、プローブ要求/応答を使用して Wi-fi ダイレクトでプリンタを検出します。 デバイス (この場合は Printer) は、適切なプローブ要求/応答フレームを使用して PC に応答します。

プローブ要求 & プローブ応答フレームは、どちらもカスタムを使用して拡張できます。 Microsoft では、さまざまな拡張機能を有効にするために、いくつかの属性を持つカスタム IE を定義しています。

### <a name="how-to-construct-a-microsoft-80211-custom-ie-for-container-uuid"></a>コンテナー UUID 用の Microsoft 802.11 カスタム IE を構築する方法

カスタム IE は、次の WFD ベンダ拡張機能の図に示すように、ベンダー ID & ベンダデータで構成されています。

![wfd ベンダ拡張機能](images/wfd-customie.png)

Microsoft は、ベンダー ID 0x137 を使用して、Microsoft が所有しているものを表します。 各ベンダーのベンダーの拡張機能に含まれるベンダーデータブロックには、ベンダーが定義する任意のデータブロックが含まれています。 Microsoft ベンダ拡張機能のベンダーデータブロックは、1つまたは複数の型の長さの値 (TLV) 構造で構成されています。 TLV 構造体の編成については、次の*WFD ベンダデータ*の図を参照してください。

![wfd ベンダデータ](images/wfd-vendordatatlv.png)

### <a name="tlv-definition-for-container-uuid"></a>コンテナー UUID の TLV 定義

含まれている ID に関連する TLVs が2つあります。 Windows が & デバイスに送信する "属性の要求" には、デバイスが応答する "コンテナー UUID" TLV があります。

定義:

| 名前/説明 | 型 (2 バイト) | 長さ (2 バイト) | 値 (長さで定義) |
|--|--|--|--|
| Microsoft 属性 (検出中にプローブ要求で PC によって送信されます) の要求 | 0x1005 | 0x0002 | 0x0001 = Microsoft は含まれている UUID を要求しています |
| コンテナー UUID (検出中にプローブ応答でプリンタによって送信されます) | 0x1006 | 0x0010 | プリンターで定義するには |

## <a name="implementing-vertical-pairing-data-blob"></a>垂直方向のペアリングデータ Blob の実装

垂直方向のペアリングデータ Blob を使用すると、PC はプリンターに接続する前に WSD 印刷サービスを理解できます。 このメカニズムは、Wi-fi Direct のサービス検出仕様が書き込まれる前に実装された、サービス検索の簡単な代替手段です。

コンテナー UUID と同様に、垂直ペアリングデータ Blob も Microsoft IE の属性です。 コンテナー ID 属性とは異なり、この属性は、その役割に応じて、デバイスから M7/M8 WPS メッセージ (Wi-fi Direct ペアリング中) に発行する必要があります。

### <a name="how-to-construct-a-microsoft-80211-custom-ie-for-vertical-pairing"></a>垂直方向のペアリング用に Microsoft 802.11 カスタム IE を構築する方法

カスタム IE は、次の WFD ベンダ拡張機能の図に示すように、ベンダー ID & ベンダデータで構成されています。

![wfd ベンダ拡張機能](images/wfd-customie.png)

Microsoft は、ベンダー ID 0x137 を使用して、Microsoft が所有しているものを表します。 各ベンダーのベンダーの拡張機能に含まれるベンダーデータブロックには、ベンダーが定義する任意のデータブロックが含まれています。 Microsoft ベンダ拡張機能のベンダーデータブロックは、1つまたは複数の型の長さの値 (TLV) 構造で構成されています。 TLV 構造体の編成については、次の WFD ベンダデータの図を参照してください。

![wfd ベンダデータ](images/wfd-vendordatatlv.png)

### <a name="tlv-definition-for-vertical-pairing-blob"></a>垂直方向のペアリング Blob の TLV 定義

2つの特定の TLV の種類が、集結の垂直方向のペアリング用に定義されています。 これらの TLV の種類を次の表に示します。

| 名前/説明 | 型 (2 バイト) | 長さ (2 バイト) | 値 (長さで定義) |
|--|--|--|--|
| 垂直方向のペアリング識別子 (デバイスの内部トポロジを通信します) | 0x1001 | 0x0002 | 下の「垂直方向のペアリング識別子 TLV」を参照してください。 |
| トランスポート UUID (デバイスのトランスポート UUID 値) | 0x1002 | 0x0010 | 上の「コンテナー UUID の TLV 定義」を参照してください。 |

### <a name="vertical-pairing-identifier-tlv"></a>垂直方向のペアリング識別子 TLV

TLV は、デバイスの内部トポロジを通信します。これは、Windows がデバイスのサービスと通信する方法を指定します。 デバイスに垂直方向のペアリングが実装されていない場合でも、1つ以上の VPI が集結方向のペアリング拡張機能をサポートするために必要です。 このような状況では、VPI はトランスポートが使用されないことを指定します。 VPI TLV は、WPS M1 メッセージで Microsoft ベンダ拡張機能の一部として送信される必要があります。

VPI TLV に含まれるデータは2バイト長で、次の2つのフィールドで構成されています。これは、VPI TLV に含まれる WFD データの次の図に示すように、トランスポートフィールドとプロファイル要求フィールドです (各フィールドは1バイト長です)。

![vpi tlv に含まれる wfd データ](images/wfd-vpi.png)

### <a name="vpi-transport-field"></a>VPI TRANSPORT フィールド

トランスポートフィールドは、Windows がデバイスとの通信に使用できるトランスポートを指定します。 各 VPI に指定できるトランスポートは1つだけです。 デバイスが複数の PnP-X トランスポートをサポートしている場合は、Microsoft ベンダ拡張機能に複数の VPI TLVs (トランスポートごとに1つ) を含めることで、このような通信を行うことができます。 次の表に、"VPI Transport" フィールドの有効な値を示します。

| 値 | トランスポート |
|--|--|
| 0x00 | None |
| 0x01 | DPWS |
| 0x02 | UPnP |
| 0x03 | セキュリティで保護された DPWS |
| 0x04 ~ 0xFF | 予約されています。 |

> [!NOTE]
> Windows 7 では DPWS (0x01) またはセキュア DPWS (0x03) がサポートされていますが、両方はサポートされていません。

デバイスが集結垂直ペアリングを実装していない場合、トランスポート値が 0x00 (なし) の VPI を1つだけ指定する必要があります。 このような状況では、デバイスでトランスポート UUID TLV を指定しないでください。 これは、デバイスとのペアリングを想定していないことを Windows に通知します。 そのため、デバイスの Wi-fi 設定を構成するときに、Windows はデバイスとの事前ペアリングを試行しません。

### <a name="vpi-profile-request-field"></a>VPI PROFILE 要求フィールド

VPI は、デバイスが WPS プロトコルを使用してデバイスのサービスをプロビジョニングできるようにします。 このような状況では、デバイスサービスは、サービスを構成するために Windows に情報を送信するように要求できます。 この情報は、プロファイルと呼ばれます。 VPI の2番目のフィールドは、デバイスが Windows にプロファイルを送信するように要求しているかどうかを指定します。 次の表に、[VPI Profile 要求] フィールドの有効な値を示します。

| 値 | 説明 |
|--|--|
| 0x01 | Wi-fi プロファイルが要求されました。 これは、現在 Windows 7 でサポートされている唯一の値です。 |
| 0x00、0x02 –0xFF | 予約されています。 |

現在 Windows 7 ではサポートされていないため、VPI Profile 要求フィールドの値0x00 は予約済みと見なされます。 トランスポートに値 0x00 (none) が指定されている場合でも、VPI Profile 要求フィールドは、0x01 (Wi-fi プロファイルが要求される) 値にのみ設定する必要があります。

### <a name="transport-uuid-tlv"></a>トランスポート UUID TLV

トランスポート UUID TLV は、特定のトランスポート (DPWS または UPnP) が、WPS UUID とは異なるベース UUID 値を持つことを指定します。 トランスポート UUID TLV は省略可能です。 トランスポート UUID TLV が含まれていない場合、指定されたトランスポートの id を形成するために、WPS UUID が使用されます。

トランスポート UUID TLV が含まれている場合は、トランスポートを識別する VPI TLV の直後にある必要があります。 複数の VPI TLV が含まれている場合は、各 VPI TLV の後にトランスポート UUID TLV を含めることができます。

トランスポート UUID TLV のデータ値は、ネットワークのバイト順にする必要があります。

デバイスで、VPI Transport 値 0x00 (none) が指定されている場合、トランスポート UUID TLV を含めないでください。

## <a name="wps-example"></a>WPS の例

この例では、プリンターデバイスが DPWS を使用し、WS Print インターフェイスを実装しているものとします。 デバイスは、次の表に示す UUID 値を使用します。

| サービス | ID |
|--|--|
| WPS | ec742c0d-5915-4bcb-b969-008132afec5e |
| DPWS 印刷 | urn: uuid: 00010203-0405-0607-0809-0a0b0c0e0e0f |

### <a name="wps-exampleservice-uuid-values"></a>WPS の例—サービス UUID の値

UUID 値はすべて小文字で指定され、DPWS id 文字列は urn: uuid: uuid 値の形式を使用し \_ ます。

> [!NOTE]
> この例の UUID 値は架空のものであり、実際のデバイスでは使用できません。

デバイスが WPS M7/M8 メッセージを送信すると、次の WFD ベンダ拡張機能の詳細の例に示されている Microsoft ベンダーの拡張機能が含まれます。

![wfd ベンダ拡張機能の詳細の例](images/wfd-vendorextensiondetails.png)

この例では、vendor 拡張機能にベンダー ID 値0x137 が含まれています。これにより、Microsoft vendor 拡張機能として識別されます。 Vendor 拡張機能の vendor データフィールド内には、2つの TLV 構造体があります。

最初の TLV の Type 値は0x1001 で、TLV は VPI として識別されます。 最初の TLV のデータの長さは2バイトで、値0x0101 を含みます。 これは、デバイスが DPWS transport (0x01) をサポートし、プロファイルを要求している (0x01) ことを指定します。

2番目の TLV の Type 値は0x1002 で、TLV はトランスポート UUID として識別されます。 2番目の TLV のデータの長さは16バイトであり、これには UUID 値00010203-0405-0607-0809-0a0b0c0e0e0f のバイナリバージョンが含まれています。

顧客がプリンターを縦に組み合わせている場合、Windows はまず、適切な設定を使用してデバイスの Wi-fi ラジオを構成します。 次に、指定されたトランスポート UUID 値を使用して、デバイスの DPWS デバイスをペアリングします。

デバイスが Wi-fi ネットワークに接続し、その DPWS サービスを発表すると、Windows は適切な PnP デバイスノードを作成し、適切なドライバーをインストールして読み込みます。
