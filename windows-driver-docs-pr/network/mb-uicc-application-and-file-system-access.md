---
title: MB UICC アプリケーションとファイル システム アクセス
description: MB UICC アプリケーションとファイル システム アクセス
ms.assetid: 9A9BFCCE-2481-412F-AEBB-9919F6916224
keywords:
- MB UICC アプリケーションとファイルシステムアクセス、モバイルブロードバンド UICC アプリケーションとファイルシステムアクセス
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4fcee2ae2d2d1b6915814577cdfa3344369a8858
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557767"
---
# <a name="mb-uicc-application-and-file-system-access"></a>MB UICC アプリケーションとファイル システム アクセス

## <a name="overview"></a>概要

このトピックでは、UICC スマートカードアプリケーションとファイルシステムへのアクセスを許可するモバイルブロードバンドインターフェイスモデル (MBIM) インターフェイスの拡張機能について説明します。 この MBIM の拡張機能は、UICC の[ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)に準拠したアプリケーションとファイルシステムへの論理アクセスを公開し、Windows 10 バージョン1903以降でサポートされています。

## <a name="uicc-access-and-security"></a>UICC アクセスとセキュリティ

UICC は、ファイルシステムを提供し、同時に実行できる一連のアプリケーションをサポートします。 たとえば、UMTS の場合は USIM、CDMA の場合は CSIM、IMS の場合は ISIM を使用します。 SIM は、これらのアプリケーションの1つ (GSM 用) としてモデル化できる、UICC の従来の部分です。

[ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション8.1 の次の図は、カードアプリケーション構造の例を示しています。

![UICC アプリケーション構造の例](images/mb-uicc-application-structure.png "UICC アプリケーション構造の例。")

UICC ファイルシステムは、ディレクトリツリーのフォレストと見なすことができます。 レガシ SIM ツリーは、マスターファイル (MF) をルートとしており、さまざまな種類の情報を保持する、複数のサブディレクトリ (専用ファイル、または DFs) が含まれています。 SIM では、MF の下に DFs が定義されています。このうちの1つは、DFTelecom に共通の電話帳などの複数の種類のアクセスに共通する情報です。 追加のアプリケーションは、それぞれ独自のアプリケーションディレクトリファイル (ADF) をルートとする個別のツリーとして効果的に実装されます。 各 ADF は、最大128ビットのアプリケーション識別子によって識別されます。 カードルート (図の MF の下にある EFDir) の下にあるファイルには、アプリケーション名と対応する識別子が含まれています。 ツリー内 (MF または ADF) では、DFs と EFs がファイル id のパスによって識別される場合があります。ファイル ID は16ビットの整数です。

## <a name="ndis-interface-extensions"></a>NDIS インターフェイスの拡張機能

次の Oid は、UICC アプリケーションとファイルシステムアクセスをサポートするために定義されています。

- [OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)
- [OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)
- [OID_WWAN_UICC_ACCESS_BINARY](oid-wwan-uicc-access-binary.md)
- [OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)
- [OID_WWAN_PIN_EX2](oid-wwan-pin-ex2.md)

## <a name="mbim-service-and-cid-values"></a>MBIM サービスと CID 値

| [サービス名] | UUID | UUID の値 |
| --- | --- | --- |
| Microsoft 低レベルの UICC アクセス | UUID_MS_UICC_LOW_LEVEL | C2F6588E-F037-4BC9-8665-F4D44BD09367 |
| Microsoft 基本 IP 接続拡張機能 | UUID_BASIC_CONNECT_EXTENSIONS | 3D01DCC5-FEF5-4D05-9D3A-BEF7058E9AAF |

次の表では、各 CID の UUID とコマンドコードに加えて、CID が Set、Query、または Event (通知) 要求をサポートしているかどうかを示します。 パラメーター、データ構造、および通知の詳細については、このトピック内の各 CID の個別のセクションを参照してください。 

| CID | UUID | コマンドコード | オン | クエリ | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_MS_UICC_APP_LIST | UUID_MS_UICC_LOW_LEVEL | 7 | N | Y | N |
| MBIM_CID_MS_UICC_FILE_STATUS | UUID_MS_UICC_LOW_LEVEL | 8 | N | Y | N |
| MBIM_CID_MS_UICC_ACCESS_BINARY | UUID_MS_UICC_LOW_LEVEL | 9 | Y | Y | N |
| MBIM_CID_MS_UICC_ACCESS_RECORD | UUID_MS_UICC_LOW_LEVEL | 10 | Y | Y | N |
| MBIM_CID_MS_PIN_EX | UUID_BASIC_CONNECT_EXTENSIONS | 14 | Y | Y | N |

## <a name="mbim_cid_ms_uicc_app_list"></a>MBIM_CID_MS_UICC_APP_LIST

この CID は、UICC 内のアプリケーションの一覧と、それらに関する情報を取得します。 モデムの UICC が完全に初期化され、携帯電話会社に登録する準備ができたら、UICC アプリケーションを登録用に選択する必要があります。また、この CID を使用してクエリを実行すると、選択したアプリケーションが応答で使用される MBIM_UICC_APP_LIST 構造の**Activeappindex**フィールドに返されます。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 適用なし | Empty | 適用なし |
| 応答 | 適用なし | MBIM_UICC_APP_LIST | 適用なし |

### <a name="query"></a>クエリ

MBIM_COMMAND_MSG の InformationBuffer が空です。

### <a name="set"></a>オン

適用不可。

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer には、次の MBIM_UICC_APP_LIST 構造が含まれています。

#### <a name="mbim_uicc_app_list-version-1"></a>MBIM_UICC_APP_LIST (バージョン 1)

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 後に続く構造体のバージョン番号。 この構造体のバージョン1では、このフィールドを**1**に設定する必要があります。 |
| 4 | 4 | AppCount | UINT32 | この応答で返される UICC アプリケーション**MBIM_UICC_APP_INFO**構造体の数。 |
| 8 | 4 | ActiveAppIndex | UINT32 (0.. NumApp-1) | モバイルネットワークに登録するためにモデムによって選択されたアプリケーションのインデックス。 このフィールドは、 **0**から**appcount-1**までの範囲で指定する必要があります。 この応答によって返されるアプリケーションの配列にインデックスを付けます。 登録するアプリケーションが選択されていない場合、このフィールドには**0xffffffff**が含まれます。 |
| 12 | 4 | アプライアンスののオフセット | OFFSET | この構造体の先頭から、アプリの一覧を格納しているバッファーまでのオフセット (バイト単位)。 |
| 16 | 4 | アプライアンスのサイズ変更 | サイズ (0. AppCount * 312) | アプリリストデータのサイズ (バイト単位)。 |
| 20 | アプライアンスのサイズ変更 | DataBuffer | DATABUFFER | **Appcount**  *  **MBIM_UICC_APP_INFO**構造体の配列。 |

#### <a name="mbim_uicc_app_info"></a>MBIM_UICC_APP_INFO

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | AppType | MBIM_UICC_APP_TYPE | UICC アプリケーションの型。 |
| 4 | 4 | AppIdSize | サイズ (0 ~ 16) | [ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション8.3 で定義されている、アプリケーション ID のサイズ (バイト単位)。 **MBIMUiccAppTypeMf**、 **MBIMUiccAppTypeMfSIM**、または**MBIMUiccAppTypeMfRUIM**アプリの種類では、このフィールドは0に設定されます。 |
| 8 | 16 | AppId | Byte array | アプリケーション ID。 最初の**Appidsize**バイトだけが意味を持ちます。 アプリケーション ID が**MBIM_MAXLENGTH_APPID**バイトを超えている場合、AppIdSize は実際の長さを指定しますが、このフィールドには最初の**MBIM_MAXLENGTH_APPID**バイトだけが含まれます。 このフィールドは、 **AppType**が**MBIMUiccAppTypeMf**、 **MBIMUiccAppTypeMfSIM**、または**MBIMUiccAppTypeMfRUIM**ではない場合にのみ有効です。 |
| 24 | 4 | AppNameLength | サイズ (0 ~ 256) | アプリケーション名の長さ (文字数)。 |
| 28 | 256 | AppName | ASCII 文字配列 | アプリケーションの名前を指定する UTF-8 文字列。 このフィールドの長さは、 **AppNameLength**によって指定されます。 長さが**MBIM_MAXLENGTH_APPNAME**バイト以上の場合、このフィールドには名前の最初の**MBIM_MAXLENGTH_APPNAME-1**バイトが格納されます。 文字列は常に null で終わります。 |
| 284 | 4 | NumPins | サイズ (0.. 8) | アプリケーションの PIN 参照の数。 つまり、有効な**Pinref**の要素の数。 仮想 R/UIM のアプリケーションには、PIN 参照がありません。 |
| 288 | 8 | PinRef | Byte array | [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション9.4.2 で定義されているように、このアプリケーションのアプリケーションの PIN 参照 (PIN1 のキーと、場合によっては upin) を指定するバイト配列。 シングル検証カードの場合、または異なるアプリケーションに対して異なるアプリケーションキーをサポートしていない MBB ドライバーやモデムの場合は、このフィールドを**0x01**にする必要があります。 |

#### <a name="mbim_uicc_app_type"></a>MBIM_UICC_APP_TYPE

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMUiccAppTypeUnknown | 0 | 不明な型です。 |
| MBIMUiccAppTypeMf | 1 | MF をルートとする従来の SIM ディレクトリ。 |
| MBIMUiccAppTypeMfSIM | 2 | DF_GSM をルートとする従来の SIM ディレクトリ。 |
| MBIMUiccAppTypeMfRUIM | 3 | DF_CDMA をルートとする従来の SIM ディレクトリ。 |
| MBIMUiccAppTypeUSIM | 4 | USIM アプリケーション。 |
| MBIMUiccAppTypeCSIM | 5 | CSIM の場合は、 |
| MBIMUiccAppTypeISIM | 6 | ISIM アプリケーション。 |

#### <a name="constants"></a>定数

MBIM_CID_MS_UICC_APP_INFO には、次の定数が定義されています。

`const int MBIM_MAXLENGTH_APPID = 16`  
`const int MBIM_MAXLENGTH_APPNAME = 256`  
`const int MBIM_MAXNUM_PINREF = 8`  

### <a name="unsolicited-events"></a>一方的なイベント

適用不可。

### <a name="status-codes"></a>状態コード

次のステータスコードが適用されます。

| status code | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_BUSY | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_FAILURE | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC がないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | Uicc がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_NOT_INITIALIZED | Uicc がまだ完全に初期化されていないため、UICC 操作を実行できません。 |

## <a name="mbim_cid_ms_uicc_file_status"></a>MBIM_CID_MS_UICC_FILE_STATUS

この CID は、指定された UICC ファイルに関する情報を取得します。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 適用なし | MBIM_UICC_FILE_PATH | 適用なし |
| 応答 | 適用なし | MBIM_UICC_FILE_STATUS | 適用なし |

### <a name="query"></a>クエリ

MBIM_COMMAND_MSG の InformationBuffer には、ターゲット EF が MBIM_UICC_FILE_PATH 構造として含まれています。

#### <a name="mbim_uicc_file_path-version-1"></a>MBIM_UICC_FILE_PATH (バージョン 1)

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 後に続く構造体のバージョン番号。 この構造体のバージョン1では、このフィールドは**1**である必要があります。 |
| 4 | 4 | AppIdOffset | OFFSET | この構造体の先頭からアプリケーション ID を格納しているバッファーまでのオフセット (バイト単位)。 |
| 8 | 4 | AppIdSize | サイズ (0 ~ 16) | [ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション8.3 で定義されている、アプリケーション ID のサイズ (バイト単位)。 2G カードの場合、このフィールドはゼロ (0) に設定する必要があります。 |
| 12 | 4 | FilePathOffset | OFFSET | ファイルパスを格納しているバッファーに、この構造体の先頭から計算されたオフセット (バイト単位)。 ファイルパスは、16ビットのファイル Id の配列です。 1つ目の**ID は、** "2" または " **0x3f00**" のいずれかである必要があります。 最初の**ID が desginated の場合、パス**は**AppId**によってアプリケーションの ADF に対して相対的になります。 それ以外の場合は、MF から始まる絶対パスです。 |
| 16 | 4 | FilePathSize | サイズ (0.. 8) | ファイルパスのサイズ (バイト単位)。 |
| 20 |   | DataBuffer | DATABUFFER | AppId と FilePath を含むデータバッファー。 |

### <a name="set"></a>オン

適用不可。

### <a name="response"></a>応答

InformationBuffer では、次の MBIM_UICC_FILE_STATUS 構造が使用されます。

#### <a name="mbim_uicc_file_status-version-1"></a>MBIM_UICC_FILE_STATUS (バージョン 1)

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 後に続く構造体のバージョン番号。 この構造体のバージョン1では、このフィールドは**1**である必要があります。 |
| 4 | 4 | StatusWord1 | UINT32 (0.. 256) | UICC コマンドに固有の戻りパラメーター。 |
| 8 | 4 | StatusWord2 | UINT32 (0.. 256) | UICC コマンドに固有の戻りパラメーター。 |
| 12 | 4 | FileAccessibility | MBIM_UICC_FILE_ACCESSIBILITY | UICC ファイルのアクセシビリティ。 |
| 16 | 4 | FileType | MBIM_UICC_FILE_TYPE | UICC ファイルの種類。 |
| 20 | 4 | FileStructure | MBIM_UICC_FILE_STRUCTURE | UICC ファイル構造体。 |
| 24 | 4 | ItemCount | UINT32 | UICC ファイル内の項目の数。 Transparent ファイルと TLV ファイルの場合は、 **1**に設定されます。 |
| 28 | 4 | サイズ | UINT32 | 各項目のサイズ (バイト単位)。 Transparent または TLV ファイルの場合、これは EF 全体のサイズです。 レコードベースのファイルの場合、これはレコードの合計数を表します。 |
| 32 | 16 | FileLockStatus | MBIM_PIN_TYPE_EX \[ 4\] | そのファイルに対する各操作 (読み取り、更新、アクティブ化、および非アクティブ化) のアクセス条件を記述する MBIM_PIN_TYPE_EX 型の配列。 |

#### <a name="mbim_uicc_file_accessibility"></a>MBIM_UICC_FILE_ACCESSIBILITY

MBIM_UICC_FILE_ACCESSIBILITY 列挙体は、前の MBIM_UICC_FILE_STATUS 構造体で使用されます。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMUiccFileAccessibilityUnknown | 0 | ファイル共有性が不明です。 |
| MBIMUiccFileAccessibilityNotShareable | 1 | 共有可能ファイルではありません。 |
| MBIMUiccFileAccessibilityShareable | 2 | 共有可能ファイル。 |

#### <a name="mbim_uicc_file_type"></a>MBIM_UICC_FILE_TYPE

MBIM_UICC_FILE_TYPE 列挙体は、前の MBIM_UICC_FILE_STATUS 構造体で使用されます。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMUiccFileTypeUnknown | 0 | ファイルの種類が不明です。 |
| MBIMUiccFileTypeWorkingEf | 1 | 作業 EF。 |
| MBIMUiccFileTypeInternalEf | 2 | 内部 EF。 |
| MBIMUiccFileTypeDfOrAdf | 3 | 専用ファイル。他のノードの親であるディレクトリです。 これは DF または ADF である可能性があります。 |

#### <a name="mbim_uicc_file_structure"></a>MBIM_UICC_FILE_STRUCTURE

MBIM_UICC_FILE_STRUCTURE 列挙体は、前の MBIM_UICC_FILE_STATUS 構造体で使用されます。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMUiccFileStructureUnknown | 0 | 不明なファイル構造です。 |
| MBIMUiccFileStructureTransparent | 1 | 可変長の1つのレコード。 |
| MBIMUiccFileStructureCyclic | 2 | 同じ長さのレコードの循環セット。 |
| MBIMUiccFileStructureLinear | 3 | レコードの線形セット。各長さは同じです。 |
| MBIMUiccFileStructureBerTLV | 4 | タグによってアクセスできるデータ値のセット。 |

#### <a name="mbim_pin_type_ex"></a>MBIM_PIN_TYPE_EX

MBIM_PIN_TYPE_EX 列挙体は、前の MBIM_UICC_FILE_STATUS 構造体で使用されます。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMPinTypeNone | 0 | 入力が保留中の PIN はありません。 |
| MBIMPinTypeCustom | 1 | PIN の種類はカスタム型で、この列挙に示されている他の PIN の種類はありません。 |
| MBIMPinTypePin1 | 2 | PIN1 キー。 |
| MBIMPinTypePin2 | 3 | PIN2 キー。 |
| MBIMPinTypeDeviceSimPin | 4 | デバイスを SIM キーにします。 |
| MBIMPinTypeDeviceFirstSimPin | 5 | デバイスは最初の SIM キーになります。 |
| MBIMPinTypeNetworkPin | 6 | ネットワークのパーソナル化キー。 |
| MBIMPinTypeNetworkSubsetPin | 7 | ネットワークサブセットのパーソナル化キー。 |
| MBIMPinTypeServiceProviderPin | 8 | サービスプロバイダー (SP) のパーソナル化キー。 |
| MBIMPinTypeCorporatePin | 9 | 企業の個人設定キー。 |
| MBIMPinTypeSubsidyLock | 10 | Subsidy unlock キー。 | 
| MBIMPinTypePuk1 | 11 | 個人識別番号1ロック解除キー (PUK1)。 |
| MBIMPinTypePuk2 | 12 | 暗証番号 (PUK2) を指定します。 |
| MBIMPinTypeDeviceFirstSimPuk | 13 | デバイスは最初に SIM ピンロック解除キーを持っています。 |
| MBIMPinTypeNetworkPuk | 14 | ネットワークパーソナル化ロック解除キー。 |
| MBIMPinTypeNetworkSubsetPuk | 15 | ネットワークサブセットのパーソナル化解除キー。 |
| MBIMPinTypeServiceProviderPuk | 16 | サービスプロバイダー (SP) のパーソナル化ロック解除キー。 |
| MBIMPinTypeCorporatePuk | 17 | 企業のパーソナル化ロック解除キー。 |
| MBIMPinTypeNev | 18 | NEV キー。 |
| MBIMPinTypeAdm | 19 | 管理キー。 |

### <a name="unsolicited-events"></a>一方的なイベント

適用不可。

### <a name="status-codes"></a>状態コード

次のステータスコードが適用されます。

| status code | 説明 |
| --- | --- |
| MBIM_STATUS_BUSY | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_FAILURE | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC がないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | Uicc がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | このファイルは共有可能ではなく、現在別のアプリケーションによってアクセスされているため、選択できません。 SIM によって返されるステータスワードは6985です。 |

## <a name="mbim_cid_ms_uicc_access_binary"></a>MBIM_CID_MS_UICC_ACCESS_BINARY

この CID は、 **MBIMUiccFileStructureTransparent**または**MBIMUiccFileStructureBerTLV**構造体型の uicc バイナリファイルにアクセスするための特定のコマンドを送信します。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 適用なし | MBIM_UICC_ACCESS_BINARY | 適用なし |
| 応答 | 適用なし | MBIM_UICC_RESPONSE | 適用なし |

### <a name="query"></a>クエリ

バイナリファイルを読み取ります。 MBIM_COMMAND_MSG の InformationBuffer に MBIM_UICC_ACCESS_BINARY 構造体が含まれています。 MBIM_COMMAND_DONE の InformationBuffer に MBIM_UICC_RESPONSE 構造体が返されます。

#### <a name="mbim_uicc_access_binary-version-1"></a>MBIM_UICC_ACCESS_BINARY (バージョン 1)

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 後に続く構造体のバージョン番号。 この構造体のバージョン1では、このフィールドを**1**に設定する必要があります。 |
| 4 | 4 | AppIdOffset | OFFSET | この構造体の先頭からアプリケーション ID を格納しているバッファーまでのオフセット (バイト単位)。 |
| 8 | 4 | AppIdSize | サイズ (0 ~ 16) | [ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション8.3 で定義されている、アプリケーション ID のサイズ (バイト単位)。 2G カードの場合、このフィールドはゼロ (0) に設定する必要があります。 |
| 12 | 4 | FilePathOffset | OFFSET | ファイルパスを格納しているバッファーに、この構造体の先頭から計算されたオフセット (バイト単位)。 ファイルパスは、16ビットのファイル Id の配列です。 1つ目の**ID は、** "2" または " **0x3f00**" のいずれかである必要があります。 最初の**ID が desginated の場合、パス**は**AppId**によってアプリケーションの ADF に対して相対的になります。 それ以外の場合は、MF から始まる絶対パスです。 |
| 16 | 4 | FilePathSize | SIZE | ファイルパスのサイズ (バイト単位)。 |
| 20 | 4 | FileOffset | UINT32 | ファイルからの読み取り時に使用されるオフセット。 このフィールドは256よりも大きくすることができます。また、 [ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)で定義されているように、オフセットの最大値とオフセット低の両方を組み合わせています。 |
| 24 | 4 | NumberOfBytes | UINT32 | 読み取るバイト数。 たとえば、クライアントドライバーは、この関数を使用して256バイトを超える transparent (バイナリ) ファイルを読み取ることができます。ただし、1つの UICC 操作で読み取りまたは書き込みが可能な最大量は、 [ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)につき256バイトです。 これを複数の APDUs に分割し、結果を1回の応答で返すのは、関数の役割です。 |
| 28 | 4 | LocalPinOffset | OFFSET | この構造体の先頭からパスワードを格納しているバッファーまでのオフセット (バイト単位)。 これはローカル PIN (PIN2) であり、操作でローカル PIN の検証が必要な場合に使用されます。 |
| 32 | 4 | LocalPinSize | サイズ (0 ~ 16) | パスワードのサイズ (バイト単位)。 |
| 36 | 4 | BinaryDataOffset | OFFSET | この構造体の先頭から、コマンド固有のデータを格納しているバッファーまでのオフセット (バイト単位)。 バイナリデータは、セット操作に対してのみ使用されます。 |
| 40 | 4 | BinaryDataSize | サイズ (0 ~ 32768) | データのサイズ (バイト単位)。 |
| 44 |   | DataBuffer | DATABUFFER | AppId、FilePath、LocalPin、および BinaryData を含むデータバッファー。 |

### <a name="set"></a>オン

適用不可。

### <a name="response"></a>応答

InformationBuffer では、次の MBIM_UICC_RESPONSE 構造が使用されます。

#### <a name="mbim_uicc_response-version-1"></a>MBIM_UICC_RESPONSE (バージョン 1)

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 次の構造体のバージョン番号。 この構造体のバージョン1では、このフィールドは**1**である必要があります。 |
| 4 | 4 | StatusWord1 | UINT32 (0.. 256) | UICC コマンドに固有の戻りパラメーター。 |
| 8 | 4 | StatusWord2 | UINT32 (0.. 256) | UICC コマンドに固有の戻りパラメーター。 |
| 12 | 4 | ResponseDataOffset | OFFSET | この構造体の先頭から応答データを格納しているバッファーまでのオフセット (バイト単位)。 応答データはクエリ操作にのみ使用されます。 |
| 16 | 4 | ResponseDataSize | サイズ (0 ~ 32768) | データのサイズ (バイト単位)。 |
| 20 |   | DataBuffer | DATABUFFER | ResponseData を格納しているデータバッファー。 |

### <a name="unsolicited-events"></a>一方的なイベント

適用不可。

### <a name="status-codes"></a>状態コード

次のステータスコードが適用されます。

| status code | 説明 |
| --- | --- |
| MBIM_STATUS_BUSY | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_FAILURE | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC がないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | Uicc がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | このファイルは共有可能ではなく、現在別のアプリケーションによってアクセスされているため、選択できません。 SIM によって返されるステータスワードは6985です。 |
| MBIM_STATUS_PIN_FAILURE | PIN エラーが発生したため、操作に失敗しました。 |

## <a name="mbim_cid_ms_uicc_access_record"></a>MBIM_CID_MS_UICC_ACCESS_RECORD

この CID は、 **MBIMUiccFileStructureCyclic**または**MBIMUIccFileStructureLinear**の構造体型を使用して、uicc 線形固定ファイルまたは循環ファイルにアクセスするための特定のコマンドを送信します。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 適用なし | MBIM_UICC_ACCESS_RECORD | 適用なし |
| 応答 | 適用なし | MBIM_UICC_RESPONSE | 適用なし |

### <a name="query"></a>クエリ

レコードの内容を読み取ります。 MBIM_COMMAND_MSG の InformationBuffer には、次の MBIM_UICC_ACCESS_RECORD 構造が含まれています。 MBIM_COMMAND_DONE の InformationBuffer に MBIM_UICC_RESPONSE が返されます。

#### <a name="mbim_uicc_access_record-version-1"></a>MBIM_UICC_ACCESS_RECORD (バージョン 1)

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 後に続く構造体のバージョン番号。 この構造体のバージョン1では、このフィールドを**1**に設定する必要があります。 |
| 4 | 4 | AppIdOffset | OFFSET | この構造体の先頭からアプリケーション ID を格納しているバッファーまでのオフセット (バイト単位)。 |
| 8 | 4 | AppIdSize | サイズ (0 ~ 16) | [ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション8.3 で定義されている、アプリケーション ID のサイズ (バイト単位)。 2G カードの場合、このフィールドはゼロ (0) に設定する必要があります。 |
| 12 | 4 | FilePathOffset | OFFSET | ファイルパスを格納しているバッファーに、この構造体の先頭から計算されたオフセット (バイト単位)。 ファイルパスは、16ビットのファイル Id の配列です。 1つ目の**ID は、** "2" または " **0x3f00**" のいずれかである必要があります。 最初の**ID が desginated の場合、パス**は**AppId**によってアプリケーションの ADF に対して相対的になります。 それ以外の場合は、MF から始まる絶対パスです。 |
| 16 | 4 | FilePathSize | SIZE | ファイルパスのサイズ (バイト単位)。 |
| 20 | 4 | RecordNumber | UINT32 (0.. 256) | レコード番号。 これは、絶対レコードインデックスを常に表します。 モデムがファイル (次、前) に対して複数のアクセスを実行できるため、相対レコードアクセスはサポートされていません。 |
| 24 | 4 | LocalPinOffset | OFFSET | この構造体の先頭からパスワードを格納しているバッファーまでのオフセット (バイト単位)。 ロックパスワードは、10進数の null で終わる UTF-8 文字列です。 | 
| 28 | 4 | LocalPinSize | サイズ (0 ~ 16) | パスワードのサイズ (バイト単位)。 |
| 32 | 4 | RecordDataOffset | OFFSET | この構造体の先頭から、コマンド固有のデータを格納しているバッファーまでのオフセット (バイト単位)。 レコードデータは、セット操作に対してのみ使用されます。 |
| 36 | 4 | RecordDataSize | サイズ (0 ~ 256) | データのサイズ (バイト単位)。 |
| 40 |   | DataBuffer | DATABUFFER | AppId、FilePath、LocalPin、および RecordData を含むデータバッファー。 |

### <a name="set"></a>オン

適用不可。

### <a name="response"></a>応答

InformationBuffer では、MBIM_UICC_RESPONSE 構造体が使用されます。

### <a name="unsolicited-events"></a>一方的なイベント

適用不可。

### <a name="status-codes"></a>状態コード

次のステータスコードが適用されます。

| status code | 説明 |
| --- | --- |
| MBIM_STATUS_BUSY | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_FAILURE | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC がないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | Uicc がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | このファイルは共有可能ではなく、現在別のアプリケーションによってアクセスされているため、選択できません。 SIM によって返されるステータスワードは6985です。 |
| MBIM_STATUS_PIN_FAILURE | PIN エラーが発生したため、操作に失敗しました。 |

## <a name="mbim_cid_ms_pin_ex"></a>MBIM_CID_MS_PIN_EX

この CID は、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション9で定義されているすべての PIN セキュリティ操作を実行するために使用されます。 CID は MBIM_CID_MS_PIN に似ていますが、マルチアプリの UICC カードをサポートするように拡張されています。 1つの検証に対応した UICCs のみがサポートされています。 複数のアプリケーション PIN をサポートするマルチ検証対応の UICCs はサポートされていません。 1つのアプリケーション PIN (PIN1) が、UICC 上のすべての ADFs/DFs およびファイルに割り当てられます。 ただし、各アプリケーションでは、レベル2のユーザー検証要件としてローカル PIN (PIN2) を指定できます。その結果、すべてのアクセスコマンドに対して追加の検証が必要になります。 このシナリオは MBIM_CID_MS_PIN_EX でサポートされています。

MBIM_CID_MS_PIN_EX MBIM_CID_MS_PIN と同様に、デバイスは一度に1つの PIN のみを報告します。 複数の Pin が有効になっていて、複数の Pin を報告する場合も、関数は PIN1 を最初に報告する必要があります。 たとえば、subsidy ロックレポートが有効で、SIM の PIN1 が有効になっている場合、PIN1 が正常に検証された後にのみ、後続のクエリ要求で subsidy lock PIN を報告する必要があります。 空の PIN は、MBIMPinOperationEnter と共に使用できます。 空の PIN を指定するには、PinSize を0に設定します。 この場合、SET コマンドはクエリに似ており、参照先の PIN の状態を返します。 これは、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション11.1.9 で指定されている VERIFY コマンドの動作に完全に対応しています。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_PIN_EX | MBIM_PIN_APP | 適用なし |
| 応答 | MBIM_PIN_INFO_EX | MBIM_PIN_INFO_EX | 適用なし |

### <a name="query"></a>クエリ

InformationBuffer では、次の MBIM_PIN_APP 構造が使用されます。

#### <a name="mbim_pin_app-version-1"></a>MBIM_PIN_APP (バージョン 1)

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 後に続く構造体のバージョン番号。 この構造体のバージョン1では、このフィールドを**1**に設定する必要があります。 |
| 4 | 4 | AppIdOffset | OFFSET | この構造体の先頭からアプリケーション ID を格納しているバッファーまでのオフセット (バイト単位)。 |
| 8 | 4 | AppIdSize | サイズ (0 ~ 16) | [ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション8.3 で定義されている、アプリケーション ID のサイズ (バイト単位)。 2G カードの場合、このフィールドはゼロ (0) に設定する必要があります。 |
| 12 |   | DataBuffer | DATABUFFER | [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)で定義されている AppId。 |

### <a name="set"></a>オン

InformationBuffer では、次の MBIM_SET_PIN_EX 構造が使用されます。

#### <a name="mbim_set_pin_ex"></a>MBIM_SET_PIN_EX

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PinType | MBIM_PIN_TYPE_EX | PIN の種類。 このトピックの MBIM_PIN_TYPE_EX テーブルを参照してください。 |
| 4 | 4 | PinOperation | MBIM_PIN_OPERATION | PIN 操作。 「MBIM 1.0」を参照してください。 |
| 8 | 4 | PinOffset | OFFSET | この構造体の先頭から、アクションの実行に使用する PIN 値を表す文字列 PIN、または PIN 設定を有効または無効にするために必要な PIN 値までのオフセット (バイト単位)。 このフィールドは、 **Pinoperation**のすべての値に適用されます。 |
| 12 | 4 | PinSize | サイズ (0.. 32) | PIN に使用されるサイズ (バイト単位)。 |
| 16 | 4 | NewPinOffset | OFFSET | PinTypeMBIMPinTypePuk1 または PinTypeMBIMPinTypePuk2 の**Pinoperation**が MBIMPinOperationChange または MBIMPinOperationEnter の場合に設定する新しい pin 値を表す**newpin**文字列に、この構造体の先頭から計算されたオフセット (バイト単位)。 |
| 20 | 4 | NewPinSize | サイズ (0.. 32) | NewPin に使用されるサイズ (バイト単位)。 |
| 24 | 4 | AppIdOffset | OFFSET | この構造体の先頭からアプリケーション ID を格納しているバッファーまでのオフセット (バイト単位)。 |
| 28 | 4 | AppIdSize | サイズ (0 ~ 16) | [ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション8.3 で定義されている、アプリケーション ID のサイズ (バイト単位)。 2G カードの場合、このフィールドはゼロ (0) に設定する必要があります。 |
| 32 |   | DataBuffer | DATABUFFER | Pin、NewPin、および AppId を格納しているデータバッファー。 |

### <a name="response"></a>応答

InformationBuffer では、次の MBIM_PIN_INFO_EX 構造が使用されます。

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PinType | MBIM_PIN_TYPE_EX | PIN の種類。 このトピックの MBIM_PIN_TYPE_EX テーブルを参照してください。 |
| 4 | 4 | PinState | MBIM_PIN_STATE | PIN の状態。 「MBIM 1.0」を参照してください。 |
| 8 | 4 | RemainingAttempts | UINT32 | Enter、enable、disable など、PIN に関連する操作の残りの試行回数。 この情報をサポートしていないデバイスは、このメンバーを0xFFFFFFFF に設定する必要があります。 |

### <a name="unsolicited-events"></a>一方的なイベント

適用不可。

### <a name="status-codes"></a>状態コード

次のステータスコードが適用されます。

| status code | 説明 |
| --- | --- |
| MBIM_STATUS_BUSY | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_FAILURE | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC がないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | Uicc がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_PIN_DISABLED | PIN が無効になっているため、操作に失敗しました。 |
| MBIM_STATUS_PIN_REQUIRED | 操作を実行できませんでした。続行するには、PIN を入力する必要があります。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 対応する PIN の種類に設定されているがデバイスでサポートされていないため、操作に失敗しました。 |
