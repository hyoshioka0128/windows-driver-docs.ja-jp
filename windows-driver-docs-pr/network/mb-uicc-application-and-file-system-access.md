---
title: MB UICC アプリケーションとファイル システム アクセス
description: MB UICC アプリケーションとファイル システム アクセス
ms.assetid: 9A9BFCCE-2481-412F-AEBB-9919F6916224
keywords:
- MB UICC アプリケーションとファイル システムへのアクセス、モバイル ブロード バンド UICC アプリケーションおよびファイル システムへのアクセス
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ac43797904bb5bce69b5bd28b21f0a181b55928c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367608"
---
# <a name="mb-uicc-application-and-file-system-access"></a>MB UICC アプリケーションとファイル システム アクセス

## <a name="overview"></a>概要

このトピックでは、UICC スマート カード アプリケーションとファイル システムへのアクセスを許可するようにモバイル ブロード バンド インターフェイス モデル (MBIM) インターフェイスの拡張機能を指定します。 MBIM に対するこの拡張機能は、UICC のに対する論理アクセスを公開します。 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)-準拠のアプリケーションおよびファイル システム、Windows 10、バージョンが 1903 以降でサポートされています。

## <a name="uicc-access-and-security"></a>UICC アクセスとセキュリティ

UICC はファイル システムを提供し、同時に実行できるアプリケーションのセットをサポートします。 以下の USIM UMTS、CSIM CDMA、および ISIM IMS の。 SIM とは、これらのアプリケーション (GSM) 用の 1 つとしてモデル化できる UICC の従来の一部です。

次の図のセクション 8.1 から、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)カード アプリケーション構造の例を示しています。

![たとえば UICC アプリケーション構造](images/mb-uicc-application-structure.png "例 UICC アプリケーションの構造体。")

UICC ファイル システムは、ディレクトリ ツリーのフォレストとして見なすことができます。 レガシの SIM ツリーは、Master ファイル (MF) では、root 化されているし、最大で 2 つのレベル サブディレクトリ (専用のファイルまたは DFs) にはが含まれていますさまざまな種類の情報を保持する Elemental ファイル (EFs) を格納しています。 SIM のいずれかと、MF DFs を定義する共通の電話帳など複数のアクセスの種類に共通の情報が含まれている DFTelecom、します。 その他のアプリケーションは個別のツリーとして効果的に実装、root 化されているそれぞれの独自アプリケーション ディレクトリ ファイル (ADF)。 各 ADF は、最大 128 ビット長可能性のあるアプリケーション識別子によって識別されます。 (下の図に MF EFDir) カードのルートの下のファイルには、アプリケーション名と対応する識別子が含まれています。 MF (ADF) ツリー内で、DFs と EFs によって特定されます。 ファイル ID が 16 ビット整数を Id のファイルのパス。

## <a name="ndis-interface-extensions"></a>NDIS インターフェイスの拡張機能

次の Oid は UICC アプリケーションとファイル システムへのアクセスをサポートするために定義されています。

- [OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)
- [OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)
- [OID_WWAN_UICC_ACCESS_BINARY](oid-wwan-uicc-access-binary.md)
- [OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)
- [OID_WWAN_PIN_EX2](oid-wwan-pin-ex2.md)

## <a name="mbim-service-and-cid-values"></a>MBIM サービスと CID 値

| サービス名 | UUID | UUID 値 |
| --- | --- | --- |
| Microsoft UICC の低レベルのアクセス | UUID_MS_UICC_LOW_LEVEL | C2F6588E-F037-4BC9-8665-F4D44BD09367 |
| Microsoft Basic IP 接続の拡張機能 | UUID_BASIC_CONNECT_EXTENSIONS | 3D01DCC5-FEF5-4D05-9D3A-BEF7058E9AAF |

次の表に、UUID を指定して、各 CID のコードをコマンドだけでなく、CID がサポートしているかどうかを設定、クエリ、またはイベント (通知) を要求します。 詳細については、パラメーター、データ構造、および通知の詳細については、このトピック内の各 CID の個々 のセクションを参照してください。 

