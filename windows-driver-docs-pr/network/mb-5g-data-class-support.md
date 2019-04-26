---
title: MB 5G データ クラスのサポート
description: MB 5G データ クラスのサポート
ms.assetid: 16531A63-76EC-4722-8817-FA8DB3B2B82F
keywords:
- MB 5 G データ クラスのサポート、モバイル ブロード バンド 5 G データ クラスのサポート
ms.date: 04/17/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c895a81e549bcd856ff796c1cdddd85bbbcf82d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343467"
---
# <a name="mb-5g-data-class-support"></a>MB 5G データ クラスのサポート

## <a name="terminology"></a>用語

このトピックでは、次の用語を使用します。

| 項目 | 定義 |
| --- | --- |
| NR | 新しいオプション。 NR は、5 G を参照するときに、3 gpp で使用される用語です。 |
| MBB | モバイル ブロード バンド。 |
| EPC | 強化されたパケットのコア。 LTE コア ネットワークを参照するときに、3 gpp で使用される用語です。 |
| NGC | 次世代コア。 5 G のコア ネットワークを参照するときに、3 gpp で使用される用語です。 EPC に NR 相当します。 |
| DC | デュアル接続します。 ネットワークには、LTE と 5 G デュアルの接続を使用するデバイスがある LTE と NR への同時接続を含む NR の両方をサポートできます。 |
| SA | スタンドアロン 5 G です。 オプション 2 のスタンドアロン NR を最も一般的なものには、すべての NGC ベース NR ネットワークを参照します。 |
| NSA | 非スタンドアロン 5 G です。 最も一般的なものは、オプション 3、非スタンドアロン NR、EPC ベース NR ネットワークを参照します。 |
| gNB | NR ラジオ基地局 NR エア インターフェイスと NGC への接続をサポートします。 |
| RAT | 無線アクセス テクノロジです。 |

## <a name="overview"></a>概要

