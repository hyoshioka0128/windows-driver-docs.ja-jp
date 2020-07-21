---
title: MB 低レベル UICC アクセス
description: MB 低レベル UICC アクセス
ms.assetid: AD0E9F20-9C95-4102-94EF-054D45E2C597
keywords:
- MB 低レベル UICC アクセス、モバイルブロードバンド低レベル UICC アクセス、モバイルブロードバンドミニポートドライバーの低レベル UICC、MB UICC ATR、リセットするための MB UICC 応答、mb uicc オープンチャネル、mb UICC 終了チャネル、mb uicc APDU、mb uicc ターミナル機能、mb UICC リセット
ms.date: 12/05/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c3e33884b3c66879bde5f5c755a5f84805246eb9
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557761"
---
# <a name="mb-low-level-uicc-access"></a>MB 低レベル UICC アクセス

## <a name="overview"></a>概要

モバイルブロードバンドインターフェイスモデルリビジョン 1.0 (MBIM1) では、ホストデバイスと携帯データモデムの間に、OEM および IHV に依存しないインターフェイスが定義されています。

MBIM1 関数には、UICC スマートカードが含まれており、そのデータの一部と内部状態にアクセスできます。 ただし、スマートカードには、MBIM インターフェイスで定義されている以外の機能が追加されている場合があります。 これらの追加機能には、近距離通信に基づくモバイル支払いソリューションのセキュリティで保護された要素のサポート、または UICC プロファイル全体のリモートプロビジョニングが含まれます。

モバイルブロードバンド対応の Windows デバイスでは、MBIM インターフェイスが、ラジオインターフェイスレイヤー (RIL) インターフェイスに加えて使用されます。 RIL が提供する機能の1つは、UICC に低レベルでアクセスするためのインターフェイスです。 このトピックでは、mbim インターフェイスでこの追加機能を説明する、MBIM に対する Microsoft の拡張機能のセットについて説明します。

Microsoft 拡張機能は、一連のデバイスサービスコマンド (設定とクエリの両方) と通知を構成します。 これらの拡張機能には、デバイスサービスストリームの新しい使用は含まれていません。

## <a name="mbim-service-and-cid-values"></a>MBIM サービスと CID 値

| [サービス名] | UUID | UUID の値 |
| --- | --- | --- |
| Microsoft 低レベルの UICC アクセス | UUID_MS_UICC_LOW_LEVEL | C2F6588E-F037-4BC9-8665-F4D44BD09367 |

次の表は、各 CID のコマンドコードと、CID が Set、Query、または Event (通知) 要求をサポートしているかどうかを示しています。 パラメーター、データ構造、および通知の詳細については、このトピック内の各 CID の個別のセクションを参照してください。 

| CID | コマンドコード | オン | クエリ | 通知 |
| --- | --- | --- | --- | --- |
| MBIM_CID_MS_UICC_ATR | 1 | N | Y | N |
| MBIM_CID_MS_UICC_OPEN_CHANNEL | 2 | Y | × | N |
| MBIM_CID_MS_UICC_CLOSE_CHANNEL | 3 | Y | × | N |
| MBIM_CID_MS_UICC_APDU) | 4 | Y | × | N |
| MBIM_CID_MS_UICC_TERMINAL_CAPABILITY | 5 | Y | Y | N |
| MBIM_CID_MS_UICC_RESET | 6 | Y | Y | N |

## <a name="status-codes"></a>状態コード