| CID | UUID | コマンド コード | 設定 | クエリ | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_MS_UICC_APP_LIST | UUID_MS_UICC_LOW_LEVEL | 7 | N | Y | N |
| MBIM_CID_MS_UICC_FILE_STATUS | UUID_MS_UICC_LOW_LEVEL | 8 | N | Y | N |
| MBIM_CID_MS_UICC_ACCESS_BINARY | UUID_MS_UICC_LOW_LEVEL | 9 | Y | Y | N |
| MBIM_CID_MS_UICC_ACCESS_RECORD | UUID_MS_UICC_LOW_LEVEL | 10 | Y | Y | N |
| MBIM_CID_MS_PIN_EX | UUID_BASIC_CONNECT_EXTENSIONS | 15 | Y | Y | N |

## <a name="mbimcidmsuiccapplist"></a>MBIM_CID_MS_UICC_APP_LIST

この CID を UICC 内のアプリケーションとそれらについての情報の一覧を取得します。 ときにモデムで UICC が完全に初期化されると携帯電話会社に登録する準備ができて、UICC アプリケーションを選択してください登録とこの CID を持つクエリで選択したアプリケーションを返す必要があります、 **ActiveAppIndex**応答で使用される MBIM_UICC_APP_LIST 構造のフィールドです。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | 空 | 該当なし |
| 応答 | 該当なし | MBIM_UICC_APP_LIST | 該当なし |

### <a name="query"></a>クエリ

MBIM_COMMAND_MSG の InformationBuffer が空です。

### <a name="set"></a>Set

適用できません。

### <a name="response"></a>応答

MBIM_COMMAND_DONE で InformationBuffer には、次の MBIM_UICC_APP_LIST 構造が含まれています。

#### <a name="mbimuiccapplist-version-1"></a>MBIM_UICC_APP_LIST (バージョン 1)

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | バージョン | UINT32 | 次の構造のバージョン番号。 このフィールドを設定する必要があります**1**この構造体のバージョン 1。 |
| 4 | 4 | AppCount | UINT32 | UICC アプリケーション数**MBIM_UICC_APP_INFO**この応答で返される構造体。 |
| 8 | 4 | ActiveAppIndex | UINT32(0..NumApp - 1) | モバイル、ネットワークへの登録用のモデムが選択したアプリケーションのインデックス。 このフィールドは、の間である必要があります**0**と**AppCount - 1**します。 この応答によって返されるアプリケーションの配列にインデックスを作成します。 このフィールドには登録のアプリケーションが選択されていない場合**0 xffffffff**します。 |
| 12 | 4 | AppListOffset | OFFSET | オフセット (バイト単位) は、アプリの一覧を格納しているバッファーには、この構造体の先頭から計算されます。 |
| 16 | 4 | AppListSize | SIZE (0..AppCount * 312) | 一覧のアプリ データのバイト単位のサイズ。 |
| 20 | AppListSize | DataBuffer | DATABUFFER | 配列の**AppCount** * **MBIM_UICC_APP_INFO**構造体。 |

#### <a name="mbimuiccappinfo"></a>MBIM_UICC_APP_INFO

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | appType | MBIM_UICC_APP_TYPE | UICC アプリケーションの種類。 |
| 4 | 4 | AppIdSize | サイズ (0..16) | (バイト単位) のセクションの 8.3 で定義されている、アプリケーション ID のサイズ、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 このフィールドの場合は 0 に設定されて、 **MBIMUiccAppTypeMf**、 **MBIMUiccAppTypeMfSIM**、または**MBIMUiccAppTypeMfRUIM**アプリの種類。 |
| 8 | 16 | AppId | バイト配列 | アプリケーション id。 最初のメッセージだけ**AppIdSize**バイトが意味を持ちます。 アプリケーション ID がより長い場合**MBIM_MAXLENGTH_APPID**最初のメッセージだけが、実際の長さを指定し、(バイト単位)、AppIdSize **MBIM_MAXLENGTH_APPID**バイトは、このフィールドにします。 このフィールドは有効な場合にのみ**AppType**ない**MBIMUiccAppTypeMf**、 **MBIMUiccAppTypeMfSIM**、または**MBIMUiccAppTypeMfRUIM**します。 |
| 24 | 4 | AppNameLength | サイズ (0..256) | アプリケーション名の文字の長さ。 |
| 28 | 256 | アプリ名 | ASCII 文字の配列 | アプリケーションの名前を指定する utf-8 文字列を返します。 このフィールドの長さがで指定された**AppNameLength**します。 長さがより大きいまたは等しい場合**MBIM_MAXLENGTH_APPNAME**バイト、このフィールドには、1 つ目が含まれています。 **MBIM_MAXLENGTH_APPNAME - 1**名のバイト数。 文字列が常に null で終了します。 |
| 284 | 4 | NumPins | サイズ (0..8) | 暗証番号 (pin) のアプリケーション参照の数。 要素の数、つまり**PinRef**が有効です。 仮想の R UIM 上のアプリケーションは、暗証番号 (pin) の参照を持つありません。 |
| 288 | 8 | PinRef | バイト配列 | 9.4.2 のセクションで定義されている (PIN1 および場合によっては UPIN keys)、このアプリケーション用のアプリケーションの暗証番号 (pin) を指定するバイト配列を参照、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 場合は単一検証カード、または、MBB ドライバーやモデムは、さまざまなアプリケーションの別のアプリケーション キーをサポートしていませんが、このフィールドにする必要があります**0x01**します。 |

