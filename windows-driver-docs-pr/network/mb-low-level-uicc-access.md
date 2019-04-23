---
title: MB 低レベル UICC アクセス
description: MB 低レベル UICC アクセス
ms.assetid: AD0E9F20-9C95-4102-94EF-054D45E2C597
keywords:
- 低レベルの MB UICC アクセス、低レベルのモバイル ブロード バンド UICC アクセス、モバイル ブロード バンド ミニポート ドライバー低レベルをリセット、MB UICC UICC、MB UICC ATR、MB UICC 応答チャネルを開く、MB UICC がチャネル、MB UICC APDU、MB UICC 端末の機能を閉じるには、MB UICC のリセット
ms.date: 12/05/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 054970b6946cfe290e978f7c4634c7cdf61362b4
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903320"
---
# <a name="mb-low-level-uicc-access"></a>MB 低レベル UICC アクセス

## <a name="overview"></a>概要

ブロード バンド インターフェイス モデルの Mobile リビジョン 1.0、または MBIM1、ホスト デバイスと、携帯データ ネットワークのモデムの OEM および IHV に依存しないインターフェイスを定義します。

MBIM1 関数は、UICC スマート カードが含まれていて、一部のデータと内部状態へのアクセスを提供します。 ただし、スマート カードには、MBIM インターフェイスによって定義されているもの以外の他の機能があります。 これらの追加機能には、近距離通信、に基づいてモバイル ペイメント ソリューションのプロビジョニング、またはリモート UICC プロファイル全体のセキュリティで保護された要素のサポートが含まれます。

モバイル ブロード バンドが有効な Windows デバイス、無線インターフェイス層 (RIL) インターフェイスだけでなく、MBIM インターフェイスを使用します。 RIL が提供する機能の 1 つは、低レベルのアクセス、UICC するインターフェイスです。 このトピックでは、MBIM インターフェイスでこの追加機能を記述する MBIM に Microsoft の拡張のセットについて説明します。

Microsoft 拡張機能には、一連のデバイスのサービスのコマンド (セットおよびクエリの両方) と通知が構成されています。 これらの拡張機能は、デバイス サービス ストリームの新しい用途を含めないでください。

## <a name="mbim-service-and-cid-values"></a>MBIM サービスと CID 値

| サービス名 | UUID | UUID 値 |
| --- | --- | --- |
| Microsoft UICC の低レベルのアクセス | UUID_MS_UICC_LOW_LEVEL | C2F6588E-F037-4BC9-8665-F4D44BD09367 |

次の表は、設定、CID がサポートするかどうかも、各 CID のコマンド コードを指定、クエリ、またはイベント (通知) を要求します。 詳細については、パラメーター、データ構造、および通知の詳細については、このトピック内の各 CID の個々 のセクションを参照してください。 

| CID | コマンド コード | 設定 | クエリ | 通知 |
| --- | --- | --- | --- | --- |
| MBIM_CID_MS_UICC_ATR | 1 | N | Y | N |
| MBIM_CID_MS_UICC_OPEN_CHANNEL | 2 | Y | N | N |
| MBIM_CID_MS_UICC_CLOSE_CHANNEL | 3 | Y | N | N |
| MBIM_CID_MS_UICC_APDU) | 4 | Y | N | N |
| MBIM_CID_MS_UICC_TERMINAL_CAPABILITY | 5 | Y | Y | N |
| MBIM_CID_MS_UICC_RESET | 6 | Y | Y | N |

## <a name="status-codes"></a>状態コード

