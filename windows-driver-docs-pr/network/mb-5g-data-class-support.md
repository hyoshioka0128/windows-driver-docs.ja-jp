---
title: MB 5G データ クラスのサポート
description: MB 5G データ クラスのサポート
ms.assetid: 16531A63-76EC-4722-8817-FA8DB3B2B82F
keywords:
- MB 5G data クラスサポート、Mobile ブロードバンド5G データクラスのサポート
ms.date: 04/17/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 94376ceae726603ccbbe4edfa3a56db87968861d
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557739"
---
# <a name="mb-5g-data-class-support"></a>MB 5G データ クラスのサポート

## <a name="terminology"></a>用語

このトピックでは、次の用語を使用します。

| 用語 | 定義 |
| --- | --- |
| NR | 新しいラジオ。 NR は、5G を参照するときに3GPP で使用される用語です。 |
| MBB | モバイルブロードバンド。 |
| EPC | 強化されたパケットコア。 3GPP で、LTE コアネットワークを参照するときに使用される用語。 |
| NGC | 次世代コア。 5G コアネットワークを参照するときに3GPP で使用される用語です。 EPC に相当する NR。 |
| DC | デュアル接続。 ネットワークは、lte と 5G NR の両方をサポートできます。これには、デバイスが LTE と NR に同時に接続しているデュアル接続が含まれます。 |
| SA | スタンドアロン5G。 は、任意の NGC ベースの NR ネットワークを参照します。 |
| NSA | 非スタンドアロン5G。 EPC ベースの NR ネットワークを参照します。 |
| gNB | NR エアインターフェイスと、NGC への接続をサポートする NR ラジオベースステーション。 |
| RAT | 無線アクセステクノロジ。 |

## <a name="overview"></a>概要