#### <a name="mbimuiccapptype"></a>MBIM_UICC_APP_TYPE

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMUiccAppTypeUnknown | 0 | 不明な種類。 |
| MBIMUiccAppTypeMf | 1 | MF レガシ SIM ディレクトリをルートとします。 |
| MBIMUiccAppTypeMfSIM | 2 | レガシ SIM ディレクトリ、DF_GSM で root 化されます。 |
| MBIMUiccAppTypeMfRUIM | 3 | レガシ SIM ディレクトリ、DF_CDMA で root 化されます。 |
| MBIMUiccAppTypeUSIM | 4 | USIM アプリケーションです。 |
| MBIMUiccAppTypeCSIM | 5 | CSIM アプリケーション。 |
| MBIMUiccAppTypeISIM | 6 | ISIM アプリケーションです。 |

#### <a name="constants"></a>定数

次の定数は、MBIM_CID_MS_UICC_APP_INFO に対して定義されます。

`const int MBIM_MAXLENGTH_APPID = 16`  
`const int MBIM_MAXLENGTH_APPNAME = 256`  
`const int MBIM_MAXNUM_PINREF = 8`  

### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

次のステータス コードが、適用されます。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_BUSY | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_FAILURE | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC が見つからないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | UICC がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_NOT_INITIALIZED | UICC はまだ完全に初期化されていないため、UICC 操作を実行できません。 |

## <a name="mbimcidmsuiccfilestatus"></a>MBIM_CID_MS_UICC_FILE_STATUS

この CID では、指定した UICC ファイルに関する情報を取得します。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | MBIM_UICC_FILE_PATH | 該当なし |
| 応答 | 該当なし | MBIM_UICC_FILE_STATUS | 該当なし |

### <a name="query"></a>クエリ

MBIM_COMMAND_MSG InformationBuffer のでは、MBIM_UICC_FILE_PATH 構造体としてターゲット EF が含まれています。

#### <a name="mbimuiccfilepath-version-1"></a>MBIM_UICC_FILE_PATH (バージョン 1)

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | バージョン | UINT32 | 次の構造のバージョン番号。 このフィールドである必要があります**1**この構造体のバージョン 1。 |
| 4 | 4 | AppIdOffset | OFFSET | アプリケーション ID を含むバッファーをこの構造体の先頭からのオフセット (バイト単位) が計算されます。 |
| 8 | 4 | AppIdSize | サイズ (0..16) | (バイト単位) のセクションの 8.3 で定義されている、アプリケーション ID のサイズ、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 2 G カードでは、このフィールドはゼロ (0) に設定する必要があります。 |
| 12 | 4 | FilePathOffset | OFFSET | オフセット (バイト単位) は、ファイルのパスを含むバッファーには、この構造体の先頭から計算されます。 ファイルのパスは、16 ビットのファイル Id の配列です。 最初の ID はいずれかである必要があります**0x7FFF**または**0x3F00**します。 最初の ID が場合**0x7FFF**、によってアプリケーション desginated の ADF の相対パスですし、 **AppId**します。 それ以外の場合、MF から絶対パスになります。 |
| 16 | 4 | FilePathSize | サイズ (0..8) | ファイルのパス (バイト単位) のサイズ。 |
| 20 |   | DataBuffer | DATABUFFER | AppId とファイル パスを含むデータ バッファー。 |

### <a name="set"></a>Set

適用できません。

### <a name="response"></a>応答

次の MBIM_UICC_FILE_STATUS 構造は、InformationBuffer で使用されます。