MBIM 状態コードがの 9.4. 5. で定義されている、 [MBIM 標準](https://go.microsoft.com/fwlink/p/?linkid=842064)します。 さらに、次の追加のエラー ステータス コードが定義されています。

| 状態コード | 値 (16 進数) | 説明 |
| --- | --- | --- |
| MBIM_STATUS_MS_NO_LOGICAL_CHANNELS | 87430001 | 開いている論理チャネルは、UICC で利用できる論理チャネルがないために失敗しました (それらがサポートしていないか、使用中のすべての状態に)。 |
| MBIM_STATUS_MS_SELECT_FAILED | 87430002 | 選択に失敗したため、論理のチャネルをオープンに失敗しました。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 87430003 | 論理のチャンネル番号が無効です (MBIM_CID_MS_UICC_OPEN_CHANNEL によってが開いていない)。 |

### <a name="mbimsubscriberreadystate"></a>MBIM_SUBSCRIBER_READY_STATE

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMSubscriberReadyStateNoEsimProfile | 7 | カードは、準備ができてが有効になっているプロファイルではありません。 |

## <a name="uicc-responses-and-status"></a>UICC 応答と状態

文字ベースまたはレコード ベースのインターフェイス、またはその両方、UICC を実装できます。 特定のメカニズムは別ですが、結果は、2 つの状態のバイト数が (SW1 と SW2 という名前) および (空にすることがあります) が応答して、UICC が各コマンドに応答します。 通常の成功の状態が 90 で示されます 00 です。 ただし、UICC カード アプリケーション ツールキットをサポートしています、UICC がターミナルに事前対応型のコマンドを送信する必要がある場合は、(XX は異なります) 91 XX の状態が正常に返されたが示されます。 MBIM 関数、またはターミナルでは処理されます (送信、FETCH、UICC を事前対応型のコマンドの処理または MBIM_ でホストに送信するその他の UICC 操作中に受信した事前対応型のコマンドと同様、このプロアクティブ コマンドを処理します。CID_STK_PAC)。 90 の両方を考慮する必要があります MBIM_CID_MS_UICC_OPEN_CHANNEL または MBIM_CID_MS_UICC_APDU MBIM ホストが送信するとき、正常な状態として XX を 00 と 91。

コマンドは、256 バイトよりも大きい応答を返すできる必要があります。 このメカニズムがの 5.1.3 のセクションで説明されている、 [ISO/IEC 7816-標準 4:2013](https://go.microsoft.com/fwlink/p/?linkid=864596)します。 カードが 90 ではなく、61 XX の SW1 SW2 ステータス ワードを返すここでは、00、XX は残りのバイト数または 00 256 バイトまたは複数の残りがある場合。 モデムする必要があります発行 GET 応答で、同じクラス バイト繰り返しのすべてのデータを受信するまで。 最終ステータス ワード 90 を示される 00 です。 シーケンスは、特定の論理チャネル内で中断されたことがあります。 追加 Apdu はモデムで処理する必要があり、ホストに透過的にする必要があります。 ホストで処理される場合、[apdu] いくつかが可能性があります Apdu のシーケンス中にカードを参照非同期にする保証はありません。

## <a name="comparison-to-ihvril"></a>IHVRIL との比較

IHVRIL 仕様の 5.2.3.3.14 を通じて 5.2.3.3.10 のセクションでは、この仕様の基になるようなインターフェイスを定義します。 いくつかの違いは次のとおりです。

- RIL インターフェイスでは、セキュリティで保護されたメッセージングを指定する方法は提供されません。 Apdu を交換する MBIM コマンドは、明示的なパラメーターとして、これを指定します。
- RIL インターフェイスは、[apdu] 内のクラスのバイトの解釈を明確に定義されません。 ホストから送信されたクラス バイトにする必要がある MBIM 仕様の状態の表示は使用されていません (および MBIM 関数がこのバイトを構築する代わりに)。
- RIL インターフェイスでは、MBIM インターフェイスでは、これを実現 CID を 1 つのバリアント型引数と一方に、グループ内のすべての UICC チャネルを閉じるに個別の関数を使用します。
- MBIM エラー状態と UICC 状態 (SW1 SW2) 間のリレーションシップは RIL エラーと UICC 状態間のリレーションシップをより明確に定義されています。
- MBIM インターフェイスは、指定したアプリケーションを選択して障害からの新しい論理チャネルの割り当ての失敗を区別します。
- MBIM インターフェイスは、モデム カードに送信するための端末の機能のオブジェクトの送信を許可します。

## <a name="mbimcidmsuiccatr"></a>MBIM_CID_MS_UICC_ATR

回答をリセット (ATR) は、リセットが実行された後に、UICC によって送信されたバイト数の最初の文字列です。 これには、カードではサポートされている論理のチャネルの数などの機能について説明します。 MBIM 関数は、UICC から受信したときに、ATR を保存する必要があります。 その後、ホストは、ATR を取得するのに MBIM_CID_MS_UICC_ATR コマンドを使用することがあります。

### <a name="parameters"></a>パラメーター

|   | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | 空 | 該当なし |
| 応答 | 該当なし | MBIM_MS_ATR_INFO | 該当なし |

### <a name="query"></a>クエリ

クエリ メッセージの InformationBuffer が空です。 

### <a name="set"></a>設定

適用できません。

### <a name="response"></a>応答

MBIM_COMMAND_DONE InformationBuffer にはには、この関数に接続されている UICC をリセットするには、その答えを記述する次の MBIM_MS_ATR_INFO 構造体が含まれています。

#### <a name="mbimmsatrinfo"></a>MBIM_MS_ATR_INFO

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | AtrSize | SIZE(0..33) | 長さ**AtrData**します。 |
| 4 | 4 | AtrOffset | OFFSET | 呼ばれるバイト配列に、この構造体の先頭からのオフセット (バイト単位) が計算される**AtrData** ATR データを格納します。 |
| 8 | AtrSize | DataBuffer | DATABUFFER | **AtrData**バイト配列。 |

### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

次のステータス コードが適用されます。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_BUSY | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_FAILURE | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC が見つからないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | UICC がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_NOT_INITIALIZED | UICC はまだ完全に初期化されていないため、UICC 操作を実行できません。 |

## <a name="mbimcidmsuiccopenchannel"></a>MBIM_CID_MS_UICC_OPEN_CHANNEL

ホストでは、MBIM_CID_MS_UICC_OPEN_CHANNEL コマンドを使用して関数が UICC カード上の新しい論理チャネルを開くし、指定した UICC アプリケーション (アプリケーション ID で指定) を選択します。

関数は、一連の UICC コマンドを使用してこの MBIM コマンドを実装します。

1.  関数は、の 11.1.17」セクションの説明に従って、UICC に管理チャネル コマンドを送信、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)、新しい論理チャネルを作成します。 このコマンドが失敗した場合、関数は SW1 SW2 で MBIM_STATUS_MS_NO_LOGICAL_CHANNELS 状態を取得し、これ以上の操作を受け取りません。 
2.  管理チャネル コマンドが成功した場合、UICC は関数に新しい論理チャネルのチャネルの数を報告します。 関数は、[名前] で、SELECT を送信するコマンドの where P1 の 11.1.1」セクションの説明に従って、04 を =、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 この操作が失敗した場合、関数は論理チャネルを閉じる UICC 管理チャネル コマンドを送信し、選択を SW1 SW2 で MBIM_STATUS_MS_SELECT_FAILED 状態を返します。
3.  SELECT コマンドが成功すると、関数は、論理のチャンネル番号と今後の参照用の host で指定したチャネルのグループを記録します。 論理のチャンネル番号、SW1 SW2 からの選択、および応答の選択からに戻りますホスト。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_UICC_OPEN_CHANNEL | 該当なし | 該当なし |
| 応答 | MBIM_MS_UICC_OPEN_CHANNEL_INFO | 該当なし | 該当なし |

### <a name="query"></a>クエリ

適用できません。

### <a name="set"></a>設定

MBIM_COMMAND_MSG InformationBuffer にはには、次の MBIM_MS_SET_UICC_OPEN_CHANNEL 構造が含まれています。

#### <a name="mbimmssetuiccopenchannel"></a>MBIM_MS_SET_UICC_OPEN_CHANNEL

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | AppIdSize | SIZE(0..32) | アプリケーション ID (AppId) のサイズ。 |
| 4 | 4 | AppIdOffset | OFFSET | 呼ばれるバイト配列に、この構造体の先頭からのオフセット (バイト単位) が計算される**AppId**を選択するアプリケーション Id を定義します。 |
| 8 | 4 | SelectP2Arg | UINT32(0..255) | *P2* SELECT コマンドの引数。 |
| 12 | 4 | ChannelGroup | UINT32 | このチャネルのチャネルのグループを識別するタグの値。 |
| 16 | AppIdSize | DataBuffer | DATABUFFER | **AppId**バイト配列。 |

### <a name="response"></a>応答

MBIM_COMMAND_DONE InformationBuffer にはには、次の MBIM_MS_UICC_OPEN_CHANNEL_INFO 構造が含まれています。

#### <a name="mbimmsuiccopenchannelinfo"></a>MBIM_MS_UICC_OPEN_CHANNEL_INFO

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 状況 | BYTE[2] | SW1 と SW2、そのバイト順でします。 詳細については、次の次の表は、ノートを参照してください。 |
| 4 | 4 | Channel | UINT32(0..19) | 論理のチャネルの識別子です。 このメンバーが 0 の場合は、操作できませんでした。 |
| 8 | 4 | ResponseLength | SIZE(0..256) | 応答の長さ (バイト単位)。 |
| 12 | 4 | ResponseOffset | OFFSET | 呼ばれるバイト配列に、この構造体の先頭からのオフセット (バイト単位) が計算される**応答**SELECT からの応答を格納しています。 |
| 16 | - | DataBuffer | DATABUFFER | **応答**バイト配列のデータ。 |

コマンドは、MBIM_STATUS_MS_NO_LOGICAL_CHANNELS を返す場合、**状態**フィールドは単語を含む、UICC 状態 SW1 と SW2 管理チャネル コマンドから、その他のフィールドが 0 になります。 コマンドは、MBIM_STATUS_MS_SELECT_FAILED を返す場合、**状態**フィールドは単語を含む、UICC 状態 SW1 と SW2 SELECT コマンドから、その他のフィールドが 0 になります。 その他の状態、InformationBuffer を空にする必要があります。

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
| MBIM_STATUS_MS_NO_LOGICAL_CHANNELS | UICC で利用できる論理チャネルがないため、論理チャネルを開いているが失敗しました (それらがサポートしていないか、使用中のすべての状態に)。 |
| MBIM_STATUS_MS_SELECT_FAILED | 選択に失敗したため、論理のチャネルをオープンに失敗しました。 |

## <a name="mbimcidmsuiccclosechannel"></a>MBIM_CID_MS_UICC_CLOSE_CHANNEL

ホストは、論理、UICC でチャネルを閉じる関数に MBIM_CID_MS_UICC_CLOSE_CHANNEL を送信します。 ホストは、チャンネル番号を指定することがあります。 またはチャネルのグループを指定することがあります。

ホストは、チャンネル番号を指定する場合、関数が以前 MBIM_CID_MS_UICC_OPEN_CHANNEL によってこのチャネルが開かれたかどうかを確認する必要があります。 そうである場合は、管理チャネル コマンドをチャネルを閉じる、MBIM_STATUS_SUCCESS、ステータス、および管理チャネルから SW1 SW2 を返すに UICC に送信します。 そうでないことが操作は不要する場合 MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL エラー状態を返すとします。

ホストは、チャネルのグループを指定する場合、関数を決定しますが (あれば) 論理チャネルがそのチャネルのグループに開かれ、このような各チャネルに対して UICC 管理チャネル コマンドを送信します。 最後の管理チャネルの SW1 SW2 で MBIM_STATUS_SUCCESS の状態を返します。 解決されたチャネルがない場合は、90 を結果が返ります 00 です。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_UICC_CLOSE_CHANNEL | 該当なし | 該当なし |
| 応答 | MBIM_MS_UICC_CLOSE_CHANNEL_INFO | 該当なし | 該当なし |

### <a name="query"></a>クエリ

適用できません。

### <a name="set"></a>設定

MBIM_COMMAND_MSG InformationBuffer にはには、次の MBIM_MS_SET_UICC_CLOSE_CHANNEL 構造が含まれています。

#### <a name="mbimmssetuiccclosechannel"></a>MBIM_MS_SET_UICC_CLOSE_CHANNEL

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Channel | UINT32(0..19) | 0 以外の場合は、終了するチャネルを指定します。 ゼロの場合に、チャネルが関連付けられていることを指定します**ChannelGroup**終了します。 |
| 4 | 4 | ChannelGroup | UINT32 | 場合**チャネル**0 の場合は、タグの値をこのタグを持つすべてのチャネルが閉じられたを指定します。 場合**チャネル**が 0 以外の場合、このフィールドは無視されます。

### <a name="response"></a>応答

MBIM_COMMAND_DONE InformationBuffer にはには、次の MBIM_MS_UICC_CLOSE_CHANNEL_INFO 構造が含まれています。

#### <a name="mbimmsuiccclosechannelinfo"></a>MBIM_MS_UICC_CLOSE_CHANNEL_INFO

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 状況 | BYTE[2] | SW1 と最後にこのコマンドの代わりの関数によって実行される管理チャネルの SW2 します。 |

### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_BUSY | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_FAILURE | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC が見つからないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | UICC がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_NOT_INITIALIZED | UICC はまだ完全に初期化されていないため、UICC 操作を実行できません。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 論理のチャンネル番号が無効です (つまり、これで開かれませんでした MBIM_CID_MS_UICC_OPEN_CHANNEL)。 |

## <a name="mbimcidmsuiccapdu"></a>MBIM_CID_MS_UICC_APDU

ホストは、[apdu] コマンドを UICC で指定した論理チャネルに送信し、応答を受信する MBIM_CID_MS_UICC_APDU を使用します。 MBIM 関数は、論理チャネルが MBIM_CID_MS_UICC_OPEN_CHANNEL で以前に開かれたことを確認し、されていない場合、ステータス MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL で失敗する必要があります。

ホストでは、完全な [apdu] を関数に送信する必要があります。 [Apdu] のセクション 4 の最初の interindustry 定義で定義されているクラスのバイト値の送信、 [ISO/IEC 7816-4:2013 標準](https://go.microsoft.com/fwlink/p/?linkid=864596)、またはの 10.1.1 の拡張定義で、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 [Apdu] は、セキュリティで保護されたメッセージングせずに、またはセキュリティで保護されたメッセージングを使用した送信があります。 認証されていないコマンド ヘッダー。 ホストでは、クラス バイト、論理チャンネル番号、および、[apdu] およびセキュリティで保護されたメッセージの種類を指定します。

コマンドの最初のバイト」のセクション 4 で定義されているコード化されたクラスのバイトは、[apdu]、 [ISO/IEC 7816-標準 4:2013](https://go.microsoft.com/fwlink/p/?linkid=864596)またはセクションの 10.1.1、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。 ホストには、0 X、4 X、X 6、8 CX、X または EX クラス バイトを送信できます。 ただし、関数は、直接、UICC にこのバイトを渡しません。 代わりに、[apdu] を UICC に送信する前に、関数は、ホストから最初のバイトで置き換えますクラスの新しいバイト (」のセクション 4 で定義されているエンコードされた、 [ISO/IEC 7816-標準 4:2013](https://go.microsoft.com/fwlink/p/?linkid=864596)またはセクションの 10.1.1、 [ETSI TS102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594))、ホストで指定された型、チャネル、および SecureMessaging 値に基づいています。

| バイト クラス | 説明 |
| --- | --- |
| 0 X | 7816 4 interindustry、1 < = チャネル < = 3、該当する場合は、低ニブルでセキュリティをエンコードします |
| 4 X | 7816 4 interindustry、4 < チャネルを = < = 19、いいえ高セキュリティ メッセージング |
| 6 X | 7816 4 interindustry、4 < チャネルを = < = 19、セキュリティで保護された (ヘッダーは認証されていない) |
| 8 X | 102 221 拡張、1 < = チャネル < = 3、該当する場合は、低ニブルでセキュリティをエンコードします |
| CX | 102 221 拡張, 4 < チャネルを = < = 19、いいえ高セキュリティ メッセージング |
| EX | 102 221 拡張, 4 < チャネルを = < = 19、セキュリティで保護された (ヘッダーは認証されていない) |

関数を返す応答の状態、および SW1 SW2、UICC からホストにします。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_UICC_APDU | 該当なし | 該当なし |
| 応答 | MBIM_MS_UICC_APDU_INFO | 該当なし | 該当なし |

### <a name="query"></a>クエリ

適用できません。

### <a name="set"></a>設定

MBIM_COMMAND_MSG InformationBuffer にはには、次の MBIM_MS_SET_UICC_APDU 構造が含まれています。

#### <a name="mbimmssetuiccapdu"></a>MBIM_MS_SET_UICC_APDU

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Channel | UINT32(1..19) | [Apdu] が送信するチャネルを指定します。 |
| 4 | 4 | SecureMessaging | MBIM_MS_UICC_SECURE_MESSAGING | セキュリティで保護されたメッセージングを使用して、[apdu] が交換されるかどうかを指定します。 |
| 8 | 4 | 種類 | MBIM_MS_UICC_CLASS_BYTE_TYPE | クラス バイト定義の種類を指定します。 |
| 12 | 4 | CommandSize | UINT32(0..261) | **コマンド**長さ (バイト単位)。 |
| 16 | 4 | CommandOffset | OFFSET | 呼ばれるバイト配列に、この構造体の先頭からのオフセット (バイト単位) が計算される**コマンド**[apdu] を格納しています。 |
| 20 | - | DataBuffer | DATABUFFER | **コマンド**バイト配列。 |

MBIM_MS_SET_UICC_APDU 構造は、次の MBIM_MS_UICC_SECURE_MESSAGING と MBIM_MS_UICC_CLASS_BYTE_TYPE データ構造を使用します。

##### <a name="mbimmsuiccsecuremessaging"></a>MBIM_MS_UICC_SECURE_MESSAGING

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMMsUiccSecureMessagingNone | 0 | セキュリティで保護しないメッセージング。 |
| MBIMMsUiccSecureMessagingNoHdrAuth | 1 | セキュリティ保護されたメッセージング、認証されていないコマンド ヘッダー。 |

##### <a name="mbimmsuiccclassbytetype"></a>MBIM_MS_UICC_CLASS_BYTE_TYPE

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMMsUiccInterindustry | 0 | ISO 7816 4 での最初の interindustry 定義に従って定義されます。 |
| MBIMMsUiccExtended | 1 | ETSI 102 221 で拡張の定義に従って定義されます。 |

### <a name="response"></a>応答

MBIM_COMMAND_DONE InformationBuffer にはには、次の MBIM_MS_UICC_APDU_INFO 構造が含まれています。

#### <a name="mbimmsuiccapduinfo"></a>MBIM_MS_UICC_APDU_INFO

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 状況 | BYTE[2] | コマンドの結果として SW1 と SW2 のステータス単語。 |
| 4 | 4 | ResponseLength | サイズ | 応答の長さ (バイト単位)。 |
| 8 | 4 | ResponseOffset | OFFSET | 呼ばれるバイト配列に、この構造体の先頭からのオフセット (バイト単位) が計算される**応答**SELECT からの応答を格納しています。 |
| 12 | - | DataBuffer | DATABUFFER | **応答**バイト配列。 |

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
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 論理のチャンネル番号が無効です (つまり、これで開かれませんでした MBIM_CID_MS_UICC_OPEN_CHANNEL)。 |

関数では、[apdu] を UICC に送信することができます、SW1 SW2 状態の単語と、UICC (あれば) からの応答と共に MBIM_STATUS_SUCCESS が返されます。 ホストには、状態、UICC で、[apdu] コマンドが成功したかどうかを判断する (SW1 SW2) または失敗した理由を調べる必要があります。

## <a name="mbimcidmsuiccterminalcapability"></a>MBIM_CID_MS_UICC_TERMINAL_CAPABILITY

ホストは、ホストの機能について、モデムを通知するために MBIM_CID_MS_UICC_TERMINAL_CAPABILITY を送信します。 ターミナル機能 APDU、11.1.19 のセクションで指定された、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)、(サポートされている) 場合、最初のアプリケーションが選択される前に、カードに送信する必要があります。 そのため、ホストは、端末の機能 [apdu] に直接送信することはできませんは、モデムが永続的に格納されている 1 つまたは複数の端末の機能オブジェクトを含む MBIM_CID_MS_UICC_TERMINAL_CAPABILITY コマンドを送信します。 次のカードを挿入またはリセット、ATR 後で、モデムを選択、MF し端末の機能がサポートされているかどうか確認します。 そうである場合、モデムは MBIM_CID_MS_UICC_TERMINAL_CAPABILITY コマンドとそのモデムで生成された情報で指定された情報でターミナル機能 [apdu] を送信します。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_UICC_TERMINAL_CAPABILITY | 空 | 該当なし |
| 応答 | 該当なし | MBIM_MS_TERMINAL_CAPABILITY_INFO | 該当なし |

### <a name="query"></a>クエリ

InformationBuffer は null にして、InformationBufferLength を 0 にする必要があります。

### <a name="set"></a>設定

MBIM_COMMAND_MSG InformationBuffer にはには、次の MBIM_MS_SET_UICC_TERMINAL_CAPABILITY 構造が含まれています。

#### <a name="mbimmssetuiccterminalcapability"></a>MBIM_MS_SET_UICC_TERMINAL_CAPABILITY

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | elementCount | UINT32 | 端末の機能のオブジェクトの要素数。 |
| 4 | 8 * EC | CapabilityList OL_PAIR_LIST| 各端末の機能オブジェクト TLV のオフセットと長さのペア リストです。 |
| 4 + 8 * EC | - | DataBuffer | DATABUFFER | TLVs 端末の機能を実際のオブジェクトのバイト配列。 |

### <a name="response"></a>応答

応答は、モデムには、最後の送信端末の機能オブジェクトの正確な SET コマンドが含まれます。 そのため、MBIM_MS_TERMINAL_CAPABILITY_INFO は MBIM_MS_SET_UICC_TERMINAL_CAPABILITY と同じです。

#### <a name="mbimmsterminalcapabilityinfo"></a>MBIM_MS_TERMINAL_CAPABILITY_INFO

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | elementCount | UINT32 | 端末の機能のオブジェクトの要素数。 |
| 4 | 8 * EC | CapabilityList OL_PAIR_LIST| 各端末の機能オブジェクト TLV のオフセットと長さのペア リストです。 |
| 4 + 8 * EC | - | DataBuffer | DATABUFFER | TLVs 端末の機能を実際のオブジェクトのバイト配列。 |

### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_BUSY | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_FAILURE | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_SIM_NOT_INSERTED | UICC が見つからないため、UICC 操作を実行できません。 |
| MBIM_STATUS_BAD_SIM | UICC がエラー状態であるため、UICC 操作を実行できません。 |
| MBIM_STATUS_NOT_INITIALIZED | UICC はまだ完全に初期化されていないため、UICC 操作を実行できません。 |
| MBIM_STATUS_MS_INVALID_LOGICAL_CHANNEL | 論理のチャンネル番号が無効です (つまり、これで開かれませんでした MBIM_CID_MS_UICC_OPEN_CHANNEL)。 |

## <a name="mbimcidmsuiccreset"></a>MBIM_CID_MS_UICC_RESET

ホストは、MBIM 関数、UICC をリセットするか、関数のパススルー状態を照会する MBIM_CID_MS_UICC_RESET を送信します。

ホストは、関数が、UICC をリセットすることを要求するときにパススルーのアクションを指定します。

ホストが指定されている場合、 *MBIMMsUICCPassThroughEnable*パススルー アクション、関数は、UICC をリセットし、電源を投入する UICC には、UICC をホストと UICC (通信に使用するパススルー モードを使用した場合と同じ扱いいない場合でも、UICC Telecom UICC ファイル システム)。 関数は、任意の Apdu をカードに送信しませんしは、ホストと、UICC 間の通信にいつでも影響しません。

ホストが指定されている場合、 *MBIMMsUICCPassThroughDisable*パススルー操作、関数で、UICC をリセットし、UICC 電源投入時に、通常の電気通信 UICC として、UICC を処理され、UICC に存在している通信費 UICC ファイル システムが必要です.

関数で応答した場合に、ホストが、パススルーの状態を判断する関数をクエリした場合、 *MBIMMsUICCPassThroughEnabled*状態、そのパススルー モードが有効になっていることを意味します。 関数で応答した場合、 *MBIMMsUICCPassThroughDisabled*状態、パススルーそのモードが無効になっていることを意味します。

### <a name="parameters"></a>パラメーター

|   | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_UICC_RESET | 空 | 該当なし |
| 応答 | MBIM_MS_UICC_RESET_INFO | MBIM_MS_UICC_RESET_INFO | 該当なし |

### <a name="query"></a>クエリ

InformationBuffer を null にするものとし、 *InformationBufferLength* 0 にする必要があります。

### <a name="set"></a>設定

#### <a name="mbimsetmsuiccreset"></a>MBIM_SET_MS_UICC_RESET

MBIM_SET_MS_UICC_RESET 構造体には、ホストによって指定されたパススルー操作が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PassThroughAction | MBIM_MS_UICC_PASSTHROUGH_ACTION | 詳細については、次を参照してください。 [MBIM_MS_UICC_PASSTHROUGH_ACTION](#mbimmsuiccpassthroughaction)します。 |

#### <a name="mbimmsuiccpassthroughaction"></a>MBIM_MS_UICC_PASSTHROUGH_ACTION

MBIM_MS_UICC_PASSTHROUGH_ACTION 列挙体は、MBIM 関数にホストを指定できますパススルー操作の種類を定義します。

| 型 | Value |
| --- | --- |
| MBIMMsUiccPassThroughDisable | 0 |
| MBIMMsUiccPassThroughEnable | 1 |

### <a name="response"></a>応答

#### <a name="mbimmsuiccresetinfo"></a>MBIM_MS_UICC_RESET_INFO

MBIM_MS_UICC_RESET_INFO 構造体には、MBIM 関数のパススルー状態が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PassThroughStatus | MBIM_MS_UICC_PASSTHROUGH_STATUS | 詳細については、次を参照してください。 [MBIM_MS_UICC_PASSTHROUGH_STATUS](#mbimmsuiccpassthroughstatus)します。 |

#### <a name="mbimmsuiccpassthroughstatus"></a>MBIM_MS_UICC_PASSTHROUGH_STATUS

MBIM_MS_UICC_PASSTHROUGH_STATUS 列挙体は、ホストに MBIM 関数を指定します、パススルーの状態の種類を定義します。

| 型 | Value |
| --- | --- |
| MBIMMsUiccPassThroughDisabled | 0 |
| MBIMMsUiccPassThroughEnabled | 1 |

### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | すべてのコマンドで定義されている基本的な MBIM 状態です。 |
| MBIM_STATUS_BUSY | デバイスがビジーです。 |
| MBIM_STATUS_FAILURE | 操作に失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスは、この操作をサポートしていません。 |

### <a name="oidwwanuiccreset"></a>OID_WWAN_UICC_RESET

MBIM_CID_MS_UICC_RESET の NDIS 相当するものは[OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)します。 


