---
title: Wi-Fi Direct ペアリングの実装
description: このセクションでは、周辺機器が Tap および Setup に参加するための設計ガイドラインと要件と、ユースケースをタップして再接続するための要件について説明します。
ms.assetid: 1B729E9F-DF9F-4263-9F0B-5EDCF817D2C3
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32ef59d8f1013ae8940386ed3042e29473eea3f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840472"
---
# <a name="wi-fi-direct-pairing-implementation"></a>Wi-Fi Direct ペアリングの実装


このセクションでは、周辺機器が Tap および Setup に参加するための設計ガイドラインと要件と、ユースケースをタップして再接続するための要件について説明します。

このトピックで説明されているペアリングの実装は、現在 Windows 8.1 でサポートされています。これは、プリンターデバイスへのペアリングのみを対象としています **。  **

 

**注**  Windows 10 では、wi-fi アライアンスの Wi-fi P2P キャリア構成レコードを通過する wi-fi ダイレクト静的接続への NFC もサポートしています。 詳細については、「 [Wi-fi アライアンス](https://www.wi-fi.org/)」を参照してください。

 

## <a name="peripheral-wi-fi-direct-device-pairing"></a>周辺機器の Wi-fi ダイレクトデバイスのペアリング


タップ中に、NFP は接続しているデバイスからペアリング情報を受け取ります。 NFP Windows にペアリング情報を渡します。 Wi-fi Direct デバイスは、Wi-fi アライアンスの帯域外 (OOB) ペアリングの手順と NFC フォーラムの推奨事項に従います。 Windows は、以下で定義されている独自のペアリングメッセージに依存しています。

Windows はユーザーに同意を求めるメッセージを表示します。指定されている場合、Windows は、各アドレスが成功するまで順番に接続を試みます。 PC の NFP プロバイダーと接続しているデバイスとの間では、これ以上の操作はありません。

例として NFC を使用すると、一方向のインストールは、ペアリング情報を静的またはパッシブな NFC タグに格納することによって実現されます (静的エミュレーションモードでアクティブな NFC タグを使用することもできます)。 Windows はこのペアリング情報をサブスクライブします。 PC 上の NFC 対応の NFP プロバイダーは、タグから接続情報を受け取り、これを Windows にサブスクライバーとして渡します。 Windows は、接続情報を受信すると、デバイスクラス固有の手法を使用して、デバイスの実際のインストールを帯域内で実行します。

## <a name="interoperability-requirements"></a>相互運用性の要件


NFP プロバイダー間での相互運用性を確保するために、ペアリング情報はプロバイダー固有のメッセージ形式でカプセル化する必要があります。

このドキュメントの他の部分で説明したように、NFC 対応の NFP プロバイダー以外の近接テクノロジについては、特定の要件はありません。

Windows では、特定の NFC フォーラムをサポートするために、一方向のペアリングのために Wi-fi Direct OOB のペアリング情報を伝達するために、NFC が有効な NFP プロバイダーを必要としています。 NDEF メッセージには、TNF フィールドの値が0x01 で、TYPE フィールドが "Hs" である最初のレコードと、Wi-fi Direct Carrier 構成レコードを指す代替の運送業者レコードが含まれています。 このメソッドでは、NDEF レコードのペイロードのみが使用されます。

## <a name="unidirectional-pairing-using-nfc-for-wi-fi-direct"></a>Wi-fi Direct の NFC を使用した一方向のペアリング


このセクションでは、NFC、Wi-fi Direct、および Windows が連携して、プリンターなどの Wi-fi ダイレクトデバイスの一方向のワイヤレスペアリングをサポートするしくみについて詳しく説明します。

### <a name="nfp-provider-references"></a>NFP プロバイダーの参照

Wi-fi Direct のペアリングは、NFC フォーラムの標準化された接続の選択メッセージの種類を使用して行います。 次の図は、Wi-fi Direct デバイスペアリング (具体的には NDEF レコード3と 4) に対して、接続転送選択メッセージがどのように適用されるかの概要を示しています。 このメッセージでは、1つまたは複数の "ac" または "代替通信事業者" レコードが記述されています。 これらのレコードは、引き渡し選択レコードに順番に従い、それぞれが適切に定義された型になります。 最後に、このメッセージには、ペアリング操作の処理方法に関する情報を Windows に提供する、Microsoft が定義したデバイスのペアリングレコードが含まれます。

![接続の引き渡し選択メッセージ](images/handover.png)

### <a name="wi-fi-direct-device-pairing-message"></a>Wi-fi Direct デバイスのペアリングメッセージ

次の例のユースケースでは、例として、NFC の種類2のタグがわかりやすい例として使用されています。 異なる NFC タグの種類を使用する必要がある場合は、そのタグ定義に従って NDEF メッセージを適切にカプセル化する必要があります。

| フィールド                 | Value                                            | 説明                                                               |
|-----------------------|--------------------------------------------------|---------------------------------------------------------------------------|
| TNF                   | 0x02                                             | 次に続く型フィールドの形式。 RFC 2046 で定義されているメディアの種類。 |
| タスクバーの検索ボックスに                  | ' application/vnd. ms-windows '             | このシナリオに対して定義する新しい型の文字列。                              |
| OOB データのサイズ      | テキスト                                             | 最大 64 KB の OOB データがサポートされています。                                        |
| Wi-fi ダイレクト OOB データ | 前のフィールドによって示されるサイズの &lt;blob&gt; | 以下で定義されている wi-fi ダイレクト OOB データ。                                   |

 

### <a name="wi-fi-direct-oob-format"></a>Wi-fi ダイレクト OOB 形式

次の表では、WiFi ダイレクト OOB データの形式について説明します。 OOB の一方向データは、任意の一方向の P2P OOB デバイスによって送信される場合があります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">属性 ID</th>
<th align="left">必須/オプション</th>
<th align="left">注意:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OOB ヘッダー</p>
<p>「OOB ヘッダー属性の形式の表」を参照してください。</p></td>
<td align="left">該当なし</td>
<td align="left">必須かどうか</td>
<td align="left">OOB ヘッダー属性は、P2P OOB データ blob 内に存在する必要があり、その OOB の種類の値は "OOB の単方向プロビジョニングデータ" に設定されている必要があります。</td>
</tr>
<tr class="even">
<td align="left"><p>OOB デバイス情報</p>
<p>「OOB デバイス情報属性フォーマットテーブル」を参照してください。</p></td>
<td align="left">1</td>
<td align="left">必須かどうか</td>
<td align="left">この属性は存在する必要があります。 この情報は、この P2P デバイスに関する情報を提供します。</td>
</tr>
<tr class="odd">
<td align="left"><p>OOB プロビジョニング情報</p>
<p></p></td>
<td align="left">2</td>
<td align="left">必須かどうか</td>
<td align="left">この属性は存在する必要があります。 このデバイスは、この P2P デバイスが使用することを想定しているプロビジョニング情報を提供します。</td>
</tr>
<tr class="even">
<td align="left"><p>OOB 構成のタイムアウト</p>
<p></p></td>
<td align="left">5</td>
<td align="left">必須かどうか</td>
<td align="left">この属性は存在する必要があります。 このメッセージは、この P2P デバイスが Wi-fi ダイレクトに対する応答を待機する時間に関する情報を提供します。</td>
</tr>
</tbody>
</table>

 

### <a name="oob-header-attribute-format"></a>OOB ヘッダー属性の形式

| フィールド名        | サイズ (オクテット) | Value    | 説明                                                                                                    |
|-------------------|---------------|----------|----------------------------------------------------------------------------------------------------------------|
| 合計データ長 | 2             | 変数 | OOB データ Blob 全体の長さ (ヘッダーを含む)。                                                             |
| 長さ            | 2             | 変数 | OOB ヘッダー内の次のフィールドの長さ。                                                                  |
| バージョン           | 1             | 0x10     | この P2P OOB レコードのバージョンを識別する値。                                                          |
| OOB の種類          | 1             | 変数 | OOB トランザクションの種類を識別する値。 特定の値は、 *OOB トランザクションの種類*のテーブルで定義されています。 |
| OUI               | 0または3        | 変数 | ベンダー固有の OUI。 これは省略可能な値です。 OOB の種類がベンダ固有の場合にのみ存在する必要があります。         |
| OUI の種類          | 0 または 1        | 変数 | ベンダー固有の型。 これは省略可能な値です。 OOB の種類がベンダ固有の場合にのみ存在する必要があります。        |

 

### <a name="oob-transaction-types"></a>OOB トランザクションの種類

| OOB の種類 (16 進) | 説明                          |
|----------------|--------------------------------------|
| 0x00           | OOB の一方向プロビジョニングデータ |
| 0x01           | OOB プロビジョニングリスナーデータ       |
| 0x02           | OOB プロビジョニングコネクタデータ      |
| 0x03           | OOB データの再呼び出し                    |
| 0x04-0xDC      | 予約済み                             |
| 0xDD           | ベンダー固有                      |
| 0xDE-0xFF      | 予約済み                             |

 

### <a name="oob-device-info-attribute-format"></a>OOB デバイス情報属性の形式

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド名</th>
<th align="left">サイズ (オクテット)</th>
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">属性 ID</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">P2P OOB 属性の種類を識別します。 特定の値は、 <em>P2P OOB Attributes</em>テーブルで定義されています。</td>
</tr>
<tr class="even">
<td align="left">長さ</td>
<td align="left">2</td>
<td align="left">変数</td>
<td align="left">属性内の次のフィールドの長さ。</td>
</tr>
<tr class="odd">
<td align="left">P2P デバイスアドレス</td>
<td align="left">6</td>
<td align="left">P2P 仕様で定義されているとおり。</td>
<td align="left">P2P デバイスを一意に参照するために使用される識別子。</td>
</tr>
<tr class="even">
<td align="left">構成メソッド</td>
<td align="left">2</td>
<td align="left">P2P 仕様で定義されているとおり。</td>
<td align="left"><p>このデバイスでサポートされている WSC メソッド。</p>
<div class="alert">
<strong>注</strong>  [構成メソッド] フィールド内のバイト順序は、ビッグエンディアンである必要があります。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left">プライマリデバイスの種類</td>
<td align="left">8</td>
<td align="left">P2P 仕様で定義されているとおり。</td>
<td align="left"><p>P2P デバイスのプライマリデバイスの種類。 WSC プライマリデバイスタイプ属性のデータ部分のみが含まれます (属性 ID と長さフィールドは除外されます)。</p>
<div class="alert">
<strong>注  :</strong> [プライマリデバイスの種類] フィールド内のバイト順序は、ビッグエンディアンである必要があります。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">デバイス機能ビットマップ</td>
<td align="left">1</td>
<td align="left">P2P 仕様で定義されているとおり。</td>
<td align="left">P2P デバイスの機能を示すパラメーターのセット。</td>
</tr>
<tr class="odd">
<td align="left">［デバイス名］</td>
<td align="left">変数</td>
<td align="left">P2P 仕様で定義されているとおり。</td>
<td align="left"><p>P2P デバイスのフレンドリ名。 WSC デバイス名属性 TLV 形式全体を含みます。</p>
<div class="alert">[デバイス名] フィールド内のバイト順序は、ビッグエンディアンである必要がある
<strong>ことに注意</strong>してください  。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

### <a name="p2p-oob-attributes"></a>P2P OOB 属性

| OOB の種類 (16 進) | 説明               |
|----------------|---------------------------|
| 0x00           | OOB の状態                |
| 0x01           | OOB デバイス情報           |
| 0x02           | OOB プロビジョニング情報     |
| 0x03           | OOB グループ ID              |
| 0x04           | OOB リッスンチャネル        |
| 0x05           | OOB 構成のタイムアウト |
| 0x06-0xDC      | 予約済み                  |
| 0xDD           | ベンダー固有の属性 |
| 0xDE-0xFF      | 予約済み                  |

 

### <a name="oob-provisioning-info-attribute-format"></a>OOB プロビジョニング情報属性の形式

| フィールド名                   | サイズ (オクテット) | Value                   | 説明                                                                                                                                                             |
|------------------------------|---------------|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 属性 ID                 | 1             | 1                       | P2P OOB 属性の種類を識別します。 特定の値は、 *P2P OOB Attributes*テーブルで定義されています。                                                                 |
| 長さ                       | 2             | 変数                | 属性内の次のフィールドの長さ。                                                                                                                        |
| プロビジョニング設定ビットマップ | 1             | 変数                | プロビジョニング*設定の表に*定義されている一連のプロビジョニング設定オプション。                                                                                   |
| 選択された構成方法       | 2             | P2P 仕様で定義されているとおり。 | この P2P デバイスによってプロビジョニングのために選択された WSC メソッド。                                                                                                   |
| Pin の長さ                   | 1             | 0 - 8                   | 次の PIN データフィールドのバイト数。 このフィールドを0に設定すると、追加の PIN データは表示されません。                                                                  |
| データをピン留めする                     | 変数      | n                       | このフィールドはオプションです。 このフィールドは、PIN の長さフィールドが0以外の場合にのみ存在し、プロビジョニングに使用する PIN を表すオクテットの配列が含まれています。 |

 

### <a name="provisioning-settings"></a>プロビジョニングの設定

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット</th>
<th align="left">情報</th>
<th align="left">注意</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">新しいグループの作成</td>
<td align="left">このプロビジョニング情報がターゲットの P2P デバイスで新しいグループを形成するためのものである場合、[新しいグループの作成] ビットは1に設定されます。 それ以外の場合、このプロビジョニング情報は既存のグループに参加するためのものです。</td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">グループの種類の設定を強制する</td>
<td align="left">必要なグループの種類のビットを強制的に適用する必要がある場合、[グループの種類の強制] 設定の [ビット] が1に設定されます。それ以外の場合は、必要なグループの種類のビットは単に優先</td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">必要なグループの種類</td>
<td align="left">必要なグループの種類が一時的である場合は、必要なグループの種類のビットを0に設定し、必要なグループの種類が永続的である場合は1に設定する必要があります。</td>
</tr>
<tr class="even">
<td align="left">3 - 7</td>
<td align="left">予約済み</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="oob-configuration-timeout-attribute-format"></a>OOB 構成のタイムアウト属性の形式

| フィールド名                     | サイズ (オクテット) | Value   | 説明                                                                                                                                                        |
|--------------------------------|---------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 属性 ID                   | 1             | 5       | P2P OOB 属性の種類を識別します。 特定の値は、 *P2P OOB Attributes*テーブルで定義されています。                                                            |
| 長さ                         | 2             | 1       | 属性内の次のフィールドの長さ。                                                                                                                   |
| リスナー構成のタイムアウト | 1             | 0 - 255 | この P2P デバイスが OOB データ転送後に Wi-fi Direct 通信を待機する時間 (100 ミリ秒単位)。 (最大25.5 秒)。 |

 

### <a name="windows-device-pairing-record"></a>Windows デバイスのペアリングレコード

Windows デバイスのペアリングレコードは、NDEF 仕様に従っています。 接続の引き渡しの選択メッセージを処理する方法について、Windows に関する追加情報を提供します。 TNF および Type フィールドは、NDEF 仕様に従って指定する必要があります。 次の他のフィールドは、NDEF レコードのペイロードフィールドに順番に一覧表示されます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド名</th>
<th align="left">Value</th>
<th align="left">長さの値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">TNF</td>
<td align="left">0x02</td>
<td align="left">3ビット</td>
<td align="left">次に続く型フィールドの形式。 RFC 2046 で定義されているメディアの種類。</td>
</tr>
<tr class="even">
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">' application/vnd. ms-windows '</td>
<td align="left">0x28 バイト数</td>
<td align="left">このシナリオに対して定義する新しい型の文字列。</td>
</tr>
<tr class="odd">
<td align="left">MajorVersion</td>
<td align="left">0x1</td>
<td align="left">2バイト</td>
<td align="left">メジャーバージョンは0x1 にする必要があります。</td>
</tr>
<tr class="even">
<td align="left">MinorVersion</td>
<td align="left">0x0</td>
<td align="left">2バイト</td>
<td align="left">マイナーバージョンは0x0 にする必要があります。</td>
</tr>
<tr class="odd">
<td align="left">フラグ</td>
<td align="left">0x0 または0x01</td>
<td align="left">4バイト</td>
<td align="left"><p>すべてのトランスポートを試すには、0x0 に設定します。</p>
<p>0x1 に設定すると、インストールを順番に試行し、最初の成功後に停止します。 トランスポートの優先順位は、代替の運送業者レコードのシーケンスによって示されます。</p>
<div class="alert">
<strong>注</strong>  0x0064 から0X0002 の値は予約されています。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">デバイスのフレンドリ名の長さ</td>
<td align="left">デバイスのフレンドリ名フィールドの長さ。</td>
<td align="left">1バイト</td>
<td align="left">デバイスのフレンドリ名の長さ。</td>
</tr>
<tr class="odd">
<td align="left">デバイスのフレンドリ名</td>
<td align="left">255バイトまでの UTF-8 エンコードされた文字列。</td>
<td align="left">デバイスのフレンドリ名の長さ</td>
<td align="left">クライアントの同意 UI に表示されるデバイスのフレンドリ名。</td>
</tr>
</tbody>
</table>

 

### <a href="" id="wi-fi-direct--just-works--ceremony--static-connection-handover-tag-format"></a>Wi-fi Direct "Works" の形式で、静的な接続の転送タグの形式

例として、NFC パッシブタグの一般的な実装を次に示します。 これは、Wi-fi ダイレクトキャリアレコード、ネットワーク共有プリンター、および ms デバイスのペアリングレコードと共に、静的な接続の転送ケースに対応します。

この最初の表は、タグの Wi-fi Direct ペアリング部分の形式を示しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">コンテンツ</th>
<th align="left">長さ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">0x91</td>
<td align="left">1</td>
<td align="left"><p>NDEF Record ヘッダー:</p>
<p>MB = 1b、ME = 0b、CF = 0b、SR = 1b、IL = 0b、TNF = 001b</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">レコードの種類の長さ: 2 オクテット</td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">0x0A</td>
<td align="left">1</td>
<td align="left">レコードの種類の長さ:10 オクテット</td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">0x48 0x73</td>
<td align="left">2</td>
<td align="left">レコードの種類: "Hs"</td>
</tr>
<tr class="odd">
<td align="left">5</td>
<td align="left">0x12</td>
<td align="left">1</td>
<td align="left">バージョン番号: Major = 1、Minor = 2</td>
</tr>
<tr class="even">
<td align="left">6</td>
<td align="left">0xD1</td>
<td align="left">1</td>
<td align="left"><p>NDEF Record ヘッダー:</p>
<p>MB = 1b、ME = 1b、CF = 0b、SR = 1b、IL = 0b、TNF = 001b</p></td>
</tr>
<tr class="odd">
<td align="left">7</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">レコードの種類の長さ: 2 オクテット</td>
</tr>
<tr class="even">
<td align="left">8</td>
<td align="left">0x04</td>
<td align="left">1</td>
<td align="left">ペイロードの長さ: 4 オクテット</td>
</tr>
<tr class="odd">
<td align="left">9</td>
<td align="left">0x61 0x63</td>
<td align="left">2</td>
<td align="left">レコードの種類: "ac"</td>
</tr>
<tr class="even">
<td align="left">11</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">通信事業者フラグ: CPS = 1、"active"</td>
</tr>
<tr class="odd">
<td align="left">12</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">通信事業者データ参照の長さ: 1 オクテット</td>
</tr>
<tr class="even">
<td align="left">13</td>
<td align="left">0x30</td>
<td align="left">1</td>
<td align="left">通信事業者データ参照: "0"</td>
</tr>
<tr class="odd">
<td align="left">14</td>
<td align="left">0x00</td>
<td align="left">1</td>
<td align="left">補助データ参照カウント: 0</td>
</tr>
<tr class="even">
<td align="left">15</td>
<td align="left">0x1A</td>
<td align="left">1</td>
<td align="left"><p>NDEF Record ヘッダー:</p>
<p>MB = 0b、ME = 0b、CF = 0b、SR = 1b、IL = 1b、TNF = 010b</p></td>
</tr>
<tr class="odd">
<td align="left">16</td>
<td align="left">0x22</td>
<td align="left">1</td>
<td align="left">レコードの種類名の長さ:34 オクテット</td>
</tr>
<tr class="even">
<td align="left">17</td>
<td align="left">0x3E</td>
<td align="left">1</td>
<td align="left">ペイロードの長さ:62 オクテット</td>
</tr>
<tr class="odd">
<td align="left">18</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">Id の長さ: 1 オクテット</td>
</tr>
<tr class="even">
<td align="left">19</td>
<td align="left"><p>0x61 0x70 0x70 0x6C</p>
<p>0x69 0x69 0x61 0x74</p>
<p>0x69 0X69 0X69 0x2F</p>
<p>0x76 0x6E 0x64 0x2E</p>
<p>0x6D 0x73 0x2D 0x73</p>
<p>0x69 0X69 0x64 0X69</p>
<p>0x77 0x77 0x2E 0x77</p>
<p>0x66 0x64 0x2E 0X66</p>
<p>0x6F 0x6f</p></td>
<td align="left">34</td>
<td align="left">レコードの種類の名前: ' application/vnd. ms-windows '</td>
</tr>
<tr class="odd">
<td align="left">53</td>
<td align="left">0x30</td>
<td align="left">1</td>
<td align="left">Id: "0"</td>
</tr>
<tr class="even">
<td align="left">54</td>
<td align="left">0x3E 0x00</td>
<td align="left">2</td>
<td align="left"><p>Wi-fi ダイレクト OOB データの長さ:62 オクテット。 長さは unsigned short として読み取られ、包括されます。</p>
<p>blob 全体の。 2つの長さのオクテットを含みます。 この値は、リトルエンディアン形式で格納する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left">56</td>
<td align="left">0x02、0x00</td>
<td align="left">2</td>
<td align="left">ヘッダーの長さ: 2 オクテット</td>
</tr>
<tr class="even">
<td align="left">58</td>
<td align="left">0x10</td>
<td align="left">1</td>
<td align="left">バージョン: 0x10</td>
</tr>
<tr class="odd">
<td align="left">59</td>
<td align="left">0x00</td>
<td align="left">1</td>
<td align="left">OOB の種類: 0x00 (一方向)</td>
</tr>
<tr class="even">
<td align="left">60</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">属性: 0x01 (デバイス情報属性)</td>
</tr>
<tr class="odd">
<td align="left">61</td>
<td align="left">0x22 0x00</td>
<td align="left">2</td>
<td align="left">デバイス情報の長さ:34 オクテット</td>
</tr>
<tr class="even">
<td align="left">63</td>
<td align="left"><p>0x01 0x23 0x34 0xab</p>
<p>0xcd 0xcd</p></td>
<td align="left">6</td>
<td align="left">Wi-fi Direct P2P デバイスの MAC アドレス: "01:23:34<span class="emoji" shortCode="ab">🆎</span>cd: ef"</td>
</tr>
<tr class="odd">
<td align="left">69</td>
<td align="left">0x01 0x00</td>
<td align="left">2</td>
<td align="left">構成の種類</td>
</tr>
<tr class="even">
<td align="left">71</td>
<td align="left"><p>0x00 0x01 0x00 0x50</p>
<p>0xF2 0x00 0x00</p></td>
<td align="left">8</td>
<td align="left">プライマリデバイスの種類</td>
</tr>
<tr class="odd">
<td align="left">79</td>
<td align="left">0x12</td>
<td align="left">1</td>
<td align="left">機能</td>
</tr>
<tr class="even">
<td align="left">80</td>
<td align="left">0x10 0x11</td>
<td align="left">2</td>
<td align="left">属性: デバイス名</td>
</tr>
<tr class="odd">
<td align="left">82</td>
<td align="left">0x00 0x0d</td>
<td align="left">2</td>
<td align="left">デバイス名の長さ:13 オクテット</td>
</tr>
<tr class="even">
<td align="left">84</td>
<td align="left"><p>0x43 0x6f 0x6f 0x74</p>
<p>0x6f 0x73 0x6f 0x20</p>
<p>0x4d 0x6f 0x75 0x75</p>
<p>0x65</p></td>
<td align="left">13</td>
<td align="left"><p>UTF-8 でのデバイスのフレンドリ名。 NULL 終端文字がないこと、および UTF-8 であることに注意してください。</p>
<p>1文字あたり1バイトまたは2バイトにすることができます。 この例では、"Contoso Mouse" を読み取ります。</p></td>
</tr>
<tr class="odd">
<td align="left">97</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">属性: プロビジョニング情報</td>
</tr>
<tr class="even">
<td align="left">98</td>
<td align="left">0x0c 0x00</td>
<td align="left">2</td>
<td align="left">プロビジョニング情報の長さ:12 オクテット</td>
</tr>
<tr class="odd">
<td align="left">100</td>
<td align="left">0x07</td>
<td align="left">1</td>
<td align="left">ビットマップの設定: 新しいグループ、永続的の強制</td>
</tr>
<tr class="even">
<td align="left">101</td>
<td align="left">0x01 0x00</td>
<td align="left">2</td>
<td align="left">構成方法: pin の入力</td>
</tr>
<tr class="odd">
<td align="left">103</td>
<td align="left">0x08</td>
<td align="left">1</td>
<td align="left">Pin の長さ: 8 オクテット</td>
</tr>
<tr class="even">
<td align="left">104</td>
<td align="left"><p>0x01 0x02 0x03 0x04</p>
<p>0x05 0x06 0x07 0x08</p></td>
<td align="left">8</td>
<td align="left">Pin: "12345678"</td>
</tr>
<tr class="odd">
<td align="left">112</td>
<td align="left">0x05</td>
<td align="left">1</td>
<td align="left">属性: 構成のタイムアウト情報</td>
</tr>
<tr class="even">
<td align="left">113</td>
<td align="left">0x01 0x00</td>
<td align="left">2</td>
<td align="left">構成のタイムアウトの長さ</td>
</tr>
<tr class="odd">
<td align="left">115</td>
<td align="left">0x64</td>
<td align="left">1</td>
<td align="left">10秒 (100 ミリ秒単位)</td>
</tr>
</tbody>
</table>

 

この2番目の表は、タグのネットワークプリンターのペアリング部分の形式を示しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">コンテンツ</th>
<th align="left">長さ</th>
<th align="left">それぞれ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">116</td>
<td align="left">0x12</td>
<td align="left">1</td>
<td align="left"><p>NDEF record ヘッダー:</p>
<p>MB = 0b、ME = 0b、CF = 0b、SR = 1b、IL = 0b、TNF = 010b</p></td>
</tr>
<tr class="even">
<td align="left">117</td>
<td align="left">0x29</td>
<td align="left">1</td>
<td align="left">型の長さフィールド</td>
</tr>
<tr class="odd">
<td align="left">118</td>
<td align="left">0x19</td>
<td align="left">1</td>
<td align="left">ペイロードの長さのフィールド</td>
</tr>
<tr class="even">
<td align="left">119</td>
<td align="left"><p>0x61 0x70 0x70 0x6c</p>
<p>0x69 0x69 0x61 0x74</p>
<p>0x69 0x69 0x69 0x2f</p>
<p>0x76 0x6e 0x64 0x2e</p>
<p>0x6d 0x73 0x2d 0x73</p>
<p>0x69 0x69 0x64 0x69</p>
<p>0x77 0x77 0x2e 0x6e</p>
<p>0x77 0x70 0x77 0x69</p>
<p>0x6e 0x74 0x6e 0x6e</p>
<p>0x67 0x2e 0x67 0x67</p>
<p>0x62</p></td>
<td align="left">41</td>
<td align="left">レコードの種類の名前: "application/vnd. ms-windows"</td>
</tr>
<tr class="odd">
<td align="left">160</td>
<td align="left"><p>0x5c 0x5c 0x70 0x72</p>
<p>0x69 0x69 0x74 0x53</p>
<p>0x65 0x72 0x72 0x65</p>
<p>0x72 0x5c 0x70 0x72</p>
<p>0x69 0x69 0x74 0x69</p>
<p>0x72 0x4e 0x61 0x6d</p>
<p>0x65</p></td>
<td align="left">25</td>
<td align="left">プリンター名: "\printServer\printerName"</td>
</tr>
</tbody>
</table>

 

この3番目の表は、タグの MS デバイスのペアリング部分の形式を示しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">コンテンツ</th>
<th align="left">長さ</th>
<th align="left">それぞれ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">185</td>
<td align="left">0x52</td>
<td align="left">1</td>
<td align="left"><p>NDEF record ヘッダー:</p>
<p>MB = 0b、ME = 1b、CF = 0b、SR = 1b、IL = 0b、TNF = 010b</p></td>
</tr>
<tr class="even">
<td align="left">186</td>
<td align="left">0x28</td>
<td align="left">1</td>
<td align="left">型の長さフィールド</td>
</tr>
<tr class="odd">
<td align="left">187</td>
<td align="left">0x15</td>
<td align="left">1</td>
<td align="left">ペイロードの長さのフィールド</td>
</tr>
<tr class="even">
<td align="left">188</td>
<td align="left"><p>0x61 0x70 0x70 0x6c</p>
<p>0x69 0x69 0x61 0x74</p>
<p>0x69 0x69 0x69 0x2f</p>
<p>0x76 0x6e 0x64 0x2e</p>
<p>0x6d 0x73 0x2d 0x73</p>
<p>0x69 0x69 0x64 0x69</p>
<p>0x77 0x77 0x2e 0x64</p>
<p>0x65 0x76 0x65 0x65</p>
<p>0x65 0x70 0x61 0x65</p>
<p>0x72 0x69 0X69 0x69</p></td>
<td align="left">40</td>
<td align="left">レコードの種類の名前: "application/vnd. ms-windows"</td>
</tr>
<tr class="odd">
<td align="left">228</td>
<td align="left">0x00 0x01 0x00</td>
<td align="left">ホーム フォルダーが置かれているコンピューターにアクセスできない</td>
<td align="left">バージョン: Major = 1、Minor = 0</td>
</tr>
<tr class="even">
<td align="left">232</td>
<td align="left">0x00</td>
<td align="left">1</td>
<td align="left">フラグ: 0 に設定し、すべてのトランスポートを試行します。</td>
</tr>
<tr class="odd">
<td align="left">233</td>
<td align="left">0x0F</td>
<td align="left">1</td>
<td align="left">デバイスのフレンドリ名の長さ</td>
</tr>
<tr class="even">
<td align="left">234</td>
<td align="left"><p>0x43 0x6f 0x6f 0x74</p>
<p>0x6f 0x73 0x6f 0x20</p>
<p>0x50 0x72 0x69 0x69</p>
<p>0x74 0x65 0x74</p></td>
<td align="left">15</td>
<td align="left">ユーザーに表示されるデバイスのフレンドリ名: "Contoso Printer"</td>
</tr>
</tbody>
</table>

 

## <a name="wi-fi-direct-connectivity-requirements"></a>Wi-fi Direct 接続の要件


デバイスとクライアントで Wi-fi ラジオをオンにする必要があります。 それ以外の場合、ペアリングは失敗します。

## <a name="handling-edge-cases"></a>エッジケースの処理


ユーザーが以前にデバイスをペアリングした後、デバイスの一覧からデバイスを手動で削除した場合は、を再度タップすると、のインストールまたはペアリングが試行されます。

ユーザーがその範囲内に入力した後で、帯域外 (OOB) 情報が転送される前に突然離脱する場合、デバイスは接続可能になりますが、PC はデバイスを検索しません。 この場合、PC から同意 UI がないため、ユーザーはもう一度をタップする必要があります。 デバイスを再びタップしたときに検出可能な場合は、検出可能な状態を維持し、タイムアウト期間をリセットする必要があります。

Wi-fi ダイレクトデバイスの場合、Wi-fi ラジオがオフになっていると、インストールは正常に実行されません。

ユーザーが2つのデバイスを同時にタップした場合、最初に受信した OOB 情報のペアリングのみが試行されます。

タップをサポートしていないオペレーティングシステムを実行しているシステム上のデバイスをタップしようとすると、デバイスは接続可能モードになりますが、ペアリングは行われません。 ユーザーは、Bluetooth 用に提供されているペアリング UI を使用し、ペアリングボタンを使用してペアリングを開始する必要があります。

 

 
## <a name="related-topics"></a>関連トピック
 [NFC デバイス ドライバー インターフェイス (DDI) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
 