#### <a name="mbimuiccfilestatus-version-1"></a>MBIM_UICC_FILE_STATUS (バージョン 1)

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | バージョン | UINT32 | 次の構造のバージョン番号。 このフィールドである必要があります**1**この構造体のバージョン 1。 |
| 4 | 4 | StatusWord1 | UINT32(0..256) | 戻り値パラメーター UICC コマンドに固有です。 |
| 8 | 4 | StatusWord2 | UINT32(0..256) | 戻り値パラメーター UICC コマンドに固有です。 |
| 12 | 4 | FileAccessibility | MBIM_UICC_FILE_ACCESSIBILITY | UICC ファイルのアクセシビリティ。 |
| 16 | 4 | FileType | MBIM_UICC_FILE_TYPE | UICC ファイルの種類。 |
| 20 | 4 | FileStructure | MBIM_UICC_FILE_STRUCTURE | UICC ファイルの構造体。 |
| 24 | 4 | ItemCount | UINT32 | UICC ファイル内の項目の数。 Transparent に設定されて TLV ファイル、および**1**します。 |
| 28 | 4 | サイズ | UINT32 | (バイト単位)、各項目のサイズ。 透過的な TLV ファイル、または全体の EF のサイズです。 ファイルのレコードに基づくレコードの合計数を表します。 |
| 32 | 16 | FileLockStatus | MBIM_PIN_TYPE_EX\[4\] | そのファイルの各操作 (読み取り、更新、アクティブ化、および非アクティブ化をこの順序で) のアクセス条件を記述する MBIM_PIN_TYPE_EX 型の配列。 |

#### <a name="mbimuiccfileaccessibility"></a>MBIM_UICC_FILE_ACCESSIBILITY

MBIM_UICC_FILE_ACCESSIBILITY 列挙体は、前述の MBIM_UICC_FILE_STATUS 構造で使用されます。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMUiccFileAccessibilityUnknown | 0 | ファイル共有性が不明です。 |
| MBIMUiccFileAccessibilityNotShareable | 1 | 共有できません。 ファイルです。 |
| MBIMUiccFileAccessibilityShareable | 2 | 共有可能なファイルです。 |

#### <a name="mbimuiccfiletype"></a>MBIM_UICC_FILE_TYPE

MBIM_UICC_FILE_TYPE 列挙体は、前述の MBIM_UICC_FILE_STATUS 構造で使用されます。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMUiccFileTypeUnknown | 0 | ファイルの種類が不明です。 |
| MBIMUiccFileTypeWorkingEf | 1 | EF の動作。 |
| MBIMUiccFileTypeInternalEf | 2 | EF の内部。 |
| MBIMUiccFileTypeDfOrAdf | 3 | 専用のファイルでは、他のノードの親であるディレクトリ。 DF または ADF 可能性があります。 |

#### <a name="mbimuiccfilestructure"></a>MBIM_UICC_FILE_STRUCTURE

MBIM_UICC_FILE_STRUCTURE 列挙体は、前述の MBIM_UICC_FILE_STATUS 構造で使用されます。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMUiccFileStructureUnknown | 0 | 不明なファイルの構造体。 |
| MBIMUiccFileStructureTransparent | 1 | 可変長の 1 つのレコード。 |
| MBIMUiccFileStructureCyclic | 2 | 同じ長さの各レコードの循環のセット。 |
| MBIMUiccFileStructureLinear | 3 | 同じ長さの各レコードの線形のセット。 |
| MBIMUiccFileStructureBerTLV | 4 | タグを使用してアクセスできるデータ値のセット。 |

#### <a name="mbimpintypeex"></a>MBIM_PIN_TYPE_EX