Windows 10、バージョンが 1903 は IHV パートナーの 5 G モバイル ブロード バンドのドライバーをサポートするために最初の Windows リリースです。 名前*5 G*フレンドリ名の新しいオプション (NR) で導入されたは、 [3 gpp リリース 15 仕様](http://www.3gpp.org/release-15)します。 NR は包括的な設定が想定する真の長期的な進化を提供する標準の既存の第 4 世代 LTE テクノロジ、超ブロード バンドをナローバンドおよびに公称からすべての携帯電話の通信ニーズをカバーする可能性があります。ミッション クリティカルな待機時間の要件。 、、のテクノロジとして 10 年間-時間の長い期間が経過する 5 G が必要です。 

このトピックでは、Windows 10、バージョンが 1903 年 nonstandalone EPC ベースのネットワークを拡張 5 G モバイル ブロード バンド (eMBB) 以上 5 G で始まる 5 G の Windows のサポートのための最初の手順について説明します。

## <a name="windows-5g-mbim-interface-extension"></a>Windows 5 G MBIM インターフェイスの拡張機能

### <a name="mbim-interface"></a>MBIM インターフェイス

Windows 10、バージョンが 1903 年の時点で 5 G 全体にまだ開発中です。 次の表は、さまざまな段階を 5 G ネットワークがデプロイされる別のネットワーク アーキテクチャのオプション (1 ~ 7) での特徴をまとめたものです。 オプション 1 では、既存 LTE モバイル ブロード バンド、これは、Windows プラットフォームでサポートされてもを表します。

![モバイル ブロード バンド 5 G のデプロイ オプション](images/mb-5g-deployment-options.png "モバイル ブロード バンド 5 G のデプロイ オプション")

以降では、2019年世界、主要なモバイル演算子 (MOs) でデプロイする、オプション 3、または"nonstandalone"(NSA) 5 G ネットワークが必要です。 NGC に基づく「スタンドアロン」(SA) オプション 2/4/5/7 ネットワーク期待されるデプロイ以降より広く 2020年にできるだけ早くします。

サポートのオプション 3 (NSA) 5 G の EPC ベースのネットワークが Windows 10、バージョンが 1903 に導入されました。 ただし、NGC ベース (SA) のネットワークは、まだ開発中です。 そのため、Windows での 5 G のサポートが容易に拡張できると、並列では、従来のモデムと完全に下位互換性です。 

[MBIM 1.0 errata 仕様](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)を追加し、省略可能な Cid を提供するためのメカニズムが新しいペイロードまたは変更されたペイロードは、既存の Cid を変更またはでは対応できないすべての変更を導入するためのメカニズムが不足していますCid の省略可能です。 MBIM 1.0 errata 仕様では、各ペイロードの固定サイズのメンバーで構成されている可能性があります。 またはオフセット/サイズ ペア メンバーを動的にサイズ変更します。 動的に規模のメンバーが存在する場合は、可変サイズのバッファーが、最後のメンバー。 重大な変更は可能な限り回避 5 G ネットワークのすべての要件をサポートするは避けではありません。

Windows 10、バージョンが 1903 がサポートのオプション 3 (NSA) 5 G を追加して、MBIM 1.0 仕様を更新は、既存の Cid に対する重大な変更を含むネットワークします。 新しい MBIM 拡張機能のリリース 2.0 は Windows 10、MBIM リリース番号と MBIM 拡張機能のリリースを MBIM デバイス番号を提供するホストを有効にする新しい CID と共にバージョン 1903 年でも追加されました。

### <a name="ndis-interface"></a>NDIS インターフェイス

NDIS は、NDIS_HEADER のリビジョン番号をサポートします。 これにより、OID メッセージに新しいメンバーを追加することが、すべてのミニポート ドライバーがバージョン番号を尊重し、新しいリビジョンが許されない。 この場合、ミニポート ドライバーのバージョンは、ドライバーでは、かどうか、OID の新しいバージョンがサポートしているかどうかに使用できます。 ただし、IHV ドライバーへの依存関係を追加、ため、代わりに NDIS テーブルを使用して、省略可能なサービスの上限で[OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)します。

5 G データ クラスのサポートを次の NDIS Oid と、データ構造が更新されました。

- [OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)
- [OID_WWAN_REGISTER_STATE](oid-wwan-register-state.md)
- [OID_WWAN_PACKET_SERVICE](oid-wwan-packet-service.md)
- [OID_WWAN_SIGNAL_STATE](oid-wwan-signal-state.md)

これらの Oid の同等の MBIM CID メッセージは、このトピックの次のセクションで説明します。

## <a name="mbim-extensions-release-20---5g-nonstandalone-epc-based-option-3-network-support"></a>MBIM 拡張機能リリース 2.0 5 G nonstandalone (EPC ベース オプション 3) ネットワークのサポート

[MBIM 1.0 errata 仕様](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)バージョンが 1903 5 G をサポートするインターフェイスを拡張する MBIM 1.0 拡張子 2.0 が導入されて新しいまたは変更されたペイロード、Windows 10 では、既存の Cid を変更するメカニズムが不足しています。

### <a name="versioning-scheme"></a>バージョン管理スキーム

> [!NOTE]
> このセクションで、用語*MBIMEx バージョン*MBIM 拡張機能のリリースの数を示します。

ホストでは、2 つの方法でデバイスの MBIMEx バージョンは学習します。

1. MBIM 拡張機能の記述子。
2. 省略可能な MBM_CID_VERSION 場合、メッセージ、デバイスが対応していることのサポートを宣言します。

これらの 2 つが異なる場合は、以降のバージョンは、デバイスは、ホストに列挙されたまま間 MBIMEx バージョンを決定します。 高い MBIMEx バージョンは、デバイスのと呼ばれます*MBIMEx バージョンを発表*します。 デバイスの発表、MBIMEx のバージョンは、デバイスをサポートする最上位の MBIMEx バージョンは、そのネイティブ MBIMEx バージョンより低くすることができます。 デバイスでは、MBIM_CID_VERSION メッセージのみを使用して、ホストの MBIMEx バージョンを明示的に学習できます。

任意のリリースでは、ホストは常に、デバイスのサポートされているサービスおよび MBIM_CID_DEVICE_SERVICES を使用して、デバイスの初期化シーケンスの先頭に Cid を照会します。 MBIM_CID_DEVICE_SERVICE クエリの応答のサポートをアドバタイズするデバイスが MBIM_CID_VERSION をサポートしている場合、MBIM_CID_VERSION が理解していないまたは MBIMEx バージョンが 2.0 より前のホストは無視されます。 一方、MBIM_CID_VERSION が理解し、ネイティブ MBIMEx バージョン 2.0 以降のホストがホストのネイティブの MBIMEx バージョンでは、デバイスに MBIM_CID_VERSION メッセージを送信し、CID が、MBIM を受信した後、デバイスに送信される最初の CID_CID_DEVICE_SERVICES 応答です。

デバイスでは、ホストから MBIM_CID_VERSION が受信最初が MBIM_CID_DEVICE_SERVICES クエリに応答した後に CID を受信すると、デバイスは、ホストの MBIMEx バージョンを認識します。 デバイスでは、ホストからその他の任意の CID が受信最初が MBIM_CID_DEVICE_SERVICES クエリに応答した後に CID を受信すると場合、デバイスが想定するホストのネイティブ MBIMEx バージョンは 1.0。

その代わりより高い MBIMEx バージョンは下位 MBIMEx バージョンのすべてのスーパー セットです。 ホストは、ホストのネイティブ MBIMEx バージョン以下で発表された MBIMEx バージョンですべてのデバイスをサポートします。 MBIMEx バージョンは、ホストのネイティブ MBIMEx バージョンよりデバイスがお知らせ、ホストがデバイスをサポートする必要はありませんし、このような状況でホストの正確な動作は未定義です。

古いホストと連携する予定のデバイスには、MBIMEx バージョン 1.0 では、または、最小ホスト MBIMEx バージョンが、デバイスが拡張機能の記述子、MBIM で、機能するため最初を提供する必要があります。 ホストが MBIM_CID_VERSION を送信および MBIM_CID_VERSION 応答には、デバイスは、その後、ホストがデバイスを最初にアドバタイズより高い MBIMEx バージョンを持っている場合、ホストのネイティブ MBIMEx バージョンのうち、小さい方まで高い MBIMEx バージョンを指定し、デバイスのネイティブ MBIMEx バージョン。

> [!NOTE]
> たとえば、デバイス MBIMEx バージョン 2.0 をサポートしますが MBIMEx 2.0 をサポートしていない OS の以前のバージョンで動作するためのものです。 デバイスは最初に MBIMEx version 1.0 での USB ディスクリプターをアドバタイズし、省略可能な MBIM_CID_VERSION のサポートをアドバタイズします。 Windows 10、バージョン 1803 を実行するホストに挿入されると、ホストは MBIM_CID_VERSION が理解していないと、MBIM_CID_VERSION をデバイスに送信しません。 ホストには、デバイスの MBIMEx バージョンは 1.0 です。 ホストは、初期化シーケンス内の他の Cid を送信し続けます。 MBIM_CID_VERSION 以外 Cid を受信すると、デバイスでは、ホストが MBIMEx バージョン 1.0 をサポートしているがわかっています。 両方の側では、MBIMEx バージョン 1.0 に準拠しているに進みます。 後で、同じデバイスが Windows 10 バージョン 1903 ネイティブ MBIMEx バージョン 2.0 の使用を実行するホストに挿入されると、ホストは、ホストのネイティブ MBIMEx バージョンが 2.0 であることを通知するデバイスに MBIM_CID_VERSION を送信します。 デバイスは、デバイスの応答に戻って MBIM_CID_VERSION 発表 MBIMEx version 2.0 を送信します。 そこから、両方の側は MBIMEx バージョン 2.0 に準拠するように進みます。

次の表では、それぞれにそのネイティブ MBIMEx バージョンが記載されている 3 つの仮想ホストと 3 つの仮想デバイスの互換性マトリックスを示します。 デバイスは、MBIMEx USB 記述子の初期段階では、バージョン 1.0 を提供します。 マトリックスは、各デバイスで各ホストの動作方法を示しています。

| モデム (下記)/OS (右) | Windows 10、バージョンは 1809 またはそれ以前 (ネイティブ MBIMEx バージョン 1.0) | Windows 10、バージョンが 1903 およびそれ以降 (MBIMEx バージョン 2.0) |
| --- | --- | --- |
| 4 G デバイス <p>ネイティブ MBIMEx バージョン 1.0</p> | デバイスは、最初に MBIMEx 1.0 をアドバタイズします。 MBIM_CID_VERSION exchange がありません。 互換性のあるデバイスとホスト。 MBIMEx version 1.0 で既定で動作します。 | デバイスは、最初に MBIMEx 1.0 をアドバタイズします。 MBIM_CID_VERSION exchange がありません。 ホストは、MBIMEx 1.0 を使用してデバイスで動作します。 |
| 5 G NSA デバイス <p>ネイティブ MBIMEx version 2.0</p> | デバイスは、最初に MBIMEx 1.0 をアドバタイズします。 MBIM_CID_VERSION exchange がありません。 デバイスは、ホストが MBIMEx 1.0 ことを認識して MBIMEx 1.0 を実行します。 | デバイスは、最初に MBIMEx 1.0 をアドバタイズします。 ホストは、ホストが MBIMEx 2.0 をサポートしているデバイスに通知する MBIM_CID_VERSION を送信します。 MBIMEx 2.0 を使用したデバイスが応答します。 両方の側では、MBIMEx 2.0 を続行します。 |

次の表には、MBIMEx version 2.0、およびそれらの変更されたペイロードで変更されているすべての既存の Cid が一覧表示します。 これらの Cid ですべての unmentioned ペイロードとその他のすべての Cid いない MBIMEx バージョン 1.0 から経由でテーブル キャリーで説明されているし、変更されません。 

| CID | ペイロード |
| --- | --- |
| MBIM_CID_REGISTER_STATE | MBIM_REGISTRATION_STATE_INFO_V2 |
| MBIM_CID_PACKET_SERVICE | MBIM_PACKET_SERVICE_INFO_V2 |
| MBIM_CID_SIGNAL_STATE | MBIM_SIGNAL_STATE_INFO_V2 |

## <a name="mbim-service"></a>MBIM サービス

| サービス名 | UUID | UUID 値 |
| --- | --- | --- |
| Microsoft Basic IP 接続の拡張機能 | UUID_BASIC_CONNECT_EXTENSIONS | 3D01DCC5-FEF5-4D05-9D3A-BEF7058E9AAF |

## <a name="mbimcidversion"></a>MBIM_CID_VERSION

MBIM_CID_VERSION は、ホストとデバイス間 MBIM バージョン情報を交換するため省略可能なコマンドです。 デバイスが古い MBIM バージョンとの下位互換性が必要な場合は、このコマンドをサポートしてする必要があります。

ホストは、デバイスがサポートされている場合、クエリとしてこのコマンドを送信します。 クエリに MBIM リリース番号が含まれており、MBIM 拡張機能のリリース、ホストは現在サポートされている番号。

デバイス側では、デバイスがその発表 MBIM リリース番号を調整し、MBIM 拡張機能のリリースで定義されたルールに基づく番号[バージョン管理スキーム](#versioning-scheme)ホストへの応答で送信します。

このコマンドは、下で定義された、**基本的な接続の拡張機能**サービス。

| CID | コマンド コード | UUID |
| --- | --- | --- |
| MBIM_CID_VERSION | 15 | 3d01dcc5-fef5-4d05-0d3abef7058e9aaf |

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | MBIM_VERSION_INFO | 該当なし |
| 応答 | 該当なし | MBIM_VERSION_INFO | 該当なし |

### <a name="query"></a>クエリ

ホストのネイティブ MBIM リリース番号と MBIM 拡張機能のリリース番号のデバイスに通知します。 InformationBuffer には、次の MBIM_VERSION_INFO 構造が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 2 | bcdMBIMVersion | UINT16 | ビット 7 および 8 間の暗黙の小数点の付いた、BCD の送信者の MBIM リリース番号。 たとえば、`0x0100 == 1.00 == 1.0` と記述します。 これは、バイトが 0x00、0x01 のため、リトル エンディアン定数です。 |
| 2 | 2 | bcdMBIMExtendedVersion | UINT16 | MBIM 拡張機能はリリース ビット 7 および 8 間の暗黙の小数点の付いた、BCD の送信者の番号です。 たとえば、`0x0100 == 1.00 == 1.0` と記述します。 これは、バイトが 0x00、0x01 のため、リトル エンディアン定数です。 |

### <a name="set"></a>Set

適用できません。

### <a name="response"></a>応答

MBIM_COMMAND_DONE で InformationBuffer には MBIM_VERSION_INFO 構造体が含まれています。

### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

この CID がのみの 9.4. 5. のセクションで定義された汎用的なステータス コードを使用して、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。

## <a name="mbimcidmsdevicecapsv2"></a>MBIM_CID_MS_DEVICE_CAPS_V2

この CID がで定義されているものと同じ[MB のマルチ SIM 操作](mb-multi-sim-operations.md#mbim-interface-update-for-multi-sim-operations)、MBIM_CID_MS_DEVICE_CAPS の拡張機能は、それ自体の 10.5.1 で定義されている、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。 MBIM 拡張機能リリース 2.0 は、その 5 G 機能を報告するデバイスを有効にする MBIM_DATA_CLASS テーブルで定義されている新しいデータ クラスがあります。 MBIMDataClass5G_NSA 表します 5 G 以外のスタンドアロン (NSA) で定義されているデバイスをサポートしている[3 gpp TS 37.340](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3198)、MBIMDataClass5G_SA 表します 5 G スタンドアロン (SA) の 3 gpp TS 37.340 でも定義されているデバイスをサポートしているとします。

デバイスは、両方の新しいデータ クラスをサポートする場合は、両方のビットを設定するものとします。

### <a name="mbimdataclass"></a>MBIM_DATA_CLASS

| 型 | ［マスク］ |
| --- | --- |
| MBIMDataClassNone | 0 h |
| MBIMDataClassGPRS | 1 時間 |
| MBIMDataClassEDGE | 2 時間 |
| MBIMDataClassUMTS | 4 時間 |
| MBIMDataClassHSDPA | 8 h |
| MBIMDataClassHSUPA | 10 h |
| MBIMDataClassLTE | 20 h |
| **MBIMDataClass5G_NSA** | **40h** |
| **MBIMDataClass5G_SA** | **80h** |
| 予約済み | 100 h ~ 8000 h |
| MBIMDataClass1XRTT | 10000 h |
| MBIMDataClass1XEVDO | 20000 h |
| MBIMDataClass1XEVDORevA | 40000 h |
| MBIMDataClass1XEVDV | 80000 h |
| MBIMDataClass3XRTT | 100000 h |
| MBIMDataClass1XEVDORevB | 200000 h |
| MBIMDataClassUMB | 400000 h |
| 予約済み | 800000 40000000 h |
| MBIMDataClassCustom | 80000000 h |

## <a name="mbimcidregisterstate"></a>MBIM_CID_REGISTER_STATE

このコマンドは、拡張機能で MBIM_CID_REGISTER_STATE CID が既に定義されている、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。 この拡張機能と呼ばれる新しいメンバーを追加する**PreferredDataClasses**応答の構造にします。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_REGISTRATION_STATE | 空 | 該当なし |
| 応答 | MBIM_REGISTRATION_STATE_INFO_V2 | MBIM_REGISTRATION_STATE_INFO_V2 | MBIM_REGISTRATION_STATE_INFO_V2 |

### <a name="query"></a>クエリ

Null で、InformationBuffer と、InformationBufferLength は 0 になります。

### <a name="set"></a>Set

登録状態を設定します。 情報は、同じ」の説明に従って、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。

### <a name="response"></a>応答

MBIM_COMMAND_DONE で InformationBuffer には、次の MBIM_REGISTRATION_STATE_INFO_V2 構造が含まれています。 10.5.10.6 で定義されている MBIM_REGISTRATION_STATE_INFO 構造体と比較して、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)、次の構造が新しい**PreferredDataClasses**フィールド。 ここで説明すると、しない限り、フィールドのテーブルの 10 ~ 55 での説明、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)この構造に適用されます。

#### <a name="mbimregistrationstateinfov2"></a>MBIM_REGISTRATION_STATE_INFO_V2

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NwError | UINT32 | ネットワーク固有のエラー。 表 10 44 インチ、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip) NwError の原因のコードについて説明します。 |
| 4 | 4 | RegisterState | MBIM_REGISTER_STATE | テーブルに 10 46 を参照してください、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。 |
| 8 | 4 | RegisterMode | MBIM_REGISTER_MODE | テーブルに 10 ~ 47 を参照してください、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。 |
| 12 | 4 | AvailableDataClass | UINT32 | 内の値のビットマップ[MBIM_DATA_CLASS](#mbimdataclass)デバイスが登録されているセルの登録されているネットワークでサポートされているデータ クラスを表します。 <p>場合、この値が MBIMDataClassNone に設定されます、 **RegisterState**ない**MBIMRegisterStateHome**、 **MBIMRegisterStateRoaming**、または**MBIMRegisterStatePartner**します。 </p> |
| 16 | 4 | CurrentCellularClass | MBIM_CELLULAR_CLASS | 関数の複数のモードの使用中の現在の移動体通信クラスを示します。 テーブルに 10-8 を参照してください、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)詳細についてはします。 <p>シングル モード関数の場合、これは MBIM_CID_DEVICE_CAPS で報告された携帯電話のクラスと同じです。 マルチ モード関数では、CDMA から GSM またはその逆への移行が示される、更新された**CurrentCellularClass**します。 </p> |
| 20 | 4 | ProviderIdOffset | OFFSET | 呼ばれる数値 (0 ~ 9) の文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される**ProviderId**プロバイダーのネットワーク id を表します。 <p>GSM ベースのネットワークでは、この文字列は、3 桁 Mobile 国コード (MCC) と、2 桁または 3 桁のモバイル ネットワーク コード (mnc も) の連結です。 GSM ベースの通信事業者が 1 つ以上の mnc もあります。 そのため、複数の 1 つと**ProviderId**します。</p><p>CDMA ベースのネットワークでは、この文字列は、5 桁システム ID (SID) です。 通常、CDMA ベースのキャリアは、1 つ以上の SID を持っています。 通常、キャリアは、通常、地理的に、民族内で除算など大都市圏統計領域 (MSA) で、米国の規制する各市場の 1 つの SID を持ちます。 この情報が利用できない場合、CDMA ベースのデバイスは MBIM_CDMA_DEFAULT_PROVIDER_ID を指定する必要があります。</p><p>処理クエリの要求および登録状態が自動登録モード、このメンバーには、デバイスが現在関連付けられている (該当する) 場合、プロバイダー ID が含まれています。 登録状態は、手動登録モードでは、このメンバーには、デバイスが登録 (プロバイダーは使用できません) 場合でも要求プロバイダーの ID が含まれています。</p><p>セットの要求と、登録状態の処理は、手動モードでは、これと、デバイスを登録するため、ホストによって選択されたプロバイダー ID が含まれます。 登録状態は、自動登録モードでは、このパラメーターが無視されます。</p><p>CDMA 1 xrtt プロバイダーは、プロバイダー ID が使用できない場合、MBIM_CDMA_DEFAULT_PROVIDER_ID に設定する必要があります。</p> |
| 24 | 4 | ProviderIdSize | SIZE(0..12) | サイズ (バイト単位) の**ProviderId**します。 |
| 28 | 4 | ProviderNameOffset | OFFSET | 呼ばれる文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される**ProviderName**ネットワーク プロバイダーの名前を表します。 このメンバーは、多くて MBIM_PROVIDERNAME_LEN 文字に制限されています。 <p>GSM ベースのネットワークでは、国頭文字のプレゼンテーションを優先し、モバイル ネットワーク名 (PCCI & N) は 20 文字を超えるデバイスにネットワーク名省略形する必要があります。</p><p>ホストが優先されるプロバイダーの一覧を設定すると、このメンバーは無視されます。 デバイスは、この情報がないデバイスの NULL 文字列を指定する必要があります。</p> |
| 32 | 4 | ProviderNameSize | SIZE(0..40) | サイズ (バイト単位) の**ProviderName**します。 |
| 36 | 4 | RoamingTextOffset | OFFSET | 呼ばれる文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される**RoamingText**デバイスがローミングをユーザーに通知します。 このメンバーは、最大で 63 文字に制限されています。 このテキストは、登録の状態が MBIMRegisterStatePartner または MBIMRegisterStateRoaming のいずれかをユーザーに追加情報を提供する必要があります。 このメンバーは省略可能です。 |
| 40 | 4 | RoamingTextSize | SIZE(0..126) | サイズ (バイト単位) の**RoamingText**します。 |
| 44 | 4 | RegistrationFlag | MBIM_REGISTRATION_FLAGS | フラグを設定ごとの表 10-48 で、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。 |
| 48 | 4 | PreferredDataClass | UINT32 | 内の値のビットマップ[MBIM_DATA_CLASS](#mbimdataclass)デバイスで有効になっているデータ クラスを表します。 のみ、デバイスは、有効になっているデータ クラスを使用して動作します。 |
| 動的 | 4 | DataBuffer | DATABUFFER | データ バッファーを含む**ProviderId**、 **ProviderName**、および**RoamingText**します。 |

### <a name="unsolicited-events"></a>要請されていないイベント

通知には、MBIM_REGISTRATION_STATE_INFO_V2 構造体が含まれています。

### <a name="status-codes"></a>状態コード

この CID がのみの 9.4. 5. のセクションで定義された汎用的なステータス コードを使用して、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。

## <a name="mbimcidpacketservice"></a>MBIM_CID_PACKET_SERVICE

このコマンドは、拡張機能で定義されている既存の MBIM_CID_PACKET_SERVICE、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。

この拡張機能と呼ばれる新しいメンバーを追加します**FrequencyRange**応答の構造の名前を変更し、 **HighestAvailableDataClass**メンバー **CurrentDataClass**にその目的を明確にします。

**CurrentDataClass**無線アクセス テクノロジ (RAT) デバイスが現在登録されていることを示します。 単一の値が含まれている[MBIM_DATA_CLASS](#mbimdataclass)します。

**FrequencyRange**周波数の範囲、デバイスが現在使用していることを示します。 これは有効な場合にのみ、 **CurrentDataClass**フィールドは、MBIMDataClass5G_NSA または MBIMDataClass5G_SA ビットが設定されていることを示します。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_PACKET_SERVICE | 空 | 該当なし |
| 応答 | MBIM_PACKET_SERVICE_INFO_V2 | MBIM_PACKET_SERVICE_INFO_V2 | MBIM_PACKET_SERVICE_INFO_V2 |

### <a name="query"></a>クエリ

Null で、InformationBuffer と、InformationBufferLength は 0 になります。

### <a name="set"></a>Set

Set コマンドの情報が記載、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。

### <a name="response"></a>応答

MBIM_COMMAND_DONE で InformationBuffer には MBIM_PACKET_SERVICE_INFO_V2 構造体が含まれています。 10.5.10.6 で定義されている MBIM_PACKET_SERVICE_INFO 構造体と比較して、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)、この新しい構造体が、 **CurrentDataClass**と**FrequencyRange**フィールド。 ここでは、フィールドの説明で表 10 ~ 55 に明記されていない限り、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)ここで適用されます。