Windows 10 バージョン1903は、IHV パートナーによる 5G mobile ブロードバンドドライバー開発のプレビューリリースをサポートするための、Windows の最初のバージョンです。 名前*5G*は、 [3GPP Release 15 仕様](https://www.3gpp.org/release-15)で導入された新しいラジオ (NR) のフレンドリ名です。 NR は標準の包括的なセットであり、既存の第4世代の LTE テクノロジに真の長期的な進化を提供することを前提としています。これは、narrowband からウルトラブロードバンドまで、および公称からミッションクリティカルな待ち時間の要件まで、すべての携帯電話通信のニーズに対応できる可能性があることを意味します。 テクノロジとして、5G は10年の長い時間枠を超えて開発することが期待されています。 

このトピックでは、Windows 10 バージョン1903で最初にリリースされた MBIM 拡張機能について説明します。これにより、ハードウェアパートナーは、5G "非スタンドアロン" EPC ベースの NR ネットワークに対するデータクラスサポート (eMBB) を使用して MBB ドライバーを開発できます。 5G のスループットと商用化の要件に対するデータプレーンのサポートと有効化は、この Windows リリースには含まれていません。このトピックでは説明しません。 

## <a name="windows-5g-mbim-interface-extension"></a>Windows 5G MBIM インターフェイス拡張機能

### <a name="mbim-interface"></a>MBIM インターフェイス

Windows 10 バージョン1903の時点で、全体の5G はまだ開発中です。 ネットワーク展開の観点からは、5G は次の2つの主要なフェーズで展開されることが想定されています。 

* フェーズ1では、ほとんどのモバイルネットワークオペレーターが、既存の LTE 無線および EPC コアの展開に 5G radio を追加して5G を展開することが想定されています。これは一般的に "非スタンドアロン 5G" ネットワークです。  

* フェーズ2では、モバイルネットワークオペレーターは、EPCs と NGCs を交換し、5G radio の展開を並行して使用して、真の "スタンドアロン" または NR ベースの5G ネットワークを有効にすることが想定されています。 フェーズ2のインターフェイス拡張は、このトピックまたは Windows リリースではスコープに含まれていません。 

基本フェーズ1のネットワーク要件をサポートするインターフェイス拡張、または "非スタンドアロン" EPC based5G ネットワークは、Windows 10 バージョン1903で導入されました。 拡張可能で、レガシモデムと完全に下位互換性を確保するために、新しい Microsoft MBIM 拡張バージョン (2.0) が導入されました。 

新しい Microsoft MBIM extesnion バージョンが必要なのは、 [mbim 1.0 の正誤仕様](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)には、省略可能な cid を追加して提供するためのメカニズムがありますが、既存の cid (新しいペイロードまたは変更されたペイロード) を変更したり、オプションの cid では対応できない側面を変更したりするためのメカニズム 各ペイロードは、固定サイズのメンバーまたは動的なサイズ (オフセット/サイズのペア) のメンバーで構成されます。 1つまたは複数の動的にサイズ設定されたメンバーが存在する場合、最後のメンバーには可変サイズのバッファーがあります。  

この仕様では、MBIM のリリースバージョンと拡張機能のリリースバージョンを MBIM デバイスに提供するために、ホストの新たな CID も追加されています。 フィールドに既に存在するレガシドライバーの場合、この CID は省略可能であるため、下位互換性は完全に維持されます。  詳細については、「 [Mbim 拡張機能のリリース 2.0](#mbim-extensions-release-20---5g-nonstandalone-epc-based-option-3-network-support)ネットワークサポート」を参照してください。 

### <a name="ndis-interface"></a>NDIS インターフェイス

NDIS では、NDIS_HEADER のリビジョン番号がサポートされています。 これにより、新しいメンバーを OID メッセージに追加することができます。この場合、NDIS は[OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)でオプションのサービスキャップテーブルを使用します。

5G data クラスのサポートのために、次の NDIS Oid とそのデータ構造が更新されました。

- [OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)
- [OID_WWAN_REGISTER_STATE](oid-wwan-register-state.md)
- [OID_WWAN_PACKET_SERVICE](oid-wwan-packet-service.md)
- [OID_WWAN_SIGNAL_STATE](oid-wwan-signal-state.md)

これらの Oid の同等の MBIM CID メッセージについては、このトピックの次のセクションで説明します。

## <a name="mbim-extensions-release-20---5g-nonstandalone-epc-based-option-3-network-support"></a>MBIM 拡張機能リリース 2.0-5G nonstandalone (EPC ベースのオプション 3) ネットワークサポート

[Mbim 1.0 のエラッタ仕様](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)には、新しいペイロードまたは変更されたペイロードで既存の cid を変更するメカニズムがありません。 Windows 10、バージョン1903では、5G をサポートするためにインターフェイスを拡張するために mbim 1.0 拡張2.0 が導入されています。

### <a name="versioning-scheme"></a>バージョン管理スキーム

> [!NOTE]
> このセクションでは、 *Mbimex バージョン*という用語は Mbim 拡張機能のリリース番号を意味します。

ホストは、次の2つの方法でデバイスの MBIMEx バージョンを学習します。

1. MBIM 拡張機能記述子。
2. デバイスがサポートし、サポートを宣言している場合は、オプションの MBM_CID_VERSION メッセージ。

これらの2つが異なる場合は、デバイスがホストに列挙されたままになっている期間の MBIMEx バージョンが上位のバージョンによって決定されます。 MBIMEx の上位バージョンは、デバイスが発表した*MBIMEx バージョン*と呼ばれます。 デバイスによって発表された MBIMEx バージョンは、デバイスがサポートしている最も高い MBIMEx バージョンである、ネイティブ MBIMEx バージョンよりも低くなる可能性があります。 デバイスは、MBIM_CID_VERSION メッセージのみを使用して、ホストの MBIMEx バージョンを明示的に調べることができます。

どのリリースでも、ホストは、デバイス初期化シーケンスの先頭に MBIM_CID_DEVICE_SERVICES を使用して、サポートされているサービスと Cid のデバイスを常に照会します。 デバイスが MBIM_CID_VERSION をサポートし、MBIM_CID_DEVICE_SERVICE クエリ応答でそのサポートをアドバタイズする場合、MBIM_CID_VERSION を認識しないホスト、または2.0 より低い MBIMEx バージョンを持つホストは、それを無視します。 一方、MBIM_CID_VERSION を認識し、ネイティブ MBIMEx バージョンの2.0 以上を持つホストは、ホストのネイティブ MBIMEx バージョンを使用してデバイスに MBIM_CID_VERSION メッセージを送信します。 CID は、MBIM_CID_DEVICE_SERVICES 応答を受け取った後にデバイスに送信される最初の CID です。

MBIM_CID_DEVICE_SERVICES クエリに応答した後に、デバイスがホストから最初に受信した CID として MBIM_CID_VERSION を受け取ると、そのホストの MBIMEx バージョンがデバイスに認識されます。 MBIM_CID_DEVICE_SERVICES クエリに応答した後、デバイスがホストから他の CID を最初に受信した CID として受信した場合、デバイスはホストのネイティブ MBIMEx バージョンが1.0 であると想定します。

機能強化された MBIMEx バージョンは、すべての下位 MBIMEx バージョンのスーパーセットになります。 ホストは、ホストのネイティブ MBIMEx バージョンで、またはその下位に発表された MBIMEx バージョンを持つすべてのデバイスをサポートします。 デバイスが発表した MBIMEx のバージョンがホストのネイティブ MBIMEx バージョンよりも高い場合、ホストはデバイスをサポートすることを想定していません。このような状況では、ホストの正確な動作は未定義です。

以前のホストとの連携を予定しているデバイスは、MBIM 拡張機能記述子に含まれる MBIMEx バージョン1.0 またはデバイスの動作を想定している最小のホスト MBIMEx バージョンを最初にアドバタイズする必要があります。 ホストが MBIM_CID_VERSION を送信し、ホストのデバイスが最初にアドバタイズしたものよりも多い MBIMEx バージョンがある場合、デバイスは MBIM_CID_VERSION、ホストのネイティブ MBIMEx バージョンとデバイスのネイティブ MBIMEx バージョンよりも小さい MBIMEx バージョンを示す必要があります。

> [!NOTE]
> たとえば、デバイスは MBIMEx バージョン2.0 をサポートしていますが、MBIMEx 2.0 をサポートしていない古いバージョンの OS を使用することを意図しています。 デバイスは最初に、USB 記述子で MBIMEx バージョン1.0 をアドバタイズし、オプションの MBIM_CID_VERSION のサポートをアドバタイズします。 Windows 10 バージョン1803を実行しているホストに挿入された場合、ホストは MBIM_CID_VERSION を認識せず、デバイスに MBIM_CID_VERSION を送信しません。 ホストに対して、デバイスの MBIMEx バージョンは1.0 です。 ホストは、初期化シーケンスで他の Cid の送信を続けます。 MBIM_CID_VERSION 以外の Cid を受信すると、そのホストが MBIMEx バージョン1.0 をサポートしていることがデバイスに認識されます。 両方の側が MBIMEx バージョン1.0 に準拠しています。 その後、Windows 10 バージョン1903を実行しているホストに、ネイティブ MBIMEx バージョン2.0 で同じデバイスが挿入されると、ホストはデバイスに MBIM_CID_VERSION を送信し、ホストのネイティブ MBIMEx バージョンが2.0 であることを通知します。 デバイスは、デバイスの発表された MBIMEx バージョン2.0 を使用して MBIM_CID_VERSION 返送します。 そこから、両方の側が MBIMEx バージョン2.0 に準拠します。

次の表は、3つの仮想ホストと3つの仮定のデバイス (それぞれにネイティブの MBIMEx バージョンが記載されています) がある互換性マトリックスを示しています。 デバイスは、最初に、USB 記述子で MBIMEx バージョン1.0 をアドバタイズします。 このマトリックスは、各デバイスが各ホストでどのように動作するかを示しています。

| デバイス (下記)/ホスト (右) | Windows 10 バージョン1809またはそれ以前 (ネイティブ MBIMEx バージョン 1.0) | Windows 10 バージョン1903以降 (MBIMEx バージョン 2.0) |
| --- | --- | --- |
| 4G デバイス <p>ネイティブ MBIMEx バージョン1.0</p> | デバイスは、最初に MBIMEx 1.0 をアドバタイズします。 MBIM_CID_VERSION exchange はありません。 互換性のあるデバイスとホスト。 MBIMEx バージョン1.0 で既定で動作します。 | デバイスは、最初に MBIMEx 1.0 をアドバタイズします。 MBIM_CID_VERSION exchange はありません。 ホストは、MBIMEx 1.0 を使用してデバイスで動作します。 |
| 5G NSA デバイス <p>ネイティブ MBIMEx バージョン2.0</p> | デバイスは、最初に MBIMEx 1.0 をアドバタイズします。 MBIM_CID_VERSION exchange はありません。 デバイスは、ホストが MBIMEx 1.0 を持っていることを認識し、MBIMEx 1.0 に進みます。 | デバイスは、最初に MBIMEx 1.0 をアドバタイズします。 ホストが MBIM_CID_VERSION を送信して、ホストが MBIMEx 2.0 をサポートしていることをデバイスに通知します。 デバイスは MBIMEx 2.0 で応答します。 両側は MBIMEx 2.0 を使用します。 |

次の表に、MBIMEx バージョン2.0 で変更された既存のすべての Cid と、その変更後のペイロードを示します。 これらの Cid に記載されていないすべてのペイロードと、表に記載されていない他のすべての Cid は、MBIMEx バージョン1.0 から引き継がれ、変更はありません。 

| CID | ペイロード |
| --- | --- |
| MBIM_CID_REGISTER_STATE | MBIM_REGISTRATION_STATE_INFO_V2 |
| MBIM_CID_PACKET_SERVICE | MBIM_PACKET_SERVICE_INFO_V2 |
| MBIM_CID_SIGNAL_STATE | MBIM_SIGNAL_STATE_INFO_V2 |

## <a name="mbim-service"></a>MBIM サービス

| [サービス名] | UUID | UUID の値 |
| --- | --- | --- |
| Microsoft 基本 IP 接続拡張機能 | UUID_BASIC_CONNECT_EXTENSIONS | 3D01DCC5-FEF5-4D05-9D3A-BEF7058E9AAF |

## <a name="mbim_cid_version"></a>MBIM_CID_VERSION

MBIM Microsoft extension 2.0 以降をサポートする MBB ドライバーの場合、MBIM_CID_VERSION は、ホストとデバイス間で MBIM のバージョン情報を交換するための必須のコマンドです。 この CID を認識しないドライバーが含まれている市場内のデバイスの場合、ホストは下位互換性を前提として提供します。

ホストは、デバイスでサポートされている場合、このコマンドをクエリとして送信します。 このクエリには、ホストが現在サポートしている MBIM リリース番号と MBIM 拡張機能のリリース番号が含まれています。

デバイス側では、デバイスは、[バージョン管理スキーム](#versioning-scheme)で定義された規則に基づいて、発表された mbim リリース番号と Mbim 拡張機能のリリース番号を調整し、ホストに応答として送信します。

このコマンドは、**基本接続拡張機能**サービスで定義されています。

| CID | コマンドコード | UUID |
| --- | --- | --- |
| MBIM_CID_VERSION | 15 | 3d01dcc5-fef5-4d05-0d3abef7058e9aaf |

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 適用なし | MBIM_VERSION_INFO | 適用なし |
| 応答 | 適用なし | MBIM_VERSION_INFO | 適用なし |

### <a name="query"></a>クエリ

ホストのネイティブ MBIM リリース番号と MBIM 拡張機能のリリース番号をデバイスに通知します。 InformationBuffer には、次の MBIM_VERSION_INFO 構造が含まれています。

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 2 | bcdMBIMVersion | UINT16 | BCD 内の送信者の MBIM リリース番号。ビット7と8の間に暗黙的な小数点があります。 たとえば、`0x0100 == 1.00 == 1.0` のようにします。 これはリトルエンディアン定数であるため、バイトは0x00、0x01 になります。 |
| 2 | 2 | bcdMBIMExtendedVersion | UINT16 | MBIM 拡張機能では、BCD 内の送信者の数がリリースされています。ビット7と8の間には暗黙的な小数点があります。 たとえば、`0x0100 == 1.00 == 1.0` のようにします。 これはリトルエンディアン定数であるため、バイトは0x00、0x01 になります。 |

### <a name="set"></a>オン

適用不可。

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer に MBIM_VERSION_INFO 構造体が含まれています。

### <a name="unsolicited-events"></a>一方的なイベント

適用不可。

### <a name="status-codes"></a>状態コード

この CID は、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)のセクション9.4.5 で定義されている汎用ステータスコードのみを使用します。

## <a name="mbim_cid_ms_device_caps_v2"></a>MBIM_CID_MS_DEVICE_CAPS_V2

この CID は、 [MB のマルチ SIM 操作](mb-multi-sim-operations.md#mbim-interface-update-for-multi-sim-operations)で定義されているものと同じです。これ自体は、 [mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)のセクション10.5.1 で定義されている MBIM_CID_MS_DEVICE_CAPS の拡張機能です。 MBIM 拡張機能のリリース2.0 では、MBIM_DATA_CLASS テーブルで定義されている新しいデータクラスを使用して、デバイスが5G 機能を報告できるようにします。 MBIMDataClass5G_NSA は、デバイスが[3GPP ts 37.340](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3198)で定義されている5G 非スタンドアロン (NSA) をサポートしていることを示し、MBIMDataClass5G_SA は、デバイスが 3GPP ts 37.340 でも定義されている 5G STANDALONE (SA) をサポートしていることを示します。

デバイスで両方の新しいデータクラスがサポートされている場合は、両方のビットを設定する必要があります。

## <a name="mbim_data_class"></a>MBIM_DATA_CLASS

| 種類 | マスク |
| --- | --- |
| MBIMDataClassNone | 0h |
| MBIMDataClassGPRS | 1h |
| MBIMDataClassEDGE | 後半 |
| MBIMDataClassUMTS | 4h |
| MBIMDataClassHSDPA | 8h |
| MBIMDataClassHSUPA | 10h |
| MBIMDataClassLTE | 20h |
| **MBIMDataClass5G_NSA** | **40h** |
| **MBIMDataClass5G_SA** | **80h** |
| 予約済み | 100h-8000h |
| MBIMDataClass1XRTT | 10000h |
| MBIMDataClass1XEVDO | 20000h |
| MBIMDataClass1XEVDORevA | 40000h |
| MBIMDataClass1XEVDV | 80000h |
| MBIMDataClass3XRTT | 100000h |
| MBIMDataClass1XEVDORevB | 200000h |
| MBIMDataClassUMB | 400000h |
| 予約済み | 800000-40000000h |
| MBIMDataClassCustom | 80000000h |

## <a name="mbim_cid_register_state"></a>MBIM_CID_REGISTER_STATE

このコマンドは、 [Mbim 仕様のリビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)で既に定義されている MBIM_CID_REGISTER_STATE CID の拡張機能です。 この拡張機能では、応答構造のために**Preferreddataclasses**新しいメンバーが追加されます。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_REGISTRATION_STATE | Empty | 適用なし |
| 応答 | MBIM_REGISTRATION_STATE_INFO_V2 | MBIM_REGISTRATION_STATE_INFO_V2 | MBIM_REGISTRATION_STATE_INFO_V2 |

### <a name="query"></a>クエリ

InformationBuffer が null で、InformationBufferLength が0です。

### <a name="set"></a>オン

登録状態を設定します。 この情報は、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)で説明されているものと同じです。

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer には、次の MBIM_REGISTRATION_STATE_INFO_V2 構造が含まれています。 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)のセクション10.5.10.6 で定義されている MBIM_REGISTRATION_STATE_INFO 構造と比較すると、次の構造には新しい**preferreddataclasses**フィールドがあります。 ここに記載されていない限り、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の表10-55 のフィールドの説明は、この構造に適用されます。

#### <a name="mbim_registration_state_info_v2"></a>MBIM_REGISTRATION_STATE_INFO_V2

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NwError | UINT32 | ネットワーク固有のエラー。 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の表10-44 は、nwerror の原因コードを文書にしたものです。 |
| 4 | 4 | RegisterState | MBIM_REGISTER_STATE | [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の表10-46 を参照してください。 |
| 8 | 4 | RegisterMode | MBIM_REGISTER_MODE | [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の表10-47 を参照してください。 |
| 12 | 4 | AvailableDataClass | UINT32 | 登録されているネットワーク上で、デバイスが登録されているセルに対してサポートされているデータクラスを表す[MBIM_DATA_CLASS](#mbim_data_class)の値のビットマップ。 <p>**Registerstate**が**Mbimregisterstatehome**、 **MBIMRegisterStateRoaming**、または**mbimregisterstatehome**でない場合、この値は MBIMDataClassNone に設定されます。 </p> |
| 16 | 4 | CurrentCellularClass | MBIM_CELLULAR_CLASS | マルチモード関数に使用されている現在の携帯ネットワーククラスを示します。 詳細については、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の表10-8 を参照してください。 <p>シングルモード関数の場合、これは MBIM_CID_DEVICE_CAPS で報告された携帯ネットワーククラスと同じです。 マルチモード関数の場合、CDMA から GSM への移行またはその逆の切り替えは、更新された**Currentcellularclass**によって示されます。 </p> |
| 20 | 4 | ProviderIdOffset | OFFSET | この構造体の先頭から計算された、ネットワークプロバイダー id を表す**ProviderId**という数値 (0-9) 文字列へのオフセット (バイト単位)。 <p>GSM ベースのネットワークの場合、この文字列は、3桁の携帯電話番号 (MCC) と2つまたは3桁のモバイルネットワークコード (MNC) を連結したものです。 GSM ベースのキャリアには複数の MNC があり、したがって複数の**ProviderId**がある場合があります。</p><p>CDMA ベースのネットワークの場合、この文字列は5桁のシステム ID (SID) です。 一般に、CDMA ベースのキャリアには複数の SID があります。 通常、通信事業者は、各市場に対して1つの SID を持ちます。この SID は、通常、米国内のメトロポリタン統計領域 (MSA) などの規制によって地域内で地理的に分割されています。 この情報が利用できない場合は、CDMA ベースのデバイスで MBIM_CDMA_DEFAULT_PROVIDER_ID を指定する必要があります。</p><p>クエリ要求を処理し、登録状態が自動登録モードである場合、このメンバーには、デバイスが現在関連付けられているプロバイダー ID (該当する場合) が含まれます。 登録状態が手動登録モードの場合、このメンバーには、デバイスの登録が要求されているプロバイダー ID が含まれます (プロバイダーが使用できない場合でも)。</p><p>セット要求を処理するときに、登録状態が手動モードである場合、これには、デバイスの登録に使用するホストによって選択されたプロバイダー ID が含まれます。 登録状態が自動登録モードの場合、このパラメーターは無視されます。</p><p>プロバイダー ID が使用できない場合は、CDMA 1xRTT プロバイダーを MBIM_CDMA_DEFAULT_PROVIDER_ID に設定する必要があります。</p> |
| 24 | 4 | ProviderIdSize | サイズ (0.. 12) | **ProviderId**のサイズ (バイト単位)。 |
| 28 | 4 | ProviderNameOffset | OFFSET | この構造体の先頭から計算された、ネットワークプロバイダーの名前を表す**ProviderName**という文字列へのオフセット (バイト単位)。 このメンバーは、最大で MBIM_PROVIDERNAME_LEN 文字までに制限されています。 <p>GSM ベースのネットワークの場合、国のイニシャルとモバイルネットワーク名 (PCCI&N) の推奨されるプレゼンテーションが20文字を超えると、デバイスはネットワーク名を省略する必要があります。</p><p>このメンバーは、ホストが優先プロバイダー一覧を設定するときに無視されます。 デバイスでは、この情報が含まれていないデバイスに対して NULL 文字列を指定する必要があります。</p> |
| 32 | 4 | ProviderNameSize | サイズ (0 ~ 40) | **ProviderName**のサイズ (バイト単位)。 |
| 36 | 4 | RoamingTextOffset | OFFSET | デバイスがローミングされていることをユーザーに通知するために、この構造体の先頭から計算された**RoamingText**という文字列へのオフセット (バイト単位)。 このメンバーは、最大で63文字までに制限されています。 このテキストは、登録状態が MBIMRegisterStatePartner または MBIMRegisterStateRoaming の場合に、ユーザーに追加情報を提供する必要があります。 このメンバーは省略可能です。 |
| 40 | 4 | RoamingTextSize | サイズ (0 ~ 126) | **RoamingText**のサイズ (バイト単位)。 |
| 44 | 4 | RegistrationFlag | MBIM_REGISTRATION_FLAGS | [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の各テーブル10-48 に設定されているフラグ。 |
| 48 | 4 | PreferredDataClass | UINT32 | デバイス上の有効なデータクラスを表す[MBIM_DATA_CLASS](#mbim_data_class)の値のビットマップ。 デバイスは、有効になっているデータクラスを使用してのみ動作できます。 |
| 動的 | 4 | DataBuffer | DATABUFFER | **ProviderId**、 **ProviderName**、および**RoamingText**を含むデータバッファー。 |

### <a name="unsolicited-events"></a>一方的なイベント

通知には MBIM_REGISTRATION_STATE_INFO_V2 構造が含まれています。

### <a name="status-codes"></a>状態コード

この CID は、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)のセクション9.4.5 で定義されている汎用ステータスコードのみを使用します。

## <a name="mbim_cid_packet_service"></a>MBIM_CID_PACKET_SERVICE

このコマンドは、 [Mbim 仕様のリビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)で定義されている既存の MBIM_CID_PACKET_SERVICE の拡張機能です。

この拡張機能は、応答構造に**FrequencyRange**という名前の新しいメンバーを追加し、その目的を明確にするために**HighestAvailableDataClass**メンバーの名前を**CurrentDataClass**に変更しました。

**CurrentDataClass**は、デバイスが現在登録されている無線アクセステクノロジ (RAT) を示します。 これには、 [MBIM_DATA_CLASS](#mbim_data_class)からの1つの値が含まれます。

**FrequencyRange**は、デバイスが現在使用している頻度の範囲を示します。 これは、MBIMDataClass5G_NSA または MBIMDataClass5G_SA ビットが設定されていることを**CurrentDataClass**フィールドが示している場合にのみ有効です。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_PACKET_SERVICE | Empty | 適用なし |
| 応答 | MBIM_PACKET_SERVICE_INFO_V2 | MBIM_PACKET_SERVICE_INFO_V2 | MBIM_PACKET_SERVICE_INFO_V2 |

### <a name="query"></a>クエリ

InformationBuffer が null で、InformationBufferLength が0です。

### <a name="set"></a>オン

Set コマンドの情報については、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)で説明されています。

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer に MBIM_PACKET_SERVICE_INFO_V2 構造体が含まれています。 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)のセクション10.5.10.6 で定義されている MBIM_PACKET_SERVICE_INFO 構造と比較して、この新しい構造体には**CurrentDataClass**フィールドと**FrequencyRange**フィールドがあります。 ここに記載されていない限り、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の表10-55 のフィールドの説明がここに適用されます。

#### <a name="mbim_packet_service_info_v2"></a>MBIM_PACKET_SERVICE_INFO_V2

| Offset | サイズ | フィールド | Type | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | NwError | UINT32 | ネットワーク固有のエラー。 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の表10-44 は、nwerror の原因コードを文書にしたものです。 |
| 4 | 4 | PacketServiceState | MBIM_PACKET_SERVICE_STATE | [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の表10-53 を参照してください。 | 
| 8 | 4 | CurrentDataClass | MBIM_DATA_CLASS | [MBIM_DATA_CLASS](#mbim_data_class)に従って指定された、現在のセルの現在のデータクラス。 関数が接続パケットサービスの状態でない場合、関数はこのメンバーを MBIMDataClassNone に設定する必要があります。 HSPA (つまり、HSUPA と HSDPA) と 5G DC を除き、関数はこのメンバーを1つの MBIM_DATA_CLASS 値に設定します。 HSPA data services の場合、関数は MBIMDataClass HSDPA と MBIMDataClassHSUPA のビットごとの OR を指定します。 HSDPA はサポートされているが HSDPA はサポートしていないセルの場合、HSDPA のみが示されます (アップリンクデータの UMTS データクラス)。 現在のデータクラスが変更されるたびに、 **CurrentDataClass**の新しい値を示す通知が関数によって送信されます。 |
| 12 | 8 | UplinkSpeed | UINT64 | アップリンクビットレートが1秒あたりのビット数で格納されます。 |
| 20 | 8 | ダウンリンク速度 | UINT64 | ダウンリンクビットレートが1秒あたりのビット数で格納されます。 |
| 38 | 4 | FrequencyRange | MBIM_FREQUENCY_RANGE | デバイスが現在使用している頻度の範囲を表す[MBIM_FREQUENCY_RANGE](#mbim_frequency_range)の値のビットマスク。 これは、 **CurrentDataClass**が MBIMDataClass5G_NSA か MBIMDataClass5G_SA のいずれかである場合にのみ有効です。 |

#### <a name="mbim_frequency_range"></a>MBIM_FREQUENCY_RANGE

次の列挙体は、前の MBIM_PACKET_SERVICE_INFO_V2 構造体の値として使用されます。

| 種類 | 値 | 説明|
| --- | --- | --- |
| MBIMFrequencyRangeUnknown | 0 | システム型が5G でない場合は。 |
| MBIMFrequencyRange1 | 1 | [3GPP TS 38.101-1](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3283) (サブ 6g) の頻度の範囲 1 (FR1)。 |
| MBIMFrequencyRange2 | 2 | FR2 [3GPP TS 38.101](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3284) (mmwave)。 |
| MBIMFrequencyRange1AndRange2 | 3 | FR1 と FR2 の両方のキャリアが接続されている場合。 |

### <a name="unsolicited-events"></a>一方的なイベント

通知には MBIM_PACKET_SERVICE_INFO_V2 構造が含まれています。

### <a name="status-codes"></a>状態コード

この CID は、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)のセクション9.4.5 で定義されている汎用ステータスコードのみを使用します。

## <a name="mbim_cid_signal_state"></a>MBIM_CID_SIGNAL_STATE

この CID は MBIM_CID_SIGNAL_STATE の拡張機能であり、シグナル状態の条件に RSRP と SNR を導入しています。 この新しい拡張機能は、デバイスで MBIM 拡張機能バージョン2.0 のサポートが指定されている場合にのみ有効です。 モデムが MBIMDataClass5G_ (N) SA データクラスをサポートしている場合、この拡張機能は必須です。

RSRP および SNR フィールドは、対応する SystemType が MGBIMDataClassLTE または MBIMDataClass5G_ (N) SA の場合にのみ有効です。 モデムが RSRP や SNR を報告する場合は、RSSI フィールドの値を**99**に設定する必要があります。

対応する SystemType が MBIMDataClass5G_ (N) SA の場合、RSRP フィールドは必須であり、SNR フィールドは省略可能です。 対応する SystemType が MBIMDataClassLTE の場合、RSRP および SNR フィールドは省略可能であり、RSSI フィールドを代わりに使用できます。 この場合、RSRP および SNR フィールドを省略するには、 **Rsrpsnroffset**と**rsrpsnの**両方のメンバーにゼロ (**0**) の値を設定します。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_SIGNAL_STATE | Empty | 適用なし |
| 応答 | MBIM_SIGNAL_STATE_INFO_V2 | MBIM_SIGNAL_STATE_INFO_V2 | MBIM_SIGNAL_STATE_INFO_V2 |

### <a name="query"></a>クエリ

InformationBuffer が null で、InformationBufferLength が0です。

### <a name="set"></a>オン

Set コマンドの情報については、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)で説明されています。

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer には、次の MBIM_SIGNAL_STATE_INFO_V2 構造が含まれています。

#### <a name="mbim_signal_state_info_v2"></a>MBIM_SIGNAL_STATE_INFO_V2

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | Rssi | UINT32 | [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の表10.58 を参照してください。 |
| 4 | 4 | ErrorRate | UINT32 | [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の表10.58 を参照してください。 |
| 8 | 4 | SignalStrengthInterval | UINT32 | レポート間隔 (秒単位)。 |
| 12 | 4 | RssiThreshold | UINT32 | レポートをトリガーする RSSI のコード化された値の違い。 これが問題でない場合は、0xFFFFFFFF を使用します。 |
| 16 | 4 | ErrorRateThreshold | UINT32 | レポートをトリガーする ErrorRate コード化された値の差。 これが問題でない場合は、0xFFFFFFFF を使用します。 |
| 20 | 4 | RsrpSnrOffset | OFFSET | この構造体の先頭から、RSRP および SNR シグナリング情報を格納しているバッファーへのオフセット (バイト単位)。 このメンバーは、RSRP および SNR シグナリング情報が使用できない場合に**NULL**にすることができます。 |
| 24 | 4 | RsrpSnrSize r) | SIZE | MBIM_RSRP_SNR_INFO 構造体の形式で指定された RSRP および SNR のシグナル化情報を格納しているバッファーのサイズ (バイト単位)。 |
|   | 4 | DataBuffer | DATABUFFER | MBIM_RSRP_SNR 構造体。 |

#### <a name="mbim_rsrp_snr"></a>MBIM_RSRP_SNR

次の MBIM_RSRP_SNR 構造は、MBIM_SIGNAL_STATE_INFO_V2 構造体の**DataBuffer**で使用されます。

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount | UINT32 | この要素の後に続く RSRP_SNR エントリの数。 |
| 4 | 4 | DataBuffer | DATABUFFER | RSRP_SNR レコードの配列。それぞれが MBIM_RSRP_SNR_INFO 構造体として指定されます。 |

#### <a name="mbim_rsrp_snr_info"></a>MBIM_RSRP_SNR_INFO

MBIM_RSRP_SNR 構造体の**DataBuffer**では、次の MBIM_RSRP_SNR_INFO 構造体の配列が使用されます。

<table>
    <tr>
        <th>Offset</th>
        <th>> サイズ</th>
        <th>フィールド</th>
        <th>Type</th>
        <th>説明</th>
    </tr>
    <tr>
        <td>0</td>
        <td>4</td>
        <td>RSRP</td>
        <td>UINT32</td>
        <td>
            <table>
                <tr>
                    <th>DBm の RSRP 値</th>
                    <th>コード化された値 (最小値 = 0、最大値 = 126)</th>
                </tr>
                <tr>
                    <td>-156 未満</td>
                    <td>0</td>
                </tr>
                <tr>
                    <td>-155 未満</td>
                    <td>1</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>-138 未満</td>
                    <td>18</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>-45 未満</td>
                    <td>111</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>-31 未満</td>
                    <td>125</td>
                </tr>
                <tr>
                    <td>-31 以上</td>
                    <td>126</td>
                </tr>
                <tr>
                    <td>不明または検出不可能</td>
                    <td>127</td>
                </tr>
            </table>
        </td>
    </tr>
    <tr>
        <td>4</td>
        <td>4</td>
        <td>SNR</td>
        <td>UINT32</td>
        <td>
            <table>
                <tr>
                    <th>DB 内の SNR 値</th>
                    <th>コード化された値 (最小値 = 0、最大値 = 127)</th>
                </tr>
                <tr>
                    <td>-23 未満</td>
                    <td>0</td>
                </tr>
                <tr>
                    <td>-22.5 未満</td>
                    <td>1</td>
                </tr>
                <tr>
                    <td>-22 未満</td>
                    <td>2</td>
                </tr>
                <tr>
                    <td>-21.5 未満</td>
                    <td>3</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>39.5 未満</td>
                    <td>125</td>
                </tr>
                <tr>
                    <td>40未満</td>
                    <td>126</td>
                </tr>
                <tr>
                    <td>40以上</td>
                    <td>127</td>
                </tr>
                <tr>
                    <td>不明または検出不可能</td>
                    <td>128</td>
                </tr>
            </table>
        </td>
    </tr>
    <tr>
        <td>8</td>
        <td>4</td>
        <td>RSRPThreshold</td>
        <td>UINT32</td>
        <td>古い (キャッシュされた) RSRP 値と新しく計算された RSRP 値の間のしきい値を定義します。 絶対差がしきい値よりも大きい場合、デバイスは要請されていないイベントをトリガーします。 単位は 1 dBm です。 0に設定した場合は、デバイス関数の既定の動作を使用します。 0xFFFFFFFF に設定されている場合は、イベントをトリガーするためにこれを使用しないでください。 指定されたしきい値がデバイスでサポートされていない場合は、サポートされる最大しきい値が返されます。</td>
    </tr>
    <tr>
        <td>12</td>
        <td>4</td>
        <td>SNRThreshold</td>
        <td>UINT32</td>
        <td>古い (キャッシュされた) SNR 値と新しく計算された SNR 値の間のしきい値を定義します。 絶対差がしきい値よりも大きい場合、デバイスは要請されていないイベントをトリガーします。 単位は 1 dB です。 0に設定した場合は、デバイス関数の既定の動作を使用します。 0xFFFFFFFF に設定されている場合は、イベントをトリガーするためにこれを使用しないでください。 指定されたしきい値がデバイスでサポートされていない場合は、サポートされる最大しきい値が返されます。</td>
    </tr>
    <tr>
        <td>16</td>
        <td>4</td>
        <td>SystemType</td>
        <td>MBIM_DATA_CLASS</td>
        <td>シグナル状態情報が有効であるシステム型を示します。 このメンバーは<a href="#mbim_data_class">MBIM_DATA_CLASS</a>で定義されている1つの型のビットマスクです。</td>
    </tr>
</table>

### <a name="unsolicited-events"></a>一方的なイベント

通知には MBIM_SIGNAL_STATE_INFO_V2 構造が含まれています。

### <a name="status-codes"></a>状態コード

この CID は、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)のセクション9.4.5 で定義されている汎用ステータスコードのみを使用します。