MBIM_PIN_TYPE_EX 列挙体は、前述の MBIM_UICC_FILE_STATUS 構造で使用されます。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMPinTypeNone | 0 | PIN が入力する保留中ではありません。 |
| MBIMPinTypeCustom | 1 | 暗証番号 (pin) の型は、カスタム型とは、他の種類の暗証番号 (pin) の一覧に表示されないこの列挙体。 |
| MBIMPinTypePin1 | 2 | PIN1 キー。 |
| MBIMPinTypePin2 | 3 | 暗証番号 2 キー。 |
| MBIMPinTypeDeviceSimPin | 4 | SIM のキーをデバイスです。 |
| MBIMPinTypeDeviceFirstSimPin | 5 | SIM の最初のキーをデバイスです。 |
| MBIMPinTypeNetworkPin | 6 | ネットワークのパーソナル化キー。 |
| MBIMPinTypeNetworkSubsetPin | 7 | ネットワークのサブセットのパーソナル化のキー。 |
| MBIMPinTypeServiceProviderPin | 8 | サービス プロバイダー (SP) パーソナル化のキー。 |
| MBIMPinTypeCorporatePin | 9 | 企業のパーソナル化のキー。 |
| MBIMPinTypeSubsidyLock | 10 | キー、subsidy のロックを解除します。 | 
| MBIMPinTypePuk1 | 11 | 個人識別番号 1 キー (PUK1) のロックを解除します。 |
| MBIMPinTypePuk2 | 12 | 個人識別番号 2 キー (PUK2) のロックを解除します。 |
| MBIMPinTypeDeviceFirstSimPuk | 13 | SIM の最初の PIN をデバイスには、キーがロックを解除します。 |
| MBIMPinTypeNetworkPuk | 14 | ネットワークのパーソナル化キーのロックを解除します。 |
| MBIMPinTypeNetworkSubsetPuk | 15 | ネットワークのサブセットのパーソナル化キーのロックを解除します。 |
| MBIMPinTypeServiceProviderPuk | 16 | サービス プロバイダー (SP) パーソナル化キーのロックを解除します。 |
| MBIMPinTypeCorporatePuk | 17 | 企業のパーソナル化キーのロックを解除します。 |
| MBIMPinTypeNev | 18 | NEV キー。 |
| MBIMPinTypeAdm | 19 | 管理者キー。 |

### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

次のステータス コードが、適用されます。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_BUSY | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_FAILURE | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC が見つからないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | UICC がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | 共有可能ではなく、別のアプリケーションによってアクセスされているために、ファイルを選択することはできません。 SIM によって返されるステータス ワードは、6985 です。 |

## <a name="mbimcidmsuiccaccessbinary"></a>MBIM_CID_MS_UICC_ACCESS_BINARY

構造体型で UICC バイナリ ファイルにアクセスする特定のコマンドを送信するこの CID **MBIMUiccFileStructureTransparent**または**MBIMUiccFileStructureBerTLV**します。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_UICC_ACCESS_BINARY | MBIM_UICC_ACCESS_BINARY | 該当なし |
| 応答 | MBIM_UICC_RESPONSE | MBIM_UICC_RESPONSE | 該当なし |

### <a name="query"></a>クエリ

バイナリ ファイルを読み取ります。 MBIM_COMMAND_MSG の InformationBuffer には MBIM_UICC_ACCESS_BINARY 構造体が含まれています。 MBIM_COMMAND_DONE の InformationBuffer MBIM_UICC_RESPONSE 構造体が返されます。

#### <a name="mbimuiccaccessbinary-version-1"></a>MBIM_UICC_ACCESS_BINARY (バージョン 1)

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | バージョン | UINT32 | 次の構造のバージョン番号。 このフィールドを設定する必要があります**1**この構造体のバージョン 1。 |
| 4 | 4 | AppIdOffset | OFFSET | アプリケーション ID を格納するバッファーへのこの構造体の先頭からのバイト単位のオフセット |
| 8 | 4 | AppIdSize | サイズ (0..16) | (バイト単位) のセクションの 8.3 で定義されている、アプリケーション ID のサイズ、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 2 G カードでは、このフィールドはゼロ (0) に設定する必要があります。 |
| 12 | 4 | FilePathOffset | OFFSET | オフセット (バイト単位) は、ファイルのパスを含むバッファーには、この構造体の先頭から計算されます。 ファイルのパスは、16 ビットのファイル Id の配列です。 最初の ID はいずれかである必要があります**0x7FFF**または**0x3F00**します。 最初の ID が場合**0x7FFF**、によってアプリケーション desginated の ADF の相対パスですし、 **AppId**します。 それ以外の場合、MF から絶対パスになります。 |
| 16 | 4 | FilePathSize | サイズ | ファイルのパス (バイト単位) のサイズ。 |
| 20 | 4 | fileOffset | UINT32 | ファイルから読み取るときに使用されるオフセット。 このフィールドは 256 より大きく、およびオフセット高と offset の両方で定義されている低が組み合わされています、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 |
| 24 | 4 | NumberOfBytes | UINT32 | 読み取るバイト数。 たとえば、クライアント ドライバーはこの関数のあたり 256 バイトが読み取りまたは単一 UICC 操作で書き込まれたができる最大量は 256 バイトより大きい、透過的な (バイナリ) ファイルを読み取るを使用できます、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 この複数 Apdu 複数に分割し、1 つの応答での結果を送信する関数の役目です。 |
| 28 | 4 | LocalPinOffset | OFFSET | オフセット (バイト単位) は、パスワードを含んでいるバッファーには、この構造体の先頭から計算されます。 これは、ローカルの PIN (暗証番号 2) であり、操作には、ローカルの PIN の検証が必要です。 場合に使用されます。 |
| 32 | 4 | LocalPinSize | サイズ (0..16) | (バイト単位)、パスワードのサイズ。 |
| 36 | 4 | BinaryDataOffset | OFFSET | オフセット (バイト単位) は、コマンドに固有のデータを格納しているバッファーには、この構造体の先頭から計算されます。 バイナリ データは、セットの操作にのみ使用されます。 |
| 40 | 4 | BinaryDataSize | サイズ (0..32768) | データのバイト単位のサイズ。 |
| 44 |   | DataBuffer | DATABUFFER | AppId、FilePath、LocalPin、およびデータを含むデータ バッファーです。 |

