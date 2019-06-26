---
title: Wi-Fi Direct 印刷の実装
description: Wi-Fi Direct 印刷の実装のデバイスの要件についてを説明します。
ms.assetid: 03266F8F-4C91-49E7-9CAF-2D08AF5E3E18
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 16381bee107e988684373adb4b147d27634f98cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387186"
---
# <a name="wi-fi-direct-printing-implementation"></a>Wi-Fi Direct 印刷の実装


## <a name="device-requirements"></a>デバイスの要件


」の説明に従って、シームレスな接続エクスペリエンスを取得する WFD WSD デバイスを[Wi-Fi Direct 印刷の概要](wfd-overview.md)、デバイスが、次の要件に準拠するには。

-   デバイスが垂直方向のペアをサポートし、WPS メッセージ ("を実装する垂直ペアリング データ Blob"以下で説明されている形式) で関連する DPWS (WSD) データを送信する必要があります。
-   すべての論理デバイスを物理デバイスでは、PNP-X 対応の拡張機能内 PNP-X 対応のコンテナーと同じ ID を使用する必要があります。
    -   PNP-X 対応のコンテナーの Id のネットワーク接続されているデバイスの実装の詳細については、次を参照してください。[コンテナー Id の概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-container-ids)します。
    -   PNP-X 対応の拡張機能の概要については、次を参照してください、 [PnP-x:。プラグ アンド プレイ Extensions for Windows 仕様](https://docs.microsoft.com/previous-versions/gg463082(v=msdn.10))します。

WFD コンテナー ID は、プリンターの UUID を照合するため、PNP-X 対応のコンテナーの ID は、デバイスのメタデータでは必要ありません。 ただし、デバイスがデバイス メタデータを PNP-X 対応のメタデータをサポートし、PNP-X 対応のコンテナー ID をデバイスのメタデータで PNP-X 対応のメタデータの一部として提供することをまだお勧めします。 このコンテナーの ID が、WFD コンテナーの ID と一致する必要があります。

WFD レイヤーと WSD のレイヤーで同じコンテナー ID を持つことにより、次の。

-   ペアリングの UI では、複数の論理デバイスが 1 つの物理デバイスで共存させるしより論理的でユーザーのペアリング処理など、デバイスを追加ウィザードを理解することができます。 (例: ユーザーが持っていない WFD と別の操作で手動での印刷デバイスをペアリングします。)
-   デバイスとプリンターは、(WFD devnode の 1 つのセット) と 1 つの WSD devnode 一連のシステムにインストールされている devnode の 2 つのセットがある場合でも、デバイスの 1 つのデバイスのアイコンを表示することができます。
-   その適切なコンテナー ID の実装が正常に実行する Windows ハードウェア認定キット テストに必要なに注意してください。 不適切な実装には、各論理デバイスを別の物理デバイスとして認識するテストが発生します。

WFD WSD デバイスは、上記の要件に準拠していませんが、これらのデバイスにこの実装で説明されている接続性は適用されません。

デバイスがで指定されている永続的なグループと同時実行の接続-複数のグループを実装する必要があります、 [Wi-fi Alliance - Wi-Fi Direct 業界に関するホワイト ペーパー](https://go.microsoft.com/fwlink/p/?LinkId=784967)します。

## <a name="how-to-publish-container-uuid-over-wi-fi-direct-for-printers"></a>プリンターの Wi-Fi Direct 経由で UUID のコンテナーを発行する方法


Windows Wi-fi Alliance"Wi Fi ピア-ツー ピア (P2P) Specification v1.1"あたりの要求/プローブ応答を使用して Wi-Fi Direct 経由でプリンターを検出するセクション 3.1.2.1.2 (スキャン フェーズ)。 デバイス、プリンターここでは、返信、適切なプローブ要求/応答フレームを使用して PC に。

カスタム i を使用して、両方のプローブ要求とプローブ応答フレームを拡張できます。 Microsoft では、さまざまな拡張機能を有効にするいくつかの属性を持つカスタム IE を定義します。

**Microsoft の 802.11 カスタム IE を構築する方法**

カスタム IE は、ベンダーの ID と仕入先データで構成されます。

![wfd ベンダー拡張機能](images/wfd-customie.png)

*WFD ベンダー拡張機能*

Microsoft では、仕入先 ID 0x137 を使用して、Microsoft によって所有されている IEs を表します。 各仕入先のベンダー拡張機能内にある仕入先データ ブロックには、仕入先を定義するデータの任意のブロックが含まれています。 仕入先データは、Microsoft のベンダー拡張機能から成る 1 つまたは複数の型の値の長さ (TLV) 構造体のブロックします。 TLV 構造体の組織は、図の下に表示されます。

![wfd 仕入先データ](images/wfd-vendordatatlv.png)

*WFD 仕入先データ*

**コンテナーの UUID の TLV 定義**

含まれる ID に関連する 2 つの TLVs があります。 デバイスには、その Windows 送信「属性の要求」があるし、"コンテナーの UUID"で、デバイスが応答 TLV があります。

定義:

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>名前/説明</th>
<th>型 (2 バイト)</th>
<th>長さ (2 バイト)</th>
<th>(長さによって定義された) 値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>(これは送信要求プローブで PC が探索時に) Microsoft 属性の要求</p></td>
<td><p>0x1005</p></td>
<td><p>0x0002</p></td>
<td><p>0x0001 = Microsoft が含まれている UUID を要求します。</p></td>
</tr>
<tr class="even">
<td><p>コンテナーの UUID (これは、プリンターで送信番目のプローブ応答探索中に)</p></td>
<td><p>0x1006</p></td>
<td><p>0x0010</p></td>
<td><p>プリンターで定義するには</p></td>
</tr>
</tbody>
</table>

 

## <a name="implementing-vertical-pairing-data-blob"></a>ペアリングの垂直方向のデータ Blob を実装します。


垂直方向のペアのデータ Blob は、pc で、プリンターに接続する前に、WSD 印刷サービスを理解できます。 このメカニズムは Wi-Fi Direct のサービスの discovery 仕様が書き込まれる前に実装されているサービスの検出の単純な代替です。

コンテナー UUID のようにペアリングの垂直方向のデータ Blob も Microsoft IE の属性です。 コンテナー ID 属性とは異なりこのする必要がありますでパブリッシュするか M7/M8 WPS メッセージ (Wi-Fi Direct ペアリング) 中の役割に応じてデバイスから。

**Microsoft の 802.11 カスタム IE を構築する方法**

カスタム IE は、ベンダーの ID と仕入先データで構成されます。

![wfd ベンダー拡張機能](images/wfd-customie.png)

*WFD ベンダー拡張機能*

Microsoft では、仕入先 ID 0x137 を使用して、Microsoft によって所有されている IEs を表します。 各仕入先のベンダー拡張機能内にある仕入先データ ブロックには、仕入先を定義するデータの任意のブロックが含まれています。 仕入先データは、Microsoft のベンダー拡張機能から成る 1 つまたは複数の型の値の長さ (TLV) 構造体のブロックします。 TLV 構造体の組織は、次の図に示されます。

![wfd 仕入先データ](images/wfd-vendordatatlv.png)

*WFD 仕入先データ*

**垂直方向のペアの Blob の TLV 定義**

垂直方向のペアリングを Rally の 2 つの特定 TLV 型が定義されます。 これらの TLV 型は、次の表に一覧表示されます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>名前/説明</th>
<th>型 (2 バイト)</th>
<th>長さ (2 バイト)</th>
<th>(長さによって定義された) 値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>垂直方向のペアの識別子 (デバイスの内部のトポロジは、通信)</p></td>
<td><p>0x1001</p></td>
<td><p>0x0002</p></td>
<td><p>以下は、"垂直方向のペアリング識別子 TLV"を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>トランスポート UUID (デバイスのトランスポート UUID 値)</p></td>
<td><p>0x1002</p></td>
<td><p>0x0010</p></td>
<td><p>上記の「UUID のコンテナーの TLV 定義」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

*垂直 TLVs のペアリングを rally*
**識別子 TLV の垂直方向のペアリング**

垂直方向のペアリング識別子 (VPI) TLV は、Windows がデバイスのサービスと通信する方法を指定します。 デバイスの内部トポロジを通信します。 垂直方向のペアは、デバイスでは実装されていない場合でも、垂直方向のペアリングを Rally 拡張機能をサポートするために少なくとも 1 つ VPI が必要です。 このような状況で、VPI はトランスポートが使用しないことを指定します。 VPI TLV は、WPS M1 メッセージで Microsoft のベンダー拡張機能の一部として送信する必要があります。

VPI TLV に含まれているデータは 2 バイト長であり、2 つの異なるフィールドで構成されます。 トランスポート フィールドとプロファイル要求フィールド、(各フィールドは 1 バイト長) 次の図のようにします。

![vpi tlv に含まれている wfd データ](images/wfd-vpi.png)

*VPI TLV に含まれている WFD データ*

**VPI トランスポート フィールド**

トランスポート フィールドには、Windows は、デバイスとの通信に使用できるトランスポートを指定します。 VPI ごとに 1 つだけのトランスポートを指定できます。 デバイスは、PNP-X 対応の複数のトランスポートをサポートする場合に、Microsoft のベンダー拡張機能 (1 つの各トランスポートの) 複数の VPI TLVs を含めることでこの通信できます。 VPI トランスポート フィールドの有効な値は、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>[値]</th>
<th>[トランスポート]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>0x01</p></td>
<td><p>DPWS</p></td>
</tr>
<tr class="odd">
<td><p>0x02</p></td>
<td><p>UPnP</p></td>
</tr>
<tr class="even">
<td><p>0x03</p></td>
<td><p>セキュリティで保護された DPWS</p></td>
</tr>
<tr class="odd">
<td><p>0x04-0 xff の場合</p></td>
<td><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

*VPI トランスポート フィールドの値*

**注**  Windows 7 は、両方は必要ありませんが、DPWS (0x01) または Secure DPWS (0x03) のサポートを提供します。

 

**注**  デバイスが垂直方向のペアリングを Rally を実装していない場合は、0x00 (なし) のトランスポート値を持つ 1 つだけ VPI が指定する必要があります。 このような状況で、デバイスでは、トランスポートの UUID TLV は指定しないでください。 デバイスとペアリングする期待する必要がありますいないを Windows に通知します。 したがって、Windows は、事前がデバイスの Wi-fi 設定を構成する間に、デバイスとペアリングには試行されません。

 

**VPI プロファイル要求 フィールド**

VPI は WPS プロトコルを使用して、デバイスのサービスをプロビジョニングするデバイスを使用できます。 このような状況で、Windows その情報を送信、サービスを構成するデバイスのサービスを要求できます。 この情報は、プロファイルと呼ばれます。 VPI の 2 番目のフィールドでは、デバイスが、Windows 送信プロファイルを要求するかどうかを指定します。 VPI プロファイル要求 フィールドの有効な値は、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x01</p></td>
<td><p>Wi-fi プロファイルが要求されました。 これは、Windows 7 で現在サポートされている唯一の値です。</p></td>
</tr>
<tr class="even">
<td><p>0x00, 0x02 – 0 xff の場合</p></td>
<td><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

*VPI プロファイル要求 フィールドの値*

**注**  0x00 のフィールドの値を VPI プロファイル要求では、Windows 7 で現在サポートされていないために予約されていると見なされます。 VPI プロファイル要求 フィールドは 0x01 (Wi-fi プロファイルの要求) の値にのみ設定する必要があります、トランスポートの場合であっても 0x00 (なし) の値が指定されています。

 

**トランスポート UUID TLV**

トランスポートの UUID TLV は、特定のトランスポートを使用している (DPWS または UPnP) に WPS UUID と異なる基本 UUID 値を指定します。 トランスポートの UUID TLV は省略可能です。 トランスポートの UUID TLV が含まれていない場合、WPS UUID は、指定されたトランスポートの id を形成に使用されます。

トランスポートの UUID TLV が含まれる場合は、トランスポートを識別する VPI TLV の直後に、必要があります。 1 つ以上の VPI TLV が含まれる場合は、トランスポートの UUID TLV できます各 VPI TLV 後。

**注**  トランスポート UUID TLV データ値がネットワークのバイト順である必要があります。

 

**注**  デバイスは、0x00 (なし) の VPI トランスポートの値を指定する場合もトランスポート UUID の TLV が含まれません。

 

## <a name="wps-example"></a>WPS 例


この例では、プリンター デバイスが DPWS を使用し、WS 印刷インターフェイスを実装するいると仮定します。 デバイスは、次の表で UUID 値を使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>サービス</th>
<th>同一。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WPS</p></td>
<td><p>ec742c0d-5915-4bcb-b969-008132afec5e</p></td>
</tr>
<tr class="even">
<td><p>DPWS 印刷</p></td>
<td><p>urn:uuid:00010203-0405-0607-0809-0a0b0c0e0e0f</p></td>
</tr>
</tbody>
</table>

 

*WPS 例: UUID の値をサービス*

**注**  UUID の値はすべて小文字で指定し、DPWS id の文字列形式の urn: uuid:uuid を使用して\_値。

 

**注**  この例では、UUID 値は、架空のものし、実際のデバイスでは使用する必要があります。

 

デバイスは、その WPS M7/M8 メッセージを送信するとき、次の図に表示される Microsoft のベンダー拡張機能が含まれています。

![例 wfd ベンダー拡張機能の詳細](images/wfd-vendorextensiondetails.png)

*例 WFD ベンダー拡張機能の詳細*

この例では、ベンダー拡張機能には、0x137 で、Microsoft のベンダー拡張機能として識別のベンダー ID 値が含まれています。 ベンダ拡張の仕入先データ フィールド内で、2 つの TLV 構造です。

最初の TLV は、0x1001、として、VPI TLV を識別するの型の値を持ちます。 最初の TLV 内のデータの長さは 0x0101 の値を含む 2 バイトです。 これは、デバイスが DPWS トランスポート (0x01) をサポートしていると、プロファイル (0x01) を要求していることを指定します。

2 番目の TLV は、トランスポート UUID として TLV を識別する、0x1002 の型値を持ちます。 2 番目の TLV 内のデータの長さは、UUID 値 00010203-0405-0607-0809-0a0b0c0e0e0f のバイナリ バージョンが含まれている 16 バイトです。

顧客は、垂直方向にプリンターをペア、ときに Windows をデバイスの Wi-fi ラジオ適切な設定で最初に構成します。 また、UUID 値の指定されたトランスポートを使用して、DPWS デバイスしペアします。

デバイスが Wi-fi ネットワークに接続するし、その DPWS サービスを発表、Windows は PnP デバイスの適切なノードを作成およびインストールし、適切なドライバーを読み込みます。

 

 




