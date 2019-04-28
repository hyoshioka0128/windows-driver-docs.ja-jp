---
title: Wi-Fi Direct ペアリングの実装
description: このセクションでは、デザインのガイドラインを提供します。 とユース ケースをタップし、セットアップし、タップおよび再接続に参加する周辺機器のデバイスの要件。
ms.assetid: 1B729E9F-DF9F-4263-9F0B-5EDCF817D2C3
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0f1a2ff29bd16f0eba6a57b54be41173c750db8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373576"
---
# <a name="wi-fi-direct-pairing-implementation"></a>Wi-Fi Direct ペアリングの実装


このセクションでは、デザインのガイドラインを提供します。 とユース ケースをタップし、セットアップし、タップおよび再接続に参加する周辺機器のデバイスの要件。

**注**  プリンター デバイスのみにペアリングするには Windows 8.1 では、ペアリングの実装では、このトピックで説明されているが現在サポートされています。

 

**注**  Wi-fi alliance の Wi-fi P2P 通信事業者の構成レコードを Wi-Fi Direct の静的な接続に移行する Windows 10 が NFC にもサポートしています。 詳細については、次を参照してください。 [Wi-fi Alliance](http://www.wi-fi.org)します。

 

## <a name="peripheral-wi-fi-direct-device-pairing"></a>周辺の Wi-Fi Direct デバイスのペアリング


タップ中には、NFP は、接続しているデバイスからのペアリング情報を受信します。 NFP は、Windows にペアリングの情報を渡します。 Wi-Fi Direct デバイスには、Wi-fi Alliance 帯域外の (OOB) のペアリングの手順と、NFC フォーラムの推奨事項に従ってください。 Windows は、独自の下記のようにメッセージをペアに依存します。

Windows がユーザーに、同意を求められ、Windows は成功するまでに、それぞれの順序で、アドレスに接続しようとしてが指定された場合。 それ以上の対話を PC に NFP プロバイダーと接続しているデバイスの間はありません。

NFC を使用して、例として、一方向のインストールは (静的エミュレーション モードで、アクティブな NFC タグを使用も可能性があります)、静的またはパッシブ NFC タグのペアに関する情報を格納することによって実現されます。 Windows は、ペアリングの情報にサブスクライブします。 PC に、NFC 対応 NFP プロバイダーは、タグからの接続情報を受信し、これをサブスクライバーとしての Windows に渡します。 帯域外でデバイスの実際のインストールを実行している Windows の接続情報の受領デバイス クラスの特定の手法を使用します。

## <a name="interoperability-requirements"></a>相互運用性の要件


NFP プロバイダー間で相互運用性を確認するには、プロバイダー固有のメッセージの形式でペアリングの情報をカプセル化する必要があります。

このドキュメントでは、NFC 対応 NFP プロバイダー以外の近接通信テクノロジの特定の要件はありません。

Windows では、Wi-Fi Direct の OOB ペアリングの一方向のペアリングの情報を伝達するための特定の NFC フォーラム: 定義されているメカニズムをサポートするために、NFC 対応 NFP プロバイダーが必要です。 NDEF メッセージには、TNF フィールド値 0x01 は最初のレコードと"%hs"に相当する型のフィールドと Wi-Fi Direct キャリア構成レコードを参照する代替の運送業者のレコードが含まれています。 このメソッドは、NDEF レコードのペイロードのみが使用されます。

## <a name="unidirectional-pairing-using-nfc-for-wi-fi-direct"></a>ペアリング Wi-Fi Direct の NFC を使用すると、一方向


ここでは、NFC、Wi-Fi Direct、および Windows がどのように連携してプリンターなどの Wi-Fi Direct デバイスの一方向のワイヤレス ペアリングをサポートするためにで詳細を示します。

### <a name="nfp-provider-references"></a>NFP プロバイダー参照

Wi-Fi Direct ペアリングを使用して、NFC フォーラムに標準化されたメッセージの種類の接続に移行を選択します。 図の下には、Wi-Fi Direct デバイスのペア、NDEF レコード具体的には 3 と 4 の接続の引き渡し選択メッセージを適用する方法の概要を説明します。 引き渡し選択メッセージには、"ac"または「代替キャリア」レコードの 1 つまたは複数がについて説明します。 これらのレコードが引き渡し選択レコードを順番にに従ってし、適切に定義された型である各します。 最後に、メッセージは、Windows をペアリングの操作を処理する方法に関する情報を提供するレコードをペアリング Microsoft 定義済みのデバイスが含まれます。

![接続の引き渡し メッセージ](images/handover.png)

### <a name="wi-fi-direct-device-pairing-message"></a>メッセージをペアリング Wi-Fi Direct デバイス

次のサンプルの使用の場合、NFC の 2 種類のタグは、分かりやすい例として使用されます。 を別の NFC タグの種類を使用する必要がある場合、そのタグの定義に従って NDEF メッセージを正しくカプセル化する必要があります。

| フィールド                 | 値                                            | 説明                                                               |
|-----------------------|--------------------------------------------------|---------------------------------------------------------------------------|
| TNF                   | 0x02                                             | 次の種類 フィールドの形式です。 RFC 2046 で定義されている、メディアの種類。 |
| 型                  | 'application/vnd.ms-windows.wfd.oob'             | 新しい型の文字列がこのシナリオを定義します。                              |
| OOB のデータのサイズ      | WORD                                             | サポートされている OOB データに最大 64 KB です。                                        |
| Wi-Fi Direct OOB データ | &lt;前のフィールドで示されるサイズの blob&gt; | Wi-Fi Direct OOB データ定義は後述します。                                   |

 

### <a name="wi-fi-direct-oob-format"></a>Wi-Fi Direct OOB 形式

次の表では、WiFi 直接 OOB データの形式について説明します。 OOB の一方向のデータは、任意の一方向の P2P OOB デバイスによって送信可能性があります。

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
<th align="left">注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OOB ヘッダー</p>
<p>OOB ヘッダー属性の形式のテーブルを参照してください。</p></td>
<td align="left">N/A</td>
<td align="left">必須</td>
<td align="left">OOB ヘッダー属性は、P2P OOB データの blob に存在して、「OOB 一方向のプロビジョニング データ」に設定、OOB 型の値があるものとします。</td>
</tr>
<tr class="even">
<td align="left"><p>OOB のデバイス情報</p>
<p>OOB のデバイス情報属性の形式のテーブルを参照してください。</p></td>
<td align="left">1</td>
<td align="left">必須</td>
<td align="left">この属性は、存在する必要があります。 この P2P デバイスに関する情報を提供します。</td>
</tr>
<tr class="odd">
<td align="left"><p>OOB プロビジョニングの情報</p>
<p></p></td>
<td align="left">2</td>
<td align="left">必須</td>
<td align="left">この属性は、存在する必要があります。 使用するこの P2P デバイスを想定するプロビジョニング情報を提供します。</td>
</tr>
<tr class="even">
<td align="left"><p>OOB 構成のタイムアウト</p>
<p></p></td>
<td align="left">5</td>
<td align="left">必須</td>
<td align="left">この属性は、存在する必要があります。 この P2P デバイスが Wi-Fi Direct 経由で応答を待つはどのくらいの期間に関する情報を提供します。</td>
</tr>
</tbody>
</table>

 

### <a name="oob-header-attribute-format"></a>OOB ヘッダー属性の形式

| フィールド名        | サイズ (オクテット) | 値    | 説明                                                                                                    |
|-------------------|---------------|----------|----------------------------------------------------------------------------------------------------------------|
| データの合計の長さ | 2             | 変数 | OOB データ Blob 全体 (ヘッダーを含む) の長さ。                                                             |
| 長さ            | 2             | 変数 | OOB のヘッダーには、次のフィールドの長さ。                                                                  |
| バージョン           | 1             | 0x10     | この P2P OOB レコードのバージョンを識別する値。                                                          |
| OOB の種類          | 1             | 変数 | OOB のトランザクションの種類を識別する値。 特定の値が定義されている*OOB トランザクション タイプ*テーブル。 |
| OUI               | 0 または 3        | 変数 | ベンダー固有の OUI します。 これは、省略可能な値です。 OOB の種類がベンダー固有の場合に存在する必要がありますのみ。         |
| OUI 型          | 0 または 1        | 変数 | ベンダー固有の型。 これは、省略可能な値です。 OOB の種類がベンダー固有の場合に存在する必要がありますのみ。        |

 

### <a name="oob-transaction-types"></a>OOB のトランザクションの種類

| OOB の種類 (16 進数) | 説明                          |
|----------------|--------------------------------------|
| 0x00           | OOB プロビジョニング データを一方向 |
| 0x01           | OOB プロビジョニング リスナー データ       |
| 0x02           | OOB プロビジョニング コネクタのデータ      |
| 0x03           | OOB Reinvoke データ                    |
| 0x04 0xDC      | 予約済み                             |
| 0 xdd を設定           | ベンダー固有                      |
| 0xDE 0 xff      | 予約済み                             |

 

### <a name="oob-device-info-attribute-format"></a>OOB のデバイス情報の属性の形式

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
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">属性 ID</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">P2P OOB 属性の型を識別します。 特定の値が定義されている、 <em>P2P OOB 属性</em>テーブル。</td>
</tr>
<tr class="even">
<td align="left">長さ</td>
<td align="left">2</td>
<td align="left">変数</td>
<td align="left">属性には、次のフィールドの長さ。</td>
</tr>
<tr class="odd">
<td align="left">P2P デバイス アドレス</td>
<td align="left">6</td>
<td align="left">P2P 仕様で定義します。</td>
<td align="left">P2P デバイスを一意に参照するための識別子。</td>
</tr>
<tr class="even">
<td align="left">構成メソッド</td>
<td align="left">2</td>
<td align="left">P2P 仕様で定義します。</td>
<td align="left"><p>このデバイスでサポートされている WSC メソッド。</p>
<div class="alert">
<strong>注</strong>  Config メソッド フィールド内のバイト順は純益ビッグ エンディアン。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left">プライマリ デバイスの種類</td>
<td align="left">8</td>
<td align="left">P2P 仕様で定義します。</td>
<td align="left"><p>P2P デバイスのプライマリ デバイスの種類。 (属性の ID と長さのフィールドを除く) WSC プライマリ デバイスの種類属性のデータの一部のみが含まれています。</p>
<div class="alert">
<strong>注</strong>  バイトのプライマリ デバイスの種類のフィールド内で順序付けは純益ビッグ エンディアン。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">デバイス機能のビットマップ</td>
<td align="left">1</td>
<td align="left">P2P 仕様で定義します。</td>
<td align="left">P2P デバイスの機能を示すパラメーターのセット。</td>
</tr>
<tr class="odd">
<td align="left">［デバイス名］</td>
<td align="left">変数</td>
<td align="left">P2P 仕様で定義します。</td>
<td align="left"><p>P2P デバイスのフレンドリ名。 全体の WSC デバイス名属性 TLV 形式が含まれています。</p>
<div class="alert">
<strong>注</strong>  デバイス名 フィールド内のバイト順は純益ビッグ エンディアン。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

### <a name="p2p-oob-attributes"></a>P2P OOB 属性

| OOB の種類 (16 進数) | 説明               |
|----------------|---------------------------|
| 0x00           | OOB ステータス                |
| 0x01           | OOB のデバイス情報           |
| 0x02           | OOB プロビジョニングの情報     |
| 0x03           | OOB グループ ID              |
| 0x04           | OOB リッスン チャネル        |
| 0x05           | OOB 構成のタイムアウト |
| 0x06 0xDC      | 予約済み                  |
| 0 xdd を設定           | ベンダー固有の属性 |
| 0xDE 0 xff      | 予約済み                  |

 

### <a name="oob-provisioning-info-attribute-format"></a>OOB プロビジョニング情報の属性の形式

| フィールド名                   | サイズ (オクテット) | 値                   | 説明                                                                                                                                                             |
|------------------------------|---------------|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 属性 ID                 | 1             | 1                       | P2P OOB 属性の型を識別します。 特定の値が定義されている*P2P OOB 属性*テーブル。                                                                 |
| 長さ                       | 2             | 変数                | 属性には、次のフィールドの長さ。                                                                                                                        |
| プロビジョニングの設定のビットマップ | 1             | 変数                | 定義されているプロビジョニングの設定オプションのセット、*プロビジョニングの設定*テーブル。                                                                                   |
| 選択した構成方法       | 2             | P2P 仕様で定義します。 | プロビジョニングするためには、この P2P デバイスで選択した WSC メソッド。                                                                                                   |
| Pin の長さ                   | 1             | 0 - 8                   | 次の暗証番号 (pin) のデータ フィールドのバイト数。 このフィールドに 0 に設定は、暗証番号 (pin) の追加のデータがないことを示します。                                                                  |
| 暗証番号 (pin) のデータ                     | 変数      | n                       | このフィールドは省略可能です。 PIN の長さのフィールドがない場合にのみ、このフィールドが存在する、0 をプロビジョニングに使用する際に PIN を表すオクテットの配列が含まれています。 |

 

### <a name="provisioning-settings"></a>プロビジョニングの設定

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット (s)</th>
<th align="left">情報</th>
<th align="left">メモ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">新しいグループを作成します。</td>
<td align="left">ターゲットの P2P デバイスに新しいグループを構成するためのプロビジョニング情報がある場合、新しいグループの作成のビットは 1 に設定します。 それ以外の場合、このプロビジョニング情報は、既存のグループに参加するためします。</td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">グループを適用する設定を入力</td>
<td align="left">必要なグループの種類のビットを指定する場合、グループの種類の設定を適用するビットが 1 に設定、それ以外の場合、必要なグループの種類のビットは、優先順位だけです。</td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">目的のグループの種類</td>
<td align="left">必要なグループの種類が一時的なものでは、必要なグループの種類が永続的な場合は 1 に設定するものと場合、必要なグループの種類のビットを 0 に設定するものとします。</td>
</tr>
<tr class="even">
<td align="left">3 - 7</td>
<td align="left">予約済み</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="oob-configuration-timeout-attribute-format"></a>OOB 構成タイムアウト属性の形式

| フィールド名                     | サイズ (オクテット) | 値   | 説明                                                                                                                                                        |
|--------------------------------|---------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 属性 ID                   | 1             | 5       | P2P OOB 属性の型を識別します。 特定の値が定義されている*P2P OOB 属性*テーブル。                                                            |
| 長さ                         | 2             | 1       | 属性には、次のフィールドの長さ。                                                                                                                   |
| リスナーの構成のタイムアウト | 1             | 0 - 255 | OOB のデータの転送、100 ミリ秒の単位で後にこの P2P デバイスが Wi-Fi Direct 通信の待機を費やす時間の量。 (最大 25.5 秒)。 |

 

### <a name="windows-device-pairing-record"></a>Windows のデバイスをペアリングするレコード

Windows デバイスのペアリング レコード NDEF 仕様に従っています。 Windows に接続引き渡し選択メッセージを処理する方法に関する追加情報が提供します。 NDEF 仕様に従って TNF と型のフィールドを指定する必要があります。 以下、他のフィールドは、NDEF レコードのペイロード フィールドに順番に表示されます。

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
<th align="left">値</th>
<th align="left">長さの値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">TNF</td>
<td align="left">0x02</td>
<td align="left">3 ビット</td>
<td align="left">次の種類 フィールドの形式です。 RFC 2046 で定義されている、メディアの種類。</td>
</tr>
<tr class="even">
<td align="left">型</td>
<td align="left">'application/vnd.ms-windows.devicepairing'</td>
<td align="left">0x28 バイト</td>
<td align="left">新しい型の文字列がこのシナリオを定義します。</td>
</tr>
<tr class="odd">
<td align="left">MajorVersion</td>
<td align="left">0x1</td>
<td align="left">2 バイト</td>
<td align="left">0x1 にするには、メジャー バージョンが必要です。</td>
</tr>
<tr class="even">
<td align="left">MinorVersion</td>
<td align="left">0x0</td>
<td align="left">2 バイト</td>
<td align="left">0x0 にするには、マイナー バージョンが必要です。</td>
</tr>
<tr class="odd">
<td align="left">フラグ</td>
<td align="left">0x0 または 0x01</td>
<td align="left">4 バイト</td>
<td align="left"><p>0x0 に設定すると、すべてのトランスポートを再試行してください。</p>
<p>インストールを順番にしようとして、最初の成功後に停止する 0x1 に設定します。 トランスポートの基本設定は、代替の運送業者のレコードのシーケンスが表示されます。</p>
<div class="alert">
<strong>注</strong>  0x0064 を通じて 0x0002 の値は予約されています。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">デバイスのフレンドリ名の長さ</td>
<td align="left">デバイスのフレンドリ名 フィールドの長さ。</td>
<td align="left">1 バイト</td>
<td align="left">デバイスのフレンドリ名の長さ。</td>
</tr>
<tr class="odd">
<td align="left">デバイスのフレンドリ名</td>
<td align="left">Utf-8 でエンコードされた文字列を 255 バイト以内の。</td>
<td align="left">デバイスのフレンドリ名の長さ</td>
<td align="left">デバイスのフレンドリ名が表示されるクライアントで UI を同意します。</td>
</tr>
</tbody>
</table>

 

### <a href="" id="wi-fi-direct--just-works--ceremony--static-connection-handover-tag-format"></a>Wi-Fi Direct"Just Works"手続き、タグの書式の静的な接続の引き渡し

たとえば、次は、パッシブ NFC タグの一般的な実装にします。 これは、Wi-Fi Direct の運送業者のレコードをネットワーク共有プリンターでは、ペアリングの ms デバイス レコードと静的な接続の引き渡しケースに対応します。

この最初のテーブルは、Wi-Fi Direct で、タグの部分をペアの形式を示しています。

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
<th align="left">Content</th>
<th align="left">長さ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">0x91</td>
<td align="left">1</td>
<td align="left"><p>NDEF レコード ヘッダー:</p>
<p>MB = 1b、ME = 0b、CF 0b、SR = 1b、IL を = = 0b、TNF 001b を =</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">レコードの種類の長さ:2 つのオクテット</td>
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
<td align="left">レコードの種類:"%Hs"</td>
</tr>
<tr class="odd">
<td align="left">5</td>
<td align="left">0x12</td>
<td align="left">1</td>
<td align="left">バージョン番号:主要な = 1、マイナー = 2</td>
</tr>
<tr class="even">
<td align="left">6</td>
<td align="left">0xD1</td>
<td align="left">1</td>
<td align="left"><p>NDEF レコード ヘッダー:</p>
<p>MB = 1b、ME = 1b、CF 0b、SR = 1b、IL を = = 0b、TNF 001b を =</p></td>
</tr>
<tr class="odd">
<td align="left">7</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">レコードの種類の長さ:2 つのオクテット</td>
</tr>
<tr class="even">
<td align="left">8</td>
<td align="left">0x04</td>
<td align="left">1</td>
<td align="left">ペイロードの長さ:4 オクテット</td>
</tr>
<tr class="odd">
<td align="left">9</td>
<td align="left">0x61 0x63</td>
<td align="left">2</td>
<td align="left">レコードの種類:"ac"</td>
</tr>
<tr class="even">
<td align="left">11</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">通信事業者のフラグ:CPS = 1、"active"</td>
</tr>
<tr class="odd">
<td align="left">12</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">通信事業者データの参照の長さ:1 オクテット</td>
</tr>
<tr class="even">
<td align="left">13</td>
<td align="left">0x30</td>
<td align="left">1</td>
<td align="left">通信事業者データの参照。“0”</td>
</tr>
<tr class="odd">
<td align="left">14</td>
<td align="left">0x00</td>
<td align="left">1</td>
<td align="left">補助データの参照カウント:0</td>
</tr>
<tr class="even">
<td align="left">15</td>
<td align="left">0x1A</td>
<td align="left">1</td>
<td align="left"><p>NDEF レコード ヘッダー:</p>
<p>MB = 0b、ME = 0b、CF 0b、SR = 1b、IL を = = 1 b、TNF 010b を =</p></td>
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
<td align="left">Id の長さ:1 オクテット</td>
</tr>
<tr class="even">
<td align="left">19</td>
<td align="left"><p>0x61 0x70 0x70 0x6C</p>
<p>0x69 0x63 0x61 0x74</p>
<p>0x69 0x6F 0x6E 0x2F</p>
<p>0x76 0x6E 0x64 0x2E</p>
<p>0x6D 0x73 0x2D 0x77</p>
<p>0x69 0x6E 0x64 0x6F</p>
<p>0x77 0x73 0x2E 0x77</p>
<p>0x66 0x64 0x2E 0x6F</p>
<p>0x6F 0x62</p></td>
<td align="left">34</td>
<td align="left">Record Type Name: 'application/vnd.ms-windows.wfd.oob'</td>
</tr>
<tr class="odd">
<td align="left">53</td>
<td align="left">0x30</td>
<td align="left">1</td>
<td align="left">Id:“0”</td>
</tr>
<tr class="even">
<td align="left">54</td>
<td align="left">0x3E 0x00</td>
<td align="left">2</td>
<td align="left"><p>Wi-Fi Direct OOB データの長さ:62 オクテット。 長さは unsigned short としては読み取り専用し、包括的には</p>
<p>blob 全体の。 長さの 2 オクテットが含まれています。 この値は、リトル エンディアン形式で格納する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left">56</td>
<td align="left">0x02, 0x00</td>
<td align="left">2</td>
<td align="left">ヘッダーの長さ:2 つのオクテット</td>
</tr>
<tr class="even">
<td align="left">58</td>
<td align="left">0x10</td>
<td align="left">1</td>
<td align="left">バージョン:0x10</td>
</tr>
<tr class="odd">
<td align="left">59</td>
<td align="left">0x00</td>
<td align="left">1</td>
<td align="left">OOB の種類:0x00 (一方向)</td>
</tr>
<tr class="even">
<td align="left">60</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">属性:0x01 (デバイス情報の属性)</td>
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
<p>0xcd 0xef</p></td>
<td align="left">6</td>
<td align="left">P2P の Wi-Fi Direct デバイスの MAC アドレス:“01:23:34<span class="emoji" shortCode="ab">🆎</span>cd:ef”</td>
</tr>
<tr class="odd">
<td align="left">69</td>
<td align="left">0x01 0x00</td>
<td align="left">2</td>
<td align="left">構成型</td>
</tr>
<tr class="even">
<td align="left">71</td>
<td align="left"><p>0x00 0x01 0x00 0x50</p>
<p>0xF2 0x00 0x00 0x00</p></td>
<td align="left">8</td>
<td align="left">プライマリ デバイスの種類</td>
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
<td align="left">属性:デバイス名</td>
</tr>
<tr class="odd">
<td align="left">82</td>
<td align="left">0x00 0x0d</td>
<td align="left">2</td>
<td align="left">デバイス名の長さ:13 オクテット</td>
</tr>
<tr class="even">
<td align="left">84</td>
<td align="left"><p>0x43 0x6f 0x6e 0x74</p>
<p>0x6f 0x73 0x6f 0x20</p>
<p>0x4d 0x6f 0x75 0x73</p>
<p>0x65</p></td>
<td align="left">13</td>
<td align="left"><p>Utf-8 でデバイスのフレンドリ名。 NULL で終了する文字とその utf-8 がないことに注意してください。</p>
<p>1 文字あたり 1 つまたは 2 つのバイトがあります。 この例は、「Contoso マウス」を読み取ります。</p></td>
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
<td align="left">プロビジョニング情報の長さ:12 のオクテット</td>
</tr>
<tr class="odd">
<td align="left">100</td>
<td align="left">0x07</td>
<td align="left">1</td>
<td align="left">ビットマップの設定: 新しいグループで、永続的な適用</td>
</tr>
<tr class="even">
<td align="left">101</td>
<td align="left">0x01 0x00</td>
<td align="left">2</td>
<td align="left">構成メソッド: エントリをピン留め</td>
</tr>
<tr class="odd">
<td align="left">103</td>
<td align="left">0x08</td>
<td align="left">1</td>
<td align="left">Pin の長さ:8 オクテット</td>
</tr>
<tr class="even">
<td align="left">104</td>
<td align="left"><p>0x01 0x02 0x03 0x04</p>
<p>0x05 0x06 0x07 0x08</p></td>
<td align="left">8</td>
<td align="left">暗証番号 (pin):“12345678”</td>
</tr>
<tr class="odd">
<td align="left">112</td>
<td align="left">0x05</td>
<td align="left">1</td>
<td align="left">属性:タイムアウトの構成情報</td>
</tr>
<tr class="even">
<td align="left">113</td>
<td align="left">0x01 0x00</td>
<td align="left">2</td>
<td align="left">タイムアウトの長さの構成</td>
</tr>
<tr class="odd">
<td align="left">115</td>
<td align="left">0x64</td>
<td align="left">1</td>
<td align="left">100 ミリ秒単位で、10 秒</td>
</tr>
</tbody>
</table>

 

2 番目のテーブルは、タグのネットワーク プリンターのペアリング部分の形式を示しています。

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
<th align="left">Content</th>
<th align="left">長さ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">116</td>
<td align="left">0x12</td>
<td align="left">1</td>
<td align="left"><p>NDEF レコード ヘッダー:</p>
<p>MB = 0b、ME = 0b、CF 0b、SR = 1b、IL を = = 0b、TNF 010b を =</p></td>
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
<td align="left">ペイロード長のフィールド</td>
</tr>
<tr class="even">
<td align="left">119</td>
<td align="left"><p>0x61 0x70 0x70 0x6c</p>
<p>0x69 0x63 0x61 0x74</p>
<p>0x69 0x6f 0x6e 0x2f</p>
<p>0x76 0x6e 0x64 0x2e</p>
<p>0x6d 0x73 0x2d 0x77</p>
<p>0x69 0x6e 0x64 0x6f</p>
<p>0x77 0x73 0x2e 0x6e</p>
<p>0x77 0x70 0x72 0x69</p>
<p>0x6e 0x74 0x69 0x6e</p>
<p>0x67 0x2e 0x6f 0x6f</p>
<p>0x62</p></td>
<td align="left">41</td>
<td align="left">レコードの種類名:"application/vnd.ms-windows.nwprinting.oob"</td>
</tr>
<tr class="odd">
<td align="left">160</td>
<td align="left"><p>0x5c 0x5c 0x70 0x72</p>
<p>0x69 0x6e 0x74 0x53</p>
<p>0x65 0x72 0x76 0x65</p>
<p>0x72 0x5c 0x70 0x72</p>
<p>0x69 0x6e 0x74 0x65</p>
<p>0x72 0x4e 0x61 0x6d</p>
<p>0x65</p></td>
<td align="left">25</td>
<td align="left">プリンター名:"\printServer\printerName"</td>
</tr>
</tbody>
</table>

 

この 3 番目のテーブルは、タグの MS デバイス ペアリング部分の形式を示しています。

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
<th align="left">Content</th>
<th align="left">長さ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">185</td>
<td align="left">0x52</td>
<td align="left">1</td>
<td align="left"><p>NDEF レコード ヘッダー:</p>
<p>MB=0b, ME=1b, CF=0b, SR=1b, IL=0b,TNF=010b</p></td>
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
<td align="left">ペイロード長のフィールド</td>
</tr>
<tr class="even">
<td align="left">188</td>
<td align="left"><p>0x61 0x70 0x70 0x6c</p>
<p>0x69 0x63 0x61 0x74</p>
<p>0x69 0x6f 0x6e 0x2f</p>
<p>0x76 0x6e 0x64 0x2e</p>
<p>0x6d 0x73 0x2d 0x77</p>
<p>0x69 0x6e 0x64 0x6f</p>
<p>0x77 0x73 0x2e 0x64</p>
<p>0x65 0x76 0x69 0x63</p>
<p>0x65 0x70 0x61 0x69</p>
<p>0x72 0x69 0x6E 0x67</p></td>
<td align="left">40</td>
<td align="left">レコードの種類名:"application/vnd.ms-windows.devicepairing"</td>
</tr>
<tr class="odd">
<td align="left">228</td>
<td align="left">0x00 0x01 0x00 0x00</td>
<td align="left">4</td>
<td align="left">バージョン:主要な 1、マイナーの = = 0</td>
</tr>
<tr class="even">
<td align="left">232</td>
<td align="left">0x00</td>
<td align="left">1</td>
<td align="left">Flags:0 に設定、すべてのトランスポートを実行してください。</td>
</tr>
<tr class="odd">
<td align="left">233</td>
<td align="left">0x0F</td>
<td align="left">1</td>
<td align="left">デバイスのフレンドリ名の長さ</td>
</tr>
<tr class="even">
<td align="left">234</td>
<td align="left"><p>0x43 0x6f 0x6e 0x74</p>
<p>0x6f 0x73 0x6f 0x20</p>
<p>0x50 0x72 0x69 0x6e</p>
<p>0x74 0x65 0x72</p></td>
<td align="left">15</td>
<td align="left">ユーザーに表示されるデバイスのフレンドリ名:"Contoso Printer"</td>
</tr>
</tbody>
</table>

 

## <a name="wi-fi-direct-connectivity-requirements"></a>Wi-Fi Direct 接続の要件


デバイスとクライアントには、オンになって、Wi-fi ラジオがある場合があります。 それ以外の場合は、ペアリングは失敗します。

## <a name="handling-edge-cases"></a>エッジ ケースの処理


ユーザーがデバイスをペアリングが、デバイスの一覧からデバイスを手動で削除する場合は、インストールまたはペアリングの試行になりますもう一度タップします。

ユーザーに作動の範囲を入力し、帯域外の (OOB) の情報が転送される前に突然残った場合は、デバイスが接続可能になる可能性がありますが、デバイス、PC は検索しません。 ここでは、同意、PC から UI ことはありませんし、ユーザーがもう一度タップする必要があります。 もう一度タップされたときに、デバイスが探索可能な既に場合は、探索可能にしておくし、タイムアウト期間をリセットする必要があります。

Wi-Fi Direct デバイス、Wi-fi オプションがオフにする場合、インストールは失敗します。

ユーザーが 2 つのデバイスをタップ、ほぼ同時刻に、最初に受信した OOB 情報の組み合わせのみが試行されます。

タップしてセットアップをサポートしていませんしようとすると、オペレーティング システムを実行するシステム上のデバイスをタップするまたは再接続をタップして、デバイスが接続可能モードに入る可能性がありますが、ペアリングは行われません。 ユーザーは、Bluetooth のペアリングの UI を使用し、[ペアリング] ボタンを使用して、ペアリングを開始する必要があります。

 

 
## <a name="related-topics"></a>関連トピック
 [NFC デバイス ドライバー インターフェイス (DDI) リファレンス](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
 