### <a name="set"></a>Set

透過的なファイルを更新します。 MBIM_COMMAND_MSG の InformationBuffer には MBIM_UICC_ACCESS_BINARY 構造体が含まれています。 MBIM_COMMAND_DONE の InformationBuffer MBIM_UICC_RESPONSE 構造体が返されます。

### <a name="response"></a>応答

次の MBIM_UICC_RESPONSE 構造は、InformationBuffer で使用されます。

#### <a name="mbimuiccresponse-version-1"></a>MBIM_UICC_RESPONSE (バージョン 1)

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | バージョン | UINT32 | 続いて、structurethat のバージョン番号。 このフィールドである必要があります**1**この構造体のバージョン 1。 |
| 4 | 4 | StatusWord1 | UINT32(0..256) | 戻り値パラメーター UICC コマンドに固有です。 |
| 8 | 4 | StatusWord2 | UINT32(0..256) | 戻り値パラメーター UICC コマンドに固有です。 |
| 12 | 4 | ResponseDataOffset | OFFSET | 計算されるこの構造体の先頭からの応答データを格納しているバッファーへのバイト オフセット。 応答データは、クエリ操作でのみ使用されます。 |
| 16 | 4 | ResponseDataSize | サイズ (0..32768) | データのバイト単位のサイズ。 |
| 20 |   | DataBuffer | DATABUFFER | ResponseData を含むデータ バッファーです。 |

### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

次のステータス コードが、適用されます。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_BUSY | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_FAILURE | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC が見つからないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | UICC がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | 共有可能ではなく、別のアプリケーションによってアクセスされているために、ファイルを選択することはできません。 SIM によって返されるステータス ワードは、6985 です。 |
| MBIM_STATUS_PIN_FAILURE | 暗証番号 (pin) エラーのため、操作が失敗しました。 |

## <a name="mbimcidmsuiccaccessrecord"></a>MBIM_CID_MS_UICC_ACCESS_RECORD

この CID UICC 線形固定または循環のファイルの構造型へのアクセスに特定のコマンドを送信する**MBIMUiccFileStructureCyclic**または**MBIMUIccFileStructureLinear**します。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_UICC_ACCESS_RECORD | MBIM_UICC_ACCESS_RECORD | 該当なし |
| 応答 | MBIM_UICC_RESPONSE | MBIM_UICC_RESPONSE | 該当なし |

### <a name="query"></a>クエリ

レコードの内容を読み取ります。 MBIM_COMMAND_MSG の InformationBuffer には、次の MBIM_UICC_ACCESS_RECORD 構造が含まれています。 MBIM_COMMAND_DONE の InformationBuffer MBIM_UICC_RESPONSE が返されます。