#### <a name="mbimpacketserviceinfov2"></a>MBIM_PACKET_SERVICE_INFO_V2

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NwError | UINT32 | ネットワーク固有のエラー。 表 10 44 インチ、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip) NwError の原因のコードについて説明します。 |
| 4 | 4 | PacketServiceState | MBIM_PACKET_SERVICE_STATE | テーブルに 10-53 を参照してください、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。 | 
| 8 | 4 | CurrentDataClass | MBIM_DATA_CLASS | に従って指定された現在のセルに現在データ クラス[MBIM_DATA_CLASS](#mbimdataclass)します。 関数は、関数は、パケットが接続されているサービスの状態にない場合は、このメンバーを MBIMDataClassNone に設定する必要があります。 HSPA (つまり、HSUPA および HSDPA) と 5 G DC を除く、関数は単一の MBIM_DATA_CLASS 値にこのメンバーを設定します。 HSPA データ サービスでは、関数は、ビットごとのまたはの MBIMDataClass HSDPA と MBIMDataClassHSUPA を指定します。 HSDPA がない HSUPA をサポートしているセルの場合は、(アップリンク データ UMTS データ クラスを暗に示して) HSDPA のみが示されます。 現在のデータ クラスの変更されるたびに、関数はの新しい値を示す通知を送信**CurrentDataClass**します。 |
| 12 | 8 | UplinkSpeed | UINT64 | アップリンク ビット レート 1 秒あたりのビットにはが含まれています。 |
| 20 | 8 | DownlinkSpeed | UINT64 | ダウンリンク ビット レート 1 秒あたりのビットにはが含まれています。 |
| 38 | 4 | FrequencyRange | MBIM_FREQUENCY_RANGE | 値のビットマスク[MBIM_FREQUENCY_RANGE](#mbimfrequencyrange)デバイスが現在使用している周波数の範囲を表します。 これはのみ有効だ場合、 **CurrentDataClass** MBIMDataClass5G_NSA か MBIMDataClass5G_SA します。 |

#### <a name="mbimfrequencyrange"></a>MBIM_FREQUENCY_RANGE

次の列挙は、前述の MBIM_PACKET_SERVICE_INFO_V2 構造内の値として使用されます。

| 種類 | Value | 説明|
| --- | --- | --- |
| MBIMFrequencyRangeUnknown | 0 | システムの種類がない 5 G の場合は。 |
| MBIMFrequencyRange1 | 1 | 周波数範囲 1 (FR1) [3 gpp TS 38.101 1](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3283) (サブ-6 G)。 |
| MBIMFrequencyRange2 | 2 | FR2 [3 gpp TS 38.101 2](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3284) (mmWave)。 |
| MBIMFrequencyRange1AndRange2 | 3 | 場合 FR1 と FR2 の両方の通信事業者が接続されます。 |

### <a name="unsolicited-events"></a>要請されていないイベント

通知には、MBIM_PACKET_SERVICE_INFO_V2 構造体が含まれています。

### <a name="status-codes"></a>状態コード

この CID がのみの 9.4. 5. のセクションで定義された汎用的なステータス コードを使用して、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。

## <a name="mbimcidsignalstate"></a>MBIM_CID_SIGNAL_STATE

この CID では、MBIM_CID_SIGNAL_STATE、RSRP と SNR をシグナル状態の基準の概要の拡張機能です。 この新しい拡張機能では、有効なは、デバイスが MBIM 拡張機能バージョン 2.0 のサポートを示している場合のみです。 この拡張機能は、モデムが MBIMDataClass5G_ (N) SA データ クラスをサポートしている場合は必須です。

RSRP と SNR フィールドでは、有効である、対応する SystemType は MGBIMDataClassLTE または MBIMDataClass5G_ (N) のいずれかの SA のみです。 モデムと報告 RSRP や SNR、RSSI フィールドは、の値に設定するものとし、場合**99**します。

対応する SystemType が MBIMDataClass5G_ (N) SA の場合は、RSRP フィールドは必須と SNR フィールドは省略可能です。 対応する SystemType が MBIMDataClassLTE の場合は、RSRP と SNR フィールドは省略可能と RSSI フィールドを代わりに使用できます。 ここでは、0 を設定して RSRP と SNR フィールドを省略できます (**0**) 両方の値**RsrpSnrOffset**と**RsrpSnrSize**メンバー。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_SIGNAL_STATE | 空 | 該当なし |
| 応答 | MBIM_SIGNAL_STATE_INFO_V2 | MBIM_SIGNAL_STATE_INFO_V2 | MBIM_SIGNAL_STATE_INFO_V2 |

### <a name="query"></a>クエリ

Null で、InformationBuffer と、InformationBufferLength は 0 になります。

### <a name="set"></a>Set

Set コマンドの情報が記載、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。

### <a name="response"></a>応答

MBIM_COMMAND_DONE で InformationBuffer には、次の MBIM_SIGNAL_STATE_INFO_V2 構造が含まれています。

#### <a name="mbimsignalstateinfov2"></a>MBIM_SIGNAL_STATE_INFO_V2

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Rssi | UINT32 | テーブル 10.58 を参照してください、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。 |
| 4 | 4 | ErrorRate | UINT32 | テーブル 10.58 を参照してください、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。 |
| 8 | 4 | SignalStrengthInterval | UINT32 | レポートの間隔 (秒)。 |
| 12 | 4 | RssiThreshold | UINT32 | RSSI の違いは、レポートをトリガーする値をコード化されました。 これは必要ない場合は、0 xffffffff を使用します。 |
| 16 | 4 | ErrorRateThreshold | UINT32 | ErrorRate の違いは、レポートをトリガーする値をコード化されました。 これは必要ない場合は、0 xffffffff を使用します。 |
| 20 | 4 | RsrpSnrOffset | OFFSET | RSRP とシグナリング情報 SNR を含むバッファーに、この構造体の先頭からのオフセット (バイト単位) が計算されます。 このメンバー **NULL**ありません RSRP と SNR シグナリング情報を利用します。 |
| 24 | 4 | RsrpSnrSize | サイズ | RSRP と SNR シグナリング MBIM_RSRP_SNR_INFO 構造体の形式で情報を格納するバッファーのバイト単位のサイズ。 |
|   | 4 | DataBuffer | DATABUFFER | MBIM_RSRP_SNR の構造体。 |

#### <a name="mbimrsrpsnr"></a>MBIM_RSRP_SNR

次の MBIM_RSRP_SNR 構造が使用される、 **DataBuffer** MBIM_SIGNAL_STATE_INFO_V2 構造体の。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | elementCount | UINT32 | この要素に続く RSRP_SNR エントリの数。 |
| 4 | 4 | DataBuffer | DATABUFFER | MBIM_RSRP_SNR_INFO 構造として指定された各 RSRP_SNR のレコードの配列。 |

#### <a name="mbimrsrpsnrinfo"></a>MBIM_RSRP_SNR_INFO

次の MBIM_RSRP_SNR_INFO 構造体の配列が使用される、 **DataBuffer** MBIM_RSRP_SNR 構造体の。

<table>
    <tr>
        <th>Offset</th>
        <th>サイズ ></th>
        <th>フィールド</th>
        <th>種類</th>
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
                    <th>Dbm RSRP 値</th>
                    <th>ハードコーディングされた値 (最小値 = 0、126 の最大値 =)</th>
                </tr>
                <tr>
                    <td>-156 より小さい</td>
                    <td>0</td>
                </tr>
                <tr>
                    <td>-155 より小さい</td>
                    <td>1</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>-138 より小さい</td>
                    <td>18</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>-45 より小さい</td>
                    <td>111</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>-31 からより小さい</td>
                    <td>125</td>
                </tr>
                <tr>
                    <td>-31 以降</td>
                    <td>126</td>
                </tr>
                <tr>
                    <td>不明なや検出できません。</td>
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
                    <th>Db SN 比</th>
                    <th>ハードコーディングされた値 (最小値 = 0、最大値 127 を =)</th>
                </tr>
                <tr>
                    <td>-23 より小さい</td>
                    <td>0</td>
                </tr>
                <tr>
                    <td>-22.5 より小さい</td>
                    <td>1</td>
                </tr>
                <tr>
                    <td>~ 22 日より小さい</td>
                    <td>2</td>
                </tr>
                <tr>
                    <td>-21.5 より小さい</td>
                    <td>3</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>39.5 より小さい</td>
                    <td>125</td>
                </tr>
                <tr>
                    <td>40 より小さい</td>
                    <td>126</td>
                </tr>
                <tr>
                    <td>40 以上</td>
                    <td>127</td>
                </tr>
                <tr>
                    <td>不明なや検出できません。</td>
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
        <td>古い (キャッシュ) RSRP 値と、新しく計算された RSRP 値の間のしきい値を定義します。 絶対差がしきい値よりも大きい場合は、デバイスは、要請していないイベントをトリガーします。 単位は、1 dBm です。 場合は 0 に設定、デバイスの機能で、既定の動作を使用します。 場合は 0 xffffffff に設定、イベントをトリガーするこれを使用しないでください。 特定のしきい値の値が、デバイスでサポートされていない場合でサポートされる最大しきい値の値を返します。</td>
    </tr>
    <tr>
        <td>12</td>
        <td>4</td>
        <td>SNRThreshold</td>
        <td>UINT32</td>
        <td>古い (キャッシュ) SN 比と新しく計算された SN 比の間のしきい値を定義します。 絶対差がしきい値よりも大きい場合は、デバイスは、要請していないイベントをトリガーします。 単位は、1 dB です。 場合は 0 に設定、デバイスの機能で、既定の動作を使用します。 場合は 0 xffffffff に設定、イベントをトリガーするこれを使用しないでください。 指定のしきい値がデバイスでサポートされていない場合でサポートされる最大しきい値の値を返します。</td>
    </tr>
    <tr>
        <td>16</td>
        <td>4</td>
        <td>SystemType</td>
        <td>MBIM_DATA_CLASS</td>
        <td>シグナルの状態情報が有効なシステム タイプを示します。 定義されている、このメンバーは 1 つの型のビットマスク<a href="#mbimdataclass">MBIM_DATA_CLASS</a>します。</td>
    </tr>
</table>

### <a name="unsolicited-events"></a>要請されていないイベント

通知には、MBIM_SIGNAL_STATE_INFO_V2 構造体が含まれています。

### <a name="status-codes"></a>状態コード

この CID がのみの 9.4. 5. のセクションで定義された汎用的なステータス コードを使用して、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。