MBIM の状態コードは、 [mbim 標準](https://go.microsoft.com/fwlink/p/?linkid=842064)の9.4.5 セクションで定義されています。 さらに、次のようなエラー状態コードが定義されています。

| 状態コード | 値 (16 進) | 説明 |
| --- | --- | --- |
| MBIM_STATUS_MS_NO_LOGICAL_CHANNELS | 87430001 | UICC で使用可能な論理チャネルがないため、論理チャネルを開くことができませんでした (サポートされていないか、それらのすべてが使用されています)。 |
| MBIM_STATUS_MS_SELECT_FAILED | 87430002 | SELECT に失敗したため、論理チャネルを開くことができませんでした。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 87430003 | 論理チャネル番号が無効です (MBIM_CID_MS_UICC_OPEN_CHANNEL によって開かれていません)。 |

### <a name="mbim_subscriber_ready_state"></a>MBIM_SUBSCRIBER_READY_STATE

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMSubscriberReadyStateNoEsimProfile | 7 | カードの準備ができていますが、有効なプロファイルがありません。 |

## <a name="uicc-responses-and-status"></a>UICC の応答とステータス

UICC は、文字ベースのインターフェイスとレコードベースのインターフェイスのいずれかまたは両方を実装する場合があります。 特定のメカニズムは異なりますが、結果として、UICC は2つのステータスバイト (SW1 と SW2) と応答 (空の場合があります) を持つ各コマンドに応答することになります。 正常な成功の状態は、90 00 によって示されます。 ただし、UICC でカード application toolkit がサポートされ、UICC がターミナルにプロアクティブコマンドを送信する必要がある場合、正常に返されるのは、状態が 91 XX (XX が異なる) であることを示します。 MBIM 関数 (ターミナル) は、他の UICC 操作中に受信したプロアクティブコマンドを処理するのと同様に、このプロアクティブコマンドを処理します (UICC にフェッチを送信する、プロアクティブコマンドを処理する、MBIM_CID_STK_PAC を使用してホストに送信するなど)。 MBIM ホストが MBIM_CID_MS_UICC_OPEN_CHANNEL または MBIM_CID_MS_UICC_APDU のいずれかを送信する場合、通常の状態として 90 00 と 91 XX の両方を考慮する必要があります。

コマンドは、256バイトを超える応答を返すことができる必要があります。 このメカニズムについては、 [ISO/IEC 7816-4:2013 標準](https://go.microsoft.com/fwlink/p/?linkid=864596)の5.1.3 セクションを参照してください。 この場合、カードは 90 00 ではなく、61 XX の SW1 SW2 ステータスワードを返します。ここで、XX は残りのバイト数か、256バイト以上がある場合は00です。 すべてのデータが受信されるまで、モデムは同じクラスバイトの GET 応答を繰り返し実行する必要があります。 これは、最後のステータスワード 90 00 によって示されます。 シーケンスは、特定の論理チャネル内で中断されないようにする必要があります。 追加の APDUs はモデムで処理される必要があり、ホストに対して透過的である必要があります。 ホストで処理された場合、APDUs のシーケンス中に他の APDU がそのカードを非同期に参照しているという保証はありません。

## <a name="comparison-to-ihvril"></a>IHVRIL との比較

5.2.3.3.10 から5.2.3.3.14 までのセクションでは、この仕様の基になる同様のインターフェイスを定義しています。 次のような違いがあります。

- RIL インターフェイスには、セキュリティで保護されたメッセージングを指定する方法は用意されていません。 APDUs を交換するための MBIM コマンドでは、これを明示的なパラメーターとして指定します。
- RIL インターフェイスは、APDU 内のクラスバイトの解釈を明確に定義しません。 MBIM 仕様では、ホストから送信されたクラスバイトは存在する必要がありますが、使用されていません (代わりに、MBIM 関数によってこのバイトが構築されます)。
- RIL インターフェイスは、グループ内のすべての UICC チャネルを閉じるために個別の関数を使用します。一方、MBIM インターフェイスでは、1つの CID に対する variant 引数を使用してこれを実現しています。
- MBIM エラー状態と UICC ステータス (SW1 SW2) の関係は、RIL エラーと UICC ステータスの関係よりも明確に定義されています。
- MBIM インターフェイスは、新しい論理チャネルを失敗から割り当てて、指定されたアプリケーションを選択できないことを識別します。
- MBIM インターフェイスは、カードに送信するモデムターミナル機能オブジェクトの送信を許可します。

## <a name="mbim_cid_ms_uicc_atr"></a>MBIM_CID_MS_UICC_ATR

リセットの解答 (ATR) は、リセットが実行された後に UICC によって送信された最初のバイトの文字列です。 サポートされている論理チャネルの数など、カードの機能について説明します。 MBIM 関数は、UICC から受信したときに、ATR を保存する必要があります。 その後、ホストは MBIM_CID_MS_UICC_ATR コマンドを使用して ATR を取得できます。

### <a name="parameters"></a>パラメーター

|   | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 適用なし | Empty | 適用なし |
| 応答 | 適用なし | MBIM_MS_ATR_INFO | 適用なし |

### <a name="query"></a>クエリ

クエリメッセージの InformationBuffer が空です。 

### <a name="set"></a>オン

適用不可。

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer には、この関数にアタッチされている UICC に対してリセットする応答を記述する次の MBIM_MS_ATR_INFO 構造が含まれています。

#### <a name="mbim_ms_atr_info"></a>MBIM_MS_ATR_INFO

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | AtrSize/ | サイズ (0.. 33) | **AtrData**の長さ。 |
| 4 | 4 | AtrOffset | OFFSET | この構造体の先頭から計算された、 **AtrData**と呼ばれるバイト配列に、ATR データを格納しているバイト単位のオフセット。 |
| 8 | AtrSize/ | DataBuffer | DATABUFFER | **AtrData**バイト配列。 |

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

## <a name="mbim_cid_ms_uicc_open_channel"></a>MBIM_CID_MS_UICC_OPEN_CHANNEL

ホストは、MBIM_CID_MS_UICC_OPEN_CHANNEL コマンドを使用して、関数が UICC カード上の新しい論理チャネルを開き、指定された UICC (アプリケーション ID で指定された) アプリケーションを選択するように要求します。

関数は、UICC コマンドのシーケンスを使用して、この MBIM コマンドを実装します。

1.  この関数は、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション11.1.17 の説明に従って、管理チャネルコマンドを uicc に送信して、新しい論理チャネルを作成します。 このコマンドが失敗した場合、この関数は、MBIM_STATUS_MS_NO_LOGICAL_CHANNELS 状態を SW1 SW2 に戻し、それ以上の操作を行いません。 
2.  [チャネルの管理] コマンドが成功した場合、UICC は新しい論理チャネルのチャネル番号を関数に報告します。 関数は、 [ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション11.1.1 で説明されているように、P1 = 04 という名前の SELECT [by name] コマンドを送信します。 この操作が失敗した場合、関数は、管理チャネルコマンドを UICC に送信して論理チャネルを閉じ、SELECT から SW1 SW2 を使用して MBIM_STATUS_MS_SELECT_FAILED の状態を返します。
3.  SELECT コマンドが成功した場合、この関数は、後で参照するためにホストによって指定された論理チャネル番号とチャネルグループを記録します。 次に、論理チャネル番号、選択からの SW1 SW2、および SELECT からホストへの応答が返されます。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_UICC_OPEN_CHANNEL | 適用なし | 適用なし |
| 応答 | MBIM_MS_UICC_OPEN_CHANNEL_INFO | 適用なし | 適用なし |

### <a name="query"></a>クエリ

適用不可。

### <a name="set"></a>オン

MBIM_COMMAND_MSG の InformationBuffer には、次の MBIM_MS_SET_UICC_OPEN_CHANNEL 構造が含まれています。

#### <a name="mbim_ms_set_uicc_open_channel"></a>MBIM_MS_SET_UICC_OPEN_CHANNEL

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | AppIdSize | サイズ (0.. 32) | アプリケーション ID (AppId) のサイズ。 |
| 4 | 4 | AppIdOffset | OFFSET | この構造体の先頭から計算された、選択する AppId を定義する**appid**と呼ばれるバイト配列へのオフセット (バイト単位)。 |
| 8 | 4 | SelectP2Arg | UINT32 (0.. 255) | SELECT コマンドの*P2*引数。 |
| 12 | 4 | ChannelGroup | UINT32 | このチャネルのチャネルグループを識別するタグ値。 |
| 16 | AppIdSize | DataBuffer | DATABUFFER | **AppId**バイト配列。 |

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer には、次の MBIM_MS_UICC_OPEN_CHANNEL_INFO 構造が含まれています。

#### <a name="mbim_ms_uicc_open_channel_info"></a>MBIM_MS_UICC_OPEN_CHANNEL_INFO

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Status | バイト [2] | このバイト順での SW1 と SW2。 詳細については、この表の次のメモを参照してください。 |
| 4 | 4 | チャネル | UINT32 (0.. 19) | 論理チャネル識別子。 このメンバーが0の場合、操作は失敗します。 |
| 8 | 4 | ResponseLength | サイズ (0 ~ 256) | 応答の長さ (バイト単位)。 |
| 12 | 4 | ResponseOffset | OFFSET | この構造体の先頭から計算されたバイト配列へのオフセット (バイト単位)。これは、SELECT からの応答を含む**応答**と呼ばれるバイト配列になります。 |
| 16 | - | DataBuffer | DATABUFFER | **応答**バイト配列データ。 |

コマンドが MBIM_STATUS_MS_NO_LOGICAL_CHANNELS を返す場合、 **status**フィールドには、[チャネルの管理] コマンドの uicc ステータスワード SW1 と SW2 が含まれており、残りのフィールドは0になります。 コマンドが MBIM_STATUS_MS_SELECT_FAILED を返す場合、 **status**フィールドには SELECT コマンドの uicc ステータスワード SW1 と SW2 が含まれ、残りのフィールドはゼロになります。 その他の状態の場合、InformationBuffer は空である必要があります。

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
| MBIM_STATUS_MS_NO_LOGICAL_CHANNELS | UICC で使用可能な論理チャネルがないため、論理チャネルを開くことができませんでした (サポートされていないか、それらのすべてが使用されています)。 |
| MBIM_STATUS_MS_SELECT_FAILED | SELECT に失敗したため、論理チャネルを開くことができませんでした。 |

## <a name="mbim_cid_ms_uicc_close_channel"></a>MBIM_CID_MS_UICC_CLOSE_CHANNEL

ホストは、UICC の論理チャネルを閉じるために MBIM_CID_MS_UICC_CLOSE_CHANNEL を関数に送信します。 ホストは、チャネル番号を指定することも、チャネルグループを指定することもできます。

ホストがチャネル番号を指定する場合、関数は、このチャネルが前の MBIM_CID_MS_UICC_OPEN_CHANNEL によって開かれたかどうかを確認する必要があります。 その場合は、チャネルの管理コマンドを UICC に送信してチャネルを閉じ、MBIM_STATUS_SUCCESS の状態を返して、MANAGE CHANNEL から SW1 SW2 を返します。 そうでない場合は、何も処理を行わず、MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL エラー状態を返します。

ホストでチャネルグループが指定されている場合、この関数は、チャネルグループを使用して開いた論理チャネルがあるかどうかを判断し、そのようなチャネルごとに UICC に管理チャネルコマンドを送信します。 最後に管理するチャネルの SW2 の MBIM_STATUS_SUCCESS 状態を返します。 チャネルが閉じられていない場合は、90 00 を返します。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_UICC_CLOSE_CHANNEL | 適用なし | 適用なし |
| 応答 | MBIM_MS_UICC_CLOSE_CHANNEL_INFO | 適用なし | 適用なし |

### <a name="query"></a>クエリ

適用不可。

### <a name="set"></a>オン

MBIM_COMMAND_MSG の InformationBuffer には、次の MBIM_MS_SET_UICC_CLOSE_CHANNEL 構造が含まれています。

#### <a name="mbim_ms_set_uicc_close_channel"></a>MBIM_MS_SET_UICC_CLOSE_CHANNEL

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | チャネル | UINT32 (0.. 19) | 0以外の場合、閉じるチャネルを指定します。 0の場合は、 **Channelgroup**に関連付けられているチャネルを閉じるように指定します。 |
| 4 | 4 | ChannelGroup | UINT32 | **Channel**が0の場合、タグ値が指定され、このタグを持つすべてのチャネルが閉じられます。 **Channel**が0以外の場合、このフィールドは無視されます。

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer には、次の MBIM_MS_UICC_CLOSE_CHANNEL_INFO 構造が含まれています。

#### <a name="mbim_ms_uicc_close_channel_info"></a>MBIM_MS_UICC_CLOSE_CHANNEL_INFO

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Status | バイト [2] | このコマンドの代わりに関数によって実行された最後の MANAGE CHANNEL の SW1 と SW2。 |

### <a name="unsolicited-events"></a>一方的なイベント

適用不可。

### <a name="status-codes"></a>状態コード

| status code | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_BUSY | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_FAILURE | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC がないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | Uicc がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_NOT_INITIALIZED | Uicc がまだ完全に初期化されていないため、UICC 操作を実行できません。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 論理チャネル番号が無効です (つまり、MBIM_CID_MS_UICC_OPEN_CHANNEL で開かれていません)。 |

## <a name="mbim_cid_ms_uicc_apdu"></a>MBIM_CID_MS_UICC_APDU

ホストは、MBIM_CID_MS_UICC_APDU を使用して、UICC 上の指定された論理チャネルにコマンド APDU を送信し、応答を受信します。 MBIM 関数は、論理チャネルが以前に MBIM_CID_MS_UICC_OPEN_CHANNEL で開かれていることを確認し、状態が MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL でない場合は失敗します。

ホストは、完全な APDU を関数に送信する必要があります。 APDU は、 [ISO/IEC 7816-4:2013 標準](https://go.microsoft.com/fwlink/p/?linkid=864596)のセクション4で定義されているクラスバイト値、または[ETSI TS 102 221 Technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション10.1.1 の拡張定義で送信される場合があります。 APDU は、セキュリティで保護されたメッセージングまたはセキュリティで保護されたメッセージングを使用せずに送信できます。 コマンドヘッダーは認証されていません。 ホストは、APDU と共に、クラスバイト、論理チャネル番号、およびセキュリティで保護されたメッセージングの種類を指定します。

コマンド APDU の最初のバイトは、 [ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)の[ISO/IEC 7816-4:2013 標準](https://go.microsoft.com/fwlink/p/?linkid=864596)またはセクション10.1.1 のセクション4で定義されているようにコード化されたクラスバイトです。 ホストは、0X、4X、6X、8X、CX、EX の各クラスバイトを送信する場合があります。 ただし、この関数は、UICC にこのバイトを直接渡しません。 代わりに、APDU を UICC に送信する前に、ホストによって指定された型、チャネル、および SecureMessaging の値に基づいて、ホストの最初のバイトを新しいクラスバイト ( [ISO/IEC 7816-4:2013 標準](https://go.microsoft.com/fwlink/p/?linkid=864596)のセクション4で定義された、または[ETSI TS 102 221 technical specification](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション10.1.1 によってエンコードされた) に置き換えます。

| Byte クラス | 説明 |
| --- | --- |
| 60 | 7816-4 インター産業、1 <= channel <= 3、該当する場合は低いニブルでセキュリティをエンコードする |
| 4 | 7816-4 インター産業、4 <= channel <= 19、セキュリティで保護されたメッセージングなし |
| 6X | 7816-4 インター産業、4 <= channel <= 19、secure (ヘッダー未認証) |
| 読み取れ | 102 221 extended、1<= channel <= 3、該当する場合は低ニブルのセキュリティをエンコードします。 |
| CX | 102 221 拡張、4 <= channel <= 19、セキュリティで保護されたメッセージングなし |
| EX | 102 221 拡張、4 <= channel <= 19、secure (ヘッダー未認証) |

関数は、UICC からホストに状態、SW1 SW2、および応答を返す必要があります。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_UICC_APDU | 適用なし | 適用なし |
| 応答 | MBIM_MS_UICC_APDU_INFO | 適用なし | 適用なし |

### <a name="query"></a>クエリ

適用不可。

### <a name="set"></a>オン

MBIM_COMMAND_MSG の InformationBuffer には、次の MBIM_MS_SET_UICC_APDU 構造が含まれています。

#### <a name="mbim_ms_set_uicc_apdu"></a>MBIM_MS_SET_UICC_APDU

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | チャネル | UINT32 (1.. 19) | APDU を送信するチャネルを指定します。 |
| 4 | 4 | SecureMessaging | MBIM_MS_UICC_SECURE_MESSAGING | セキュリティで保護されたメッセージングを使用して APDU を交換するかどうかを指定します。 |
| 8 | 4 | 種類 | MBIM_MS_UICC_CLASS_BYTE_TYPE | クラスのバイト定義の種類を指定します。 |
| 12 | 4 | CommandSize | UINT32 (0.. 261) | **コマンド**の長さ (バイト単位)。 |
| 16 | 4 | ド Doffset | OFFSET | この構造体の先頭から、APDU を含む**コマンド**と呼ばれるバイト配列へのオフセット (バイト単位)。 |
| 20 | - | DataBuffer | DATABUFFER | **コマンド**バイト配列。 |

MBIM_MS_SET_UICC_APDU 構造体は、次の MBIM_MS_UICC_SECURE_MESSAGING と MBIM_MS_UICC_CLASS_BYTE_TYPE データ構造を使用します。

##### <a name="mbim_ms_uicc_secure_messaging"></a>MBIM_MS_UICC_SECURE_MESSAGING

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMMsUiccSecureMessagingNone | 0 | セキュリティで保護されたメッセージングはありません。 |
| MBIMMsUiccSecureMessagingNoHdrAuth | 1 | セキュリティで保護されたメッセージング、コマンドヘッダーは認証されていません。 |

##### <a name="mbim_ms_uicc_class_byte_type"></a>MBIM_MS_UICC_CLASS_BYTE_TYPE

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMMsUiccInterindustry | 0 | ISO 7816-4 の最初の業界の定義に従って定義されます。 |
| MBIMMsUiccExtended | 1 | ETSI 102 221 の拡張定義に従って定義されます。 |

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer には、次の MBIM_MS_UICC_APDU_INFO 構造が含まれています。

#### <a name="mbim_ms_uicc_apdu_info"></a>MBIM_MS_UICC_APDU_INFO

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | Status | バイト [2] | コマンドの結果として生成された SW1 と SW2 のステータスワード。 |
| 4 | 4 | ResponseLength | SIZE | 応答の長さ (バイト単位)。 |
| 8 | 4 | ResponseOffset | OFFSET | この構造体の先頭から計算されたバイト配列へのオフセット (バイト単位)。これは、SELECT からの応答を含む**応答**と呼ばれるバイト配列になります。 |
| 12 | - | DataBuffer | DATABUFFER | **応答**のバイト配列。 |

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
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 論理チャネル番号が無効です (つまり、MBIM_CID_MS_UICC_OPEN_CHANNEL で開かれていません)。 |

関数が、UICC に APDU を送信できる場合、SW2 ステータスワードと、UICC からの応答 (存在する場合) と共に MBIM_STATUS_SUCCESS を返します。 ホストは状態 (SW1 SW2) を調べて、UICC で APDU コマンドが成功したかどうか、または失敗した理由を確認する必要があります。

## <a name="mbim_cid_ms_uicc_terminal_capability"></a>MBIM_CID_MS_UICC_TERMINAL_CAPABILITY

ホストは MBIM_CID_MS_UICC_TERMINAL_CAPABILITY を送信して、ホストの機能についてモデムに通知します。 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション11.1.19 に記載されているターミナル機能 APDU は、最初のアプリケーションが選択される前にカードに送信される必要があります (サポートされている場合)。 このため、ホストはターミナル機能の APDU を直接送信することはできませんが、その代わりに、モデムによって永続的に格納される1つ以上のターミナル機能オブジェクトを含む MBIM_CID_MS_UICC_TERMINAL_CAPABILITY コマンドを送信します。 次のカードの挿入時またはリセット時に、ATR の後に、モデムは MF を選択し、ターミナル機能がサポートされているかどうかを確認します。 その場合、モデムは、MBIM_CID_MS_UICC_TERMINAL_CAPABILITY コマンドで指定された情報と、モデムによって生成された情報を使用して、ターミナル機能の APDU を送信します。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_UICC_TERMINAL_CAPABILITY | Empty | 適用なし |
| 応答 | 適用なし | MBIM_MS_TERMINAL_CAPABILITY_INFO | 適用なし |

### <a name="query"></a>クエリ

InformationBuffer は null にする必要があり、InformationBufferLength は0である必要があります。

### <a name="set"></a>オン

MBIM_COMMAND_MSG の InformationBuffer には、次の MBIM_MS_SET_UICC_TERMINAL_CAPABILITY 構造が含まれています。

#### <a name="mbim_ms_set_uicc_terminal_capability"></a>MBIM_MS_SET_UICC_TERMINAL_CAPABILITY

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount | UINT32 | ターミナル機能オブジェクトの要素数。 |
| 4 | 8 * EC | CapabilityList OL_PAIR_LIST| 各ターミナル機能オブジェクト TLV のオフセット長ペアの一覧。 |
| 4 + 8 * EC | - | DataBuffer | DATABUFFER | 実際のターミナル機能オブジェクト TLVs のバイト配列。 |

### <a name="response"></a>応答

応答には、最後に送信されたターミナル機能オブジェクトと共に、正確な SET コマンドが格納されます。 したがって、MBIM_MS_TERMINAL_CAPABILITY_INFO は MBIM_MS_SET_UICC_TERMINAL_CAPABILITY と同じです。

#### <a name="mbim_ms_terminal_capability_info"></a>MBIM_MS_TERMINAL_CAPABILITY_INFO

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount | UINT32 | ターミナル機能オブジェクトの要素数。 |
| 4 | 8 * EC | CapabilityList OL_PAIR_LIST| 各ターミナル機能オブジェクト TLV のオフセット長ペアの一覧。 |
| 4 + 8 * EC | - | DataBuffer | DATABUFFER | 実際のターミナル機能オブジェクト TLVs のバイト配列。 |

### <a name="unsolicited-events"></a>一方的なイベント

適用不可。

### <a name="status-codes"></a>状態コード

| status code | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_BUSY | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_FAILURE | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC がないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | Uicc がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_NOT_INITIALIZED | Uicc がまだ完全に初期化されていないため、UICC 操作を実行できません。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 論理チャネル番号が無効です (つまり、MBIM_CID_MS_UICC_OPEN_CHANNEL で開かれていません)。 |

## <a name="mbim_cid_ms_uicc_reset"></a>MBIM_CID_MS_UICC_RESET

ホストは、MBIM 関数に MBIM_CID_MS_UICC_RESET を送信して UICC をリセットするか、関数のパススルー状態を照会します。

関数が UICC をリセットしたことをホストが要求すると、パススルーアクションを指定します。

ホストが*MBIMMsUICCPassThroughEnable*パススルーアクションを指定した場合、関数は uicc をリセットし、uicc 電源をオンにすると、uicc はホストと uicc 間の通信を可能にするパススルーモードであるかのように処理されます (Uicc に通信 uicc ファイルシステムがない場合でも)。 関数は、APDUs をカードに送信するのではなく、ホストと UICC 間の通信を使用していつでも邪魔になることはありません。

ホストで*MBIMMsUICCPassThroughDisable*パススルーアクションが指定されている場合、関数は uicc をリセットし、uicc 電源をオンにすると、uicc を通常の通信用 uicc として扱い、通信 uicc ファイルシステムが uicc に存在することを想定します。

ホストが関数に対してクエリを行い、パススルーの状態を判断すると、その関数が*MBIMMsUICCPassThroughEnabled*ステータスで応答する場合は、パススルーモードが有効になっていることを意味します。 関数が*MBIMMsUICCPassThroughDisabled*状態で応答する場合は、パススルーモードが無効になっていることを意味します。

### <a name="parameters"></a>パラメーター

|   | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_UICC_RESET | Empty | 適用なし |
| 応答 | MBIM_MS_UICC_RESET_INFO | MBIM_MS_UICC_RESET_INFO | 適用なし |

### <a name="query"></a>クエリ

InformationBuffer は null にする必要があり、 *Informationbufferlength*は0である必要があります。

### <a name="set"></a>オン

#### <a name="mbim_set_ms_uicc_reset"></a>MBIM_SET_MS_UICC_RESET

MBIM_SET_MS_UICC_RESET 構造体には、ホストによって指定されたパススルーアクションが含まれています。

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | アクションの実行 | MBIM_MS_UICC_PASSTHROUGH_ACTION | 詳細については、「 [MBIM_MS_UICC_PASSTHROUGH_ACTION](#mbim_ms_uicc_passthrough_action)」を参照してください。 |

#### <a name=""></a><a name="mbim_ms_uicc_passthrough_action">MBIM_MS_UICC_PASSTHROUGH_ACTION</a>

MBIM_MS_UICC_PASSTHROUGH_ACTION 列挙体は、ホストが MBIM 関数に指定できるパススルーアクションの種類を定義します。

| 種類 | 値 |
| --- | --- |
| MBIMMsUiccPassThroughDisable | 0 |
| MBIMMsUiccPassThroughEnable | 1 |

### <a name="response"></a>応答

#### <a name="mbim_ms_uicc_reset_info"></a>MBIM_MS_UICC_RESET_INFO

MBIM_MS_UICC_RESET_INFO 構造体には、MBIM 関数のパススルーステータスが格納されます。

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 状態の状態 | MBIM_MS_UICC_PASSTHROUGH_STATUS | 詳細については、「 [MBIM_MS_UICC_PASSTHROUGH_STATUS](#mbim_ms_uicc_passthrough_status)」を参照してください。 |

#### <a name=""></a><a name="mbim_ms_uicc_passthrough_status">MBIM_MS_UICC_PASSTHROUGH_STATUS</a> 

MBIM_MS_UICC_PASSTHROUGH_STATUS 列挙体は、MBIM 関数がホストに対して指定するパススルーステータスの種類を定義します。

| 種類 | 値 |
| --- | --- |
| MBIMMsUiccPassThroughDisabled | 0 |
| MBIMMsUiccPassThroughEnabled | 1 |

### <a name="unsolicited-events"></a>一方的なイベント

適用不可。

### <a name="status-codes"></a>状態コード

| status code | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | すべてのコマンドに対して定義されている基本的な MBIM ステータス。 |
| MBIM_STATUS_BUSY | デバイスがビジー状態です。 |
| MBIM_STATUS_FAILURE | 操作が失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスはこの操作をサポートしていません。 |

### <a name="oid_wwan_uicc_reset"></a>OID_WWAN_UICC_RESET

MBIM_CID_MS_UICC_RESET に対応する NDIS は[OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)です。 