#### <a name="mbimuiccaccessrecord-version-1"></a>MBIM_UICC_ACCESS_RECORD (バージョン 1)

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | バージョン | UINT32 | 次の構造のバージョン番号。 このフィールドを設定する必要があります**1**この構造体のバージョン 1。 |
| 4 | 4 | AppIdOffset | OFFSET | アプリケーション ID を格納するバッファーへのこの構造体の先頭からのバイト単位のオフセット |
| 8 | 4 | AppIdSize | サイズ (0..16) | (バイト単位) のセクションの 8.3 で定義されている、アプリケーション ID のサイズ、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 2 G カードでは、このフィールドはゼロ (0) に設定する必要があります。 |
| 12 | 4 | FilePathOffset | OFFSET | オフセット (バイト単位) は、ファイルのパスを含むバッファーには、この構造体の先頭から計算されます。 ファイルのパスは、16 ビットのファイル Id の配列です。 最初の ID はいずれかである必要があります**0x7FFF**または**0x3F00**します。 最初の ID が場合**0x7FFF**、によってアプリケーション desginated の ADF の相対パスですし、 **AppId**します。 それ以外の場合、MF から絶対パスになります。 |
| 16 | 4 | FilePathSize | サイズ | ファイルのパス (バイト単位) のサイズ。 |
| 20 | 4 | RecordNumber | UINT32(0..256) | レコードの数。 これは、常に絶対のレコードのインデックスを表します。 モデムは (次に、前) のファイルに対して複数回アクセスを実行できるため、相対レコードへのアクセスがサポートされていません。 |
| 24 | 4 | LocalPinOffset | OFFSET | オフセット (バイト単位) は、パスワードを含んでいるバッファーには、この構造体の先頭から計算されます。 ロックのパスワードは、10 進数字の null で終わる utf-8 文字列です。 | 
| 28 | 4 | LocalPinSize | サイズ (0..16) | (バイト単位)、パスワードのサイズ。 |
| 32 | 4 | RecordDataOffset | OFFSET | オフセット (バイト単位) は、コマンドに固有のデータを格納しているバッファーには、この構造体の先頭から計算されます。 レコード データは、セットの操作にのみ使用されます。 |
| 36 | 4 | RecordDataSize | サイズ (0..256) | データのバイト単位のサイズ。 |
| 40 |   | DataBuffer | DATABUFFER | AppId、FilePath、LocalPin、および RecordData を含むデータ バッファーです。 |

### <a name="set"></a>Set

線形の固定または循環ファイルを更新します。 MBIM_COMMAND_MSG の InformationBuffer には、次の MBIM_UICC_ACCESS_RECORD 構造が含まれています。 MBIM_COMMAND_DONE の InformationBuffer MBIM_UICC_RESPONSE が返されます。

### <a name="response"></a>応答

MBIM_UICC_RESPONSE 構造体は、InformationBuffer で使用されます。

### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

次のステータス コードが、適用されます。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_BUSY | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_FAILURE | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC が見つからないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | UICC がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | 共有可能ではなく、別のアプリケーションによってアクセスされているために、ファイルを選択することはできません。 SIM によって返されるステータス ワードは、6985 です。 |
| MBIM_STATUS_PIN_FAILURE | 暗証番号 (pin) エラーのため、操作が失敗しました。 |

## <a name="mbimcidmspinex"></a>MBIM_CID_MS_PIN_EX

セクション 9 で定義されているすべてのピン留めするセキュリティ操作を実行するこの CID が使用される、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 CID は MBIM_CID_MS_PIN に似ていますが、マルチ アプリ UICC カードをサポートするように拡張します。 1 つの検証に対応 UICCs のみがサポートされています。 暗証番号 (pin) がサポートされていない 1 つ以上のアプリケーションをサポートするマルチ verification 対応 UICCs します。 1 つのアプリケーション (PIN1) 暗証番号 (pin) は、すべての ADFs/DFs と、UICC 上のファイルに割り当てられます。 ただし、各アプリケーションでは、すべてのアクセス コマンドの追加の検証が必要になり、レベル 2 のユーザーの検証要件として、ローカルの PIN (暗証番号 2) を指定できます。 このシナリオは、MBIM_CID_MS_PIN_EX がサポートしています。

MBIM_CID_MS_PIN と同じように MBIM_CID_MS_PIN_EX でデバイスを報告するだけ 1 つの PIN、時にします。 複数の Pin が有効になっているし、複数の Pin の報告を有効にも、機能する必要がありますを報告 PIN1 最初。 たとえば、subsidy ロックの報告を有効にすると、SIM の PIN1 が有効になっている、し subsidy ロック PIN に報告されます後続のクエリ要求 PIN1 が正常に検証された後にのみ。 MBIMPinOperationEnter と共に空の PIN が許可されます。 空の PIN を指定するには、PinSize を 0 に設定します。 この場合、SET コマンドでは、クエリに似ていて、参照ピンの状態を返します。 指定したセクション 11.1.9 の確認 コマンドの動作に整列されて完全、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_PIN_EX | MBIM_PIN_APP | 該当なし |
| 応答 | MBIM_PIN_INFO_EX | MBIM_PIN_INFO_EX | 該当なし |

### <a name="query"></a>クエリ

次の MBIM_PIN_APP 構造は、InformationBuffer で使用されます。

#### <a name="mbimpinapp-version-1"></a>MBIM_PIN_APP (バージョン 1)

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | バージョン | UINT32 | 次の構造のバージョン番号。 このフィールドを設定する必要があります**1**この構造体のバージョン 1。 |
| 4 | 4 | AppIdOffset | OFFSET | アプリケーション ID を格納するバッファーへのこの構造体の先頭からのバイト単位のオフセット |
| 8 | 4 | AppIdSize | サイズ (0..16) | (バイト単位) のセクションの 8.3 で定義されている、アプリケーション ID のサイズ、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 2 G カードでは、このフィールドはゼロ (0) に設定する必要があります。 |
| 12 |   | DataBuffer | DATABUFFER | 定義されている、AppId、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 |

### <a name="set"></a>Set

次の MBIM_SET_PIN_EX 構造は、InformationBuffer で使用されます。

#### <a name="mbimsetpinex"></a>MBIM_SET_PIN_EX

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PinType | MBIM_PIN_TYPE_EX | 暗証番号 (pin) の型。 このトピックの「MBIM_PIN_TYPE_EX テーブルを参照してください。 |
| 4 | 4 | PinOperation | MBIM_PIN_OPERATION | ピン留め操作です。 MBIM 1.0 を参照してください。 |
| 8 | 4 | PinOffset | OFFSET | 暗証番号 (pin)、操作を実行するための暗証番号 (pin) 値を表す文字列をこの構造体の先頭からのオフセット (バイト単位) が計算されますか、有効または PIN の設定を無効にするために必要な暗証番号 (pin) の値。 このフィールドはのすべての値に適用されます。 **PinOperation**します。 |
| 12 | 4 | PinSize | サイズ (0..32) | PIN の使用、バイト単位のサイズ。 |
| 16 | 4 | NewPinOffset | OFFSET | この構造体の先頭からのオフセット (バイト単位) が計算されます、 **NewPin**を設定するときに新しい PIN の値を表す文字列を**PinOperation**は MBIMPinOperationChange またはMBIMPinOperationEnter、PinTypeMBIMPinTypePuk1 または PinTypeMBIMPinTypePuk2 します。 |
| 20 | 4 | NewPinSize | サイズ (0..32) | 使用される、NewPin バイト サイズ。 |
| 24 | 4 | AppIdOffset | OFFSET | アプリケーション ID を含むバッファーをこの構造体の先頭からのオフセット (バイト単位) が計算されます。 |
| 28 | 4 | AppIdSize | サイズ (0..16) | (バイト単位) のセクションの 8.3 で定義されている、アプリケーション ID のサイズ、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 2 G カードでは、このフィールドはゼロ (0) に設定する必要があります。 |
| 32 |   | DataBuffer | DATABUFFER | 暗証番号 (pin)、NewPin、および AppId を含むデータ バッファー。 |

### <a name="response"></a>応答

次の MBIM_PIN_INFO_EX 構造は、InformationBuffer で使用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PinType | MBIM_PIN_TYPE_EX | 暗証番号 (pin) の型。 このトピックの「MBIM_PIN_TYPE_EX テーブルを参照してください。 |
| 4 | 4 | PinState | MBIM_PIN_STATE | 暗証番号 (pin) の状態。 MBIM 1.0 を参照してください。 |
| 8 | 4 | RemainingAttempts | UINT32 | 残り試行回数を有効にする、暗証番号 (pin) に関連する操作など」と入力します、または無効にします。 この情報をサポートしていないデバイスでは、このメンバーを 0 xffffffff に設定する必要があります。 |

### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

次のステータス コードが、適用されます。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_BUSY | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_FAILURE | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC が見つからないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | UICC がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_PIN_DISABLED | PIN が無効になっているため、操作に失敗しました。 |
| MBIM_STATUS_PIN_REQUIRED | 続行する PIN を入力する必要があるため操作に失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 暗証番号 (pin)、対応する型のセットが、デバイスでサポートされていないため、操作が失敗しました。 |
