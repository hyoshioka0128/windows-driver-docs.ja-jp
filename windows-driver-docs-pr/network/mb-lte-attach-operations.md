---
title: MB LTE アタッチの操作
description: MB LTE アタッチの操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e11ca811b7caea3538fcc6391ab2afaf78fdc77f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549670"
---
# <a name="mb-lte-attach-operations"></a>MB LTE アタッチの操作

## <a name="lte-attach-apn-configuration-for-mbim-modems"></a>LTE は、MBIM モデムの構成を APN をアタッチします。

LTE のアタッチこれまでは、登録と Windows の一部が LTE に直接関係していない考慮されてプロシージャをアタッチします。 ただし、一般的な回線スイッチのネットワーク登録とは異なり LTE がパケットのスイッチのみのネットワークには、LTE ネットワークの登録を維持するためにデバイスを有効にする既定の EPS ベアラーが必要です。

ネットワーク デバイスと既定の EPS ベアラーを確立するには、必要があります要求中、LTE に PDP コンテキストのアクティブ化アタッチの手順で、アクセス ポイント名 (APN) の指定が必要です。 3 gpp は、標準的な単位は、デバイスが APN LTE としたときの接続を指定できます、4 つのシナリオがあります。

1.  デバイスでは、特定の LTE アタッチ APN を指定します。
2.  デバイスでは、特定の LTE APN をアタッチするが、ネットワークがローミング中には代わりに別の APN に接続するデバイスに決定を指定します。
3.  デバイスでは、LTE APN をアタッチし、ネットワーク、デバイスに 1 つのバックエンドを割り当てることができますを指定しません。
4.  LTE に G 2/3 G ネットワークから、デバイスが登録されているし、で最低限の 1 つのアクティブな PDP コンテキストが既にします。 ネットワークを使用、LTE APN を添付するとします。

すべての LTE が APN をアタッチする今日では、構成を持つプロバイダーごとに、モデムに直接情報を Ihv と Oem によって提供されます。 ただし、すべての可能な LTE が世界中のすべての演算子の APN の設定をアタッチするには、Ihv と Oem の完全にスケーラブルなモデルではありません。 Windows 10 バージョン 1703 以降の新しいインターフェイスが両方の NDIS Oid に対して定義されてし、MBIM Microsoft 独自の Cid LTE をサポートするためには、OS から構成を APN を添付します。 

Windows 10 以降、バージョン 1703 を基になるハードウェア サポート LTE、ユーザーが、LTE を構成できますに OS から APN 構成を添付する場合は、設定から、APN をアタッチします。 ハードウェア LTE を既定値を持つ接続 APN 構成する必要がありますもその構成が使用できるように、OS。

この機能は、新しい 2 つの Oid と Cid を追加してサポートされます。  MBIM を実装するための IHV パートナー、CID バージョンのみについては、サポートする必要があります。

## <a name="mb-interface-update-for-lte-attach-operations"></a>LTE MB インターフェイスの更新プログラムのアタッチの操作

最新 LTE、デバイスの状態をアタッチする LTE 接続 APN の構成と、OS を取得するを許可する 2 つの新しい MBIM Cid が作成されました。 IHV パートナーが OS 既定 LTE をサポートする場合は、両方のコマンドをサポートする必要がありますし、APN の管理をアタッチします。

サービス名 = **Basic 拡張機能の接続**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 値 = **3d01dcc5 fef5-4 d 05-0d3abef7058e9aaf**

| CID | コマンド コード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_MS_LTE_ATTACH_CONFIG | 3 | Windows 10 Version 1703 |
| MBIM_CID_MS_LTE_ATTACH_STATUS | 4 | Windows 10 Version 1703 |

## <a name="mbimcidmslteattachconfig"></a>MBIM_CID_MS_LTE_ATTACH_CONFIG

### <a name="description"></a>説明

LTE コンテキストをアタッチする、デバイスで実行時に、ネットワークの対話に応じて異なることができます。 このドキュメントの残りの部分、LTE 接続コンテキストが参照に LTE が使用されている現在の PDP コンテキストのアタッチし、LTE の既定の接続コンテキストが参照されます LTE を実行するデバイス上に構成されたとして使用して接続するその他の例が存在しない場合isting に PDP コンテキストが有効になります。  MBIM_CID_MS_LTE_ATTACH_CONFIG により、OS を照会して LTE の既定の設定は、挿入された SIM のプロバイダー (MCC/mnc もペア) のコンテキストをアタッチします。 

LTE アタッチ コンテキストとして APN でした技術的にと見なされますが、モデムに格納されている他のすべてのコンテキストとは異なります。 登録後の他のすべてのコンテキストのアクティブ化になることし、さまざまな条件に基づいて、OS を決定できますコンテキストは接続に最適です。 ただし、LTE、アタッチ、LTE ネットワーク上のデバイス登録の一部としてコンテキストが有効にします。 OS は登録の完了前に、ネットワーク関連の状態を取得できません。この制限により、OS が LTE を構成することがあります、デバイスを確認するデバイスのすべてのさまざまなローミング状態がどのようなローミングの状態に関係なく LTE ネットワークで登録できますのコンテキストをアタッチします。

LTE コンテキストのアタッチ、OS が、モデムは自己開始型のコンテキストのアクティブ化を認識していないために、ネットワークでのアクティブ化で OS 明示的な接続要求が必要ありません。 LTE を既定では、このカテゴリに分類をコンテキストをアタッチします。 OS PDP コンテキストを有効にする MBIM_CID_CONNECT 要求を発行すると、特定の PDP コンテキストが、次のすべてと一致する、モデムは、ネットワークと新しい無線ベアラー開かず CID のアクティブ化要求が成功を完了する必要があります。

1.  モデムが開始し、OS に使用できないする既存の有効な PDP コンテキストがあります。
2.  PDP コンテキストでは、CID 要求で指定した APN と一致します。
3.  有効な PDP コンテキストの IP の種類は、CID の要求の IP の種類と互換性が。

これは、OS がモデムが開始されたすべての PDP コンテキストを認識していないために重要です。 ネットワーク ノイズの軽減をロードします。 それ以外の場合、モデムが新しい無線ベアラー一致する OS APN 仕様に従って、通常のコンテキストのライセンス認証要求に起動する必要があります。 ここでは、IP の型の互換性を指定します。

| モデム内で有効になっている PDP コンテキストの IP の種類 | 要求された IP との互換性を種類します。 | 要求された IP の種類と互換性がありません。 |
| --- | --- | --- |
| IPv4 | 既定値です。IPv4;IPv4v6;IPv4 および v6 | IPv6 |
| IPv6 | 既定値です。IPv6 です。IPv4v6;IPv4 および v6 | IPv4 |
| IPv4v6 | 既定値です。IPv4;IPv6 です。IPv4v6;IPv4 および v6 | なし |

> [!NOTE]
> 無線で IP の種類のいずれかが有効になっている場合のみ、モデムのことは 2 つ目の PDP コンテキストをありません必要があります。 例では、IPv4 が有効になっていると、ホストの IPv4 および IPv6 を要求し、モデムは、IPv6 のベアラーを開かず、アクティブ化要求を完了する必要があります。

OS が非アクティブ化する MBIM_CID_CONNECT 要求を発行すると PDP コンテキスト、そのモデムは、以下を確認する必要があります。

1.  デバイスが接続されている LTE かどうかと、非アクティブになるコンテキストは、唯一 LTE 登録を維持するために PDP コンテキストを有効になっています。
2.  OS に公開されているかどうか非アクティブ化するコンテキストもモデムが内部的に使用されますがサービスの

これらのいずれかに該当する場合、モデムする必要があります CID の非アクティブ化要求を完了が、ネットワークと無線ベアラーを維持し続けます。 それ以外の場合、モデムには、通常の非アクティブ化要求に従ってコンテキストが非アクティブ化する必要があります。

LTE 接続 APN 構成が、OS によって提供されるすべての既定のプロバイダーであり、挿入された SIM カードのホーム プロバイダーの ID (MCC/mnc もペア) に一致します。 モデムは構成されている LTE のみを提供する必要があります、現在の挿入 SIM のプロバイダー ID の照会されたときにコンテキストをアタッチします。 常に 3 つの既定 LTE、ローミングの条件 (ホーム/パートナー/パートナー以外) ごとに 1 つ挿入した SIM のプロバイダー ID と一致するコンテキストをアタッチするモデムを返します。

ある SIM のスワップの間でモデムをクリアする既定のことが予想されます LTE は、[次へ] の SIM カードの構成を適用する前にコンテキストをアタッチします。 新しく挿入された SIM カードが LTE を既定値を持たない場合、デバイスは空の文字列を NULL、LTE の APN を有効になっているコンテキストを維持しながらのローミングのすべての条件のコンテキストのアタッチを返す必要があります、コンテキストの構成を接続します。 コンテキストが無効になっている場合、デバイス LTE 接続、使用可能な構成がないため LTE にアタッチできませんが想定されます。 モデムが、工場出荷時の既定を復元する必要があります、ユーザーは、デバイス上に構成した SIM カードに交換、ときに LTE SIM カードの構成をアタッチします。 SIM のスワップの間で保持する実行時構成は必要ありません。 いつでもでも必要がありますのみがある 1 つの既定 LTE が 1 つの条件 (ホーム/パートナー/パートナー以外) の移動、モデムの APN をアタッチします。  

OS は常にすべて設定 3 つの既定 LTE アタッチ コンテキスト Set コマンドが発行されると、ローミング条件ごとに 1 つ。 OS によって提供される一覧があるちょうど 3 Set コマンドを拒否する必要があります。 コンテキストにアタッチ LTE 指定された既定のいずれかの場合は、一致する現在の登録状態し、モデムする必要があります、ネットワークから切断されて LTE を再実行は、新しく指定した LTE でアタッチ ローミングの条件がコンテキストをアタッチする OS によって構成されます。 それ以外の場合、LTE 接続コンテキスト、次回のローミングの条件が一致する場合、指定された既定を使用するデバイスが必要です。  デバイスが指定した既定 LTE アタッチし、LTE のネットワーク上のレジスタにコンテキストが失敗し、デバイスはフォールバックとして適切なし 3 G/2 G にします。 パートナーと非パートナー ネットワーク、モデムでモデムは区別できないときに既定値の使用非パートナー LTE はすべてのローミングのシナリオのコンテキストをアタッチする必要があります。 OS、LTE 既定を構成した場合は、IP の種類とコンテキストをアタッチ = 既定では、モデムが LTE 接続コンテキストは、最も適切な IP の種類を割り当てることが想定されます。  ただし、OS には、ローミングの条件をパートナーし、LTE の IP の種類の構成を正確に反映するコンテキストをアタッチするには返される場合も、モデムが必要です。

Ihv と Oem が事前に構成できますが、LTE、モデムの既定の設定としてコンテキストをアタッチする、これらのコンテキストは MBIM_MS_CONTEXT_SOURCE としてタグ付けする必要があります MbimMsContextSourceModemProvisioned を =。  

ごと、3 gpp、標準的な LTE アタッチ既定コンテキストは、2 つのカテゴリに分割できます。UE 開始され、ネットワークが開始されます。 NULL 空のアクセスの文字列で、デバイスを構成する場合は、LTE がネットワークにコンテキストをアタッチし、1 つのバックアップをデバイスに割り当てるネットワーク待機を提供していないデバイスが必要です。 コンテキストの IP の種類を既定として構成されている場合は、LTE アタッチし、モデムの内部アルゴリズムに基づいて最適な IP の種類を選択する必要があります、MBIM 1.0 で規定されているだけです。

次の図は、例を示しています。 LTE のフローは、構成をアタッチします。

![LTE 構成の例のフローをアタッチする](images/LTE_attach_1.png "LTE アタッチ構成フローの例")

#### <a name="query"></a>クエリ

MBIM_MS_LTE_ATTACH_CONFIG_INFO、InformationBuffer で完了したクエリと一連のメッセージが返されます。 クエリの場合は、InformationBuffer は NULL です。

#### <a name="set"></a>設定

セットに対して、InformationBuffer には、MBIM_MS_SET_LTE_ATTACH_CONFIG が含まれています。

#### <a name="unsolicited-events"></a>要請されていないイベント

イベント InformationBuffer には MBIM_MS_LTE_ATTACH_CONFIG_INFO 構造体が含まれています。 場合によっては、既定の LTE 接続コンテキストはネットワークによって、Over-The-Air (OTA) を更新またはでショート メッセージ サービス (SMS) を MBIM_CID_MS_LTE_ATTACH_CONFIG を経由しませんが、OS からコマンドします。 関数は、既定値を更新する必要があります LTE がコンテキストにアタッチし、MBIM_MS_CONTEXT_SOURCE のタグを付ける MbimMsContextSourceOperatorProvisioned を適宜 =。 その後、関数が更新された一覧で、このイベントを使用する更新プログラムについて、ホストに通知する必要があります。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_MS_LTE_ATTACH_CONFIG | 該当なし | 該当なし |
| 応答 | MBIM_MS_LTE_ATTACH_CONFIG_INFO | MBIM_MS_LTE_ATTACH_CONFIG_INFO | MBIM_MS_LTE_ATTACH_CONFIG_INFO |

### <a name="data-structures"></a>データ構造体

#### <a name="query"></a>クエリ 

InformationBuffer は NULL にするものとし、InformationBufferLength を 0 にする必要があります。

#### <a name="set"></a>設定

次の MBIM_MS_SET_LTE_ATTACH_CONFIG 構造、InformationBuffer で使用されます。 Set コマンドでは、有効なは、一覧には、3 ローミング条件 (ホーム/パートナー/パートナー以外) ごとに 1 つの要素数が含まれている場合のみ。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 操作 | MBIM_MS_LTE_CONTEXT_OPERATIONS | Set コマンドを使用する対象の操作の種類を指定します。 場合 MbimMsLteAttachContextOperationRestoreFactory に設定するその他のすべてのフィールドを無視する必要があります。 LTE アタッチ既定の OS が作成または変更されたコンテキストを削除する必要があり、既定のファクトリの事前構成済み既定 LTE 接続コンテキストを読み込む必要があります。 モデムは持っていない場合、既定の構成、し、すべての条件は、ローミング LTE 添付 APN の空の文字列と IP の種類にコンテキストを設定する必要があります = 既定値。 |
| 4 | 4 | ElementCount (EC) | UINT32 | 後に、DataBuffer にカウントの MBIM_MS_LTE_ATTACH_CONTEXT 構造体。 このコンポーネントは現在、3 ローミング条件 (ホーム/パートナー/パートナー以外) ごとに 1 つに指定します。 |
| 8 | 8 * EC | MsLteAttachContextRefList | OL_PAIR_LIST | ペアの最初の要素は、4 バイト オフセット MBIM_MS_LTE_ATTACH_CONTEXT 構造体をこの MBIM_MS_LTE_ATTACH_CONFIG_INFO 構造体の先頭 (オフセット 0) から計算されます (詳細については、MBIM_MS_LTE_ATTACH_CONTEXT テーブルを参照してください)。 ペアの 2 番目の要素は、対応する MBIM_MS_LTE_ATTACH_CONTEXT 構造へのポインターのサイズが 4 バイトです。 |
| 8 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_LTE_ATTACH_CONTEXT 構造体の配列。 |

上記の表に、次の構造が使用されます。

MBIM_MS_LTE_ATTACH_CONTEXT_OPERATIONS では、Set コマンドで使用できる操作の種類について説明します。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MbimMsLteAttachContextOperationDefault | 0 | 既存のデフォルト LTE を上書きするための既定の操作では、モデムのコンテキストをアタッチします。 OS は 3 つすべての既定を常に置き換える LTE が条件をローミングのコンテキストをアタッチします。 |
| MbimMsLteAttachContextOperationRestoreFactory | 1 | LTE のコンテキストからのプロバイダー id の現在アタッチ ファクトリ事前構成済み既定値に戻すには、SIM が挿入されます。 LTE 接続コンテキストを交換またはオペレーティング システムによって作成されたすべての既定値は削除されを交換する必要があります。 LTE アタッチの事前構成済みの既定の既定値がない場合に、現在のコンテキストが 1 つ以上のローミング条件と共に SIM プロバイダー ID を挿入し、LTE アタッチ既定値は、APN の空の文字列と IP の種類を返す必要があります = 既定値。 |

MBIM_MS_LTE_ATTACH_CONTEXT LTE に使用するコンテキストを指定する構成をアタッチします。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | IPType | MBIM_CONTEXT_IP_TYPE | 詳細については、MBIM_CONTEXT_IP_TYPE テーブルを参照してください。 |
| 4 | 4 | Roaming | MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL | この既定値に適用される移動条件を示します LTE がコンテキストをアタッチします。 詳細については、MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL テーブルを参照してください。 |
| 8 | 4 | Source | MBIM_MS_CONTEXT_SOURCE | コンテキストの作成のソースを指定します。 詳細については、MBIM_MS_CONTEXT_SOURCE テーブルを参照してください。 |
| 12 | 4 | AccessStringOffset | オフセット | 文字列、AccessString、ネットワークにアクセスするデータ バッファーのオフセットします。 GSM ベースのネットワークでは、"data.thephone company.com"など、アクセス ポイント名 (APN) 文字列になります。 文字列のサイズは 100 文字を超えない必要があります。 AccessString が空の場合、デバイスで、ネットワーク アクセスの文字列をデバイスに割り当てるには。 ここで指定するのにはまだ IP の種類があります。 |
| 16 | 4 | AccessStringSize | SIZE(0..200) | AccessString に使用するサイズ。 デバイスが LTE の元のデバイスにアクセス文字列を割り当てるネットワークが必要な場合、この値は 0 にはアタッチします。 |
| 20 | 4 | UserNameOffset | オフセット | 計算される、この構造体の先頭から、ユーザー名、認証するユーザー名を表す文字列へのバイト オフセットします。 このメンバーは、NULL を指定できます。 |
| 24 | 4 | UserNameSize | SIZE(0..510) | ユーザー名に使用するサイズ。 |
| 28 | 4 | PasswordOffset | オフセット | ユーザー名のパスワードを表すオフセット (バイト)、文字列、パスワードに、この構造体の先頭から計算されます。 このメンバーは、NULL を指定できます。 |
| 32 | 4 | PasswordSize | SIZE(0..510) | パスワードを使用するサイズ。 |
| 36 | 4 | 圧縮 | MBIM_COMPRESSION | ヘッダーとデータのデータ接続に使用する圧縮形式を指定します。 このメンバーは、GSM ベースのデバイスにのみ適用されます。 ホストは、CDMA ベースのデバイス、MBIMCompressionNone にこのメンバーを設定します。 詳細については、MBIM_COMPRESSION テーブルを参照してください。 |
| 40 | 4 | AuthProtocol | MBIM_AUTH_PROTOCOL | PDP ライセンス認証を使用する認証の種類。 詳細については、MBIM_AUTH_PROTOCOL テーブルを参照してください。 |
| 44 |  | DataBuffer | DATABUFFER | AccessString、UserName、およびパスワードを格納しているデータ バッファー。 |

MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL では、この既定の設定が適用されるどのローミングの条件を示します LTE がコンテキストをアタッチします。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MbimMsLteAttachContextRoamingControlHome | 0 | 既定 LTE アタッチするかどうかを示すコンテキストがホーム ネットワーク上で使用するかを許可します。 |
| MbimMsLteAttachContextRoamingControlPartner | 1 | コンテキストがない、またはパートナーのローミング ネットワークで使用できるかどうかを示します。 |
| MbimMsLteAttachContextRoamingControlNonPartner | 2 | コンテキストがない、または非パートナー ローミング ネットワークで使用できるかどうかを示します。 |

MBIM_MS_CONTEXT_SOURCE では、コンテキストの作成のソースを指定します。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MbimMsContextSourceAdmin | 0 | コンテキストは、OS から企業の IT 管理者によって作成されました。 |
| MbimMsContextSourceUser | 1 | コンテキストは、OS の設定を使用してユーザーによって作成されました。 |
| MbimMsContextSourceOperator | 2 | コンテキストは、OMA-DM またはその他のチャネルを通じて演算子によって作成されました。 | 
| MbimMsContextSourceModem | 3 | コンテキストは、IHV および OEM によって作成されました。 |
| MbimMsContextSourceDevice | 4 | コンテキストは、OS の APN データベースによって作成されました。 |

#### <a name="response"></a>応答

次の MBIM_MS_LTE_ATTACH_CONFIG_INFO 構造、InformationBuffer で使用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | 後に、DataBuffer にカウントの MBIM_MS_LTE_ATTACH_CONTEXT 構造体。 このコンポーネントは現在、3 ローミング条件 (ホーム/パートナー/パートナー以外) ごとに 1 つに指定します。 |
| 4 | 8 * EC | MsLteAttachContextRefList | OL_PAIR_LIST | ペアの最初の要素は、4 バイト オフセット MBIM_MS_LTE_ATTACH_CONTEXT 構造体をこの MBIM_MS_LTE_ATTACH_CONFIG_INFO 構造体の先頭 (オフセット 0) から計算されます (詳細については、MBIM_MS_LTE_ATTACH_CONTEXT テーブルを参照してください)。 ペアの 2 番目の要素は、対応する MBIM_MS_LTE_ATTACH_CONTEXT 構造へのポインターのサイズが 4 バイトです。 |
| 4 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_LTE_ATTACH_CONTEXT 構造体の配列。 |

#### <a name="notification"></a>通知

詳細については、MBIM_MS_LTE_ATTACH_CONFIG_INFO テーブルを参照してください。

### <a name="status-codes"></a>状態コード

クエリおよびセットの操作。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | デバイスがプロビジョニングされているコンテキストを取得できなかったため、操作が失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスは、操作をサポートしていないため、操作が失敗しました。 |

セット操作の場合のみ。 

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーターのため、操作が失敗しました。 |
| MBIM_STATUS_WRITE_FAILURE  | 更新の要求が成功した操作が失敗しました。 |

## <a name="mbimcidmslteattachstatus"></a>MBIM_CID_MS_LTE_ATTACH_STATUS

### <a name="description"></a>説明

3 gpp の要件によっては、デバイスが LTE LTE ことがなく、ネットワークへのアタッチに PDP コンテキストが有効になっているときに使用されるコンテキストをアタッチする既定値を指定できますが状況もあります。 デバイスはどこ LTE アタッチ LTE 既定とは異なる PDP コンテキストデバイスで構成されているコンテキストにアタッチします。 すべての可能なシナリオの一覧を次には。

1.  UE は、特定の LTE アタッチ APN を指定します。
2.  UE は、特定の LTE APN をアタッチするが、ネットワークがローミング中には代わりに別の APN に接続するデバイスに決定を指定します。
3.  LTE、APN にアタッチでき、いずれかのネットワークの割り当てをデバイスには、UE は指定しません。
4.  LTE に G 2/3 G ネットワークから、UE が登録されているし、で最低限の 1 つのアクティブな PDP コンテキストが既にします。 ネットワークを使用、LTE APN を添付するとします。

LTE デバイスの既定値がアタッチするときに、os、LTE 最新添付ファイルの PDP コンテキストの詳細を提供 MBIM_CID_MS_LTE_ATTACH_STATUS の通知を送信します。 既定 LTE アタッチとき、次のシナリオのいずれかが満たされたときに発生します。

1.  デバイスは、最初に LTE ネットワークにアタッチします。
2.  デバイスの手を G 2/3 G LTE をすべて事前に PDP コンテキストが有効になります。

返されたコンテキストをアタッチ、LTE MBIM_CID_LTE_ATTACH_STATUS は、次のいずれかになります。

1.  LTE を既定では、モデムに格納されているコンテキストをアタッチします。
2.  LTE を既定では、ネットワークから割り当てられたコンテキストをアタッチします。

実行時に、OS もことができるよう、最後の使用をクエリ アタッチ LTE アタッチ既定の情報はでした。 最後に返される、モデムが期待どおり LTE 既知の既定のコンテキストをアタッチします。  デバイスは、2 G/3 G ネットワークに、オフ、LTE から渡された、以前の LTE に使用されたコンテキストを返します、モデムの期待されますをアタッチします。 ネットワークから、デバイスの登録を解除するたびに、APN を空になるが期待されます。

以下の図 LTE アタッチ状態用にメッセージ フローの例を示します。

![LTE 状態フローの例のアタッチ](images/LTE_attach_2.png "LTE アタッチ状態フローの例")

#### <a name="query"></a>クエリ

MBIM_MS_LTE_ATTACH_STATUS、InformationBuffer でクエリの完全なメッセージが返されます。 クエリの場合は、InformationBuffer は NULL です。

#### <a name="set"></a>設定 

セット操作はサポートされていません。

#### <a name="unsolicited-events"></a>要請されていないイベント

イベント InformationBuffer には MBIM_MS_LTE_ATTACH_STATUS 構造体が含まれています。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | 該当なし | 該当なし |
| 応答 | 該当なし | MBIM_MS_LTE_ATTACH_STATUS | MBIM_MS_LTE_ATTACH_STATUS |

### <a name="data-structures"></a>データ構造体

#### <a name="query"></a>クエリ

InformationBuffer は NULL にするものとし、InformationBufferLength を 0 にする必要があります。

#### <a name="set"></a>設定

セット操作はサポートされていません。

#### <a name="response"></a>応答

次の MBIM_MS_LTE_ATTACH_STATUS 構造、InformationBuffer で使用されます。


| Offset | サイズ |       フィールド        |           種類           |                                                                                                                                                                                                                                                                                                    説明                                                                                                                                                                                                                                                                                                     |
|--------|------|--------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |   LteAttachState   | MBIM_MS_LTE_ATTACH_STATE |                                                                                                                                                                                                                                    かどうか、デバイスが現在 LTE ネットワークに接続するかどうかを示します。  詳細については、MBIM_MS_LTE_ATTACH_STATE テーブルを参照してください。                                                                                                                                                                                                                                     |
|   4    |  4   |       IPType       |  MBIM_CONTEXT_IP_TYPES   |                                                                                                                                                                                                                                                                             詳細については、MBIM_CONTEXT_IP_TYPE テーブルを参照してください。                                                                                                                                                                                                                                                                              |
|   8    |  4   | AccessStringOffset |          オフセット          | 文字列、AccessString、ネットワークにアクセスするデータ バッファーのオフセットします。 GSM ベースのネットワークでは、"data.thephone company.com"など、アクセス ポイント名 (APN) 文字列になります。 CDMA ベースのネットワークでは、これがあります「#777」またはネットワーク アクセスの識別子 (NAI) などの特殊なダイヤル コードなど"foo@thephone-company.com"。 このメンバーは、APN の既定のネットワークを割り当てることを要求する NULL を指定できます。 注:すべてのネットワークでは、この NULL APN 規則をサポートします。 したがって、無効な APN によって発生した接続エラーは、考えられる結果です。 文字列のサイズは 100 文字を超えない必要があります。 |
|   12   |  4   |  AccessStringSize  |       SIZE(0..200)       |                                                                                                                                                                                                                                                                                        AccessString のサイズをバイト単位のサイズ。                                                                                                                                                                                                                                                                                        |
|   16   |  4   |   UserNameOffset   |          オフセット          |                                                                                                                                                                                                                          計算される、この構造体の先頭から、ユーザー名、認証するユーザー名を表す文字列へのバイト オフセットします。 このメンバーは、NULL を指定できます。                                                                                                                                                                                                                           |
|   20   |  4   |    UserNameSize    |       SIZE(0..510)       |                                                                                                                                                                                                                                                                                          サイズ (バイト) のユーザー名に使用します。                                                                                                                                                                                                                                                                                          |
|   24   |  4   |   PasswordOffset   |          オフセット          |                                                                                                                                                                                                                             ユーザー名のパスワードを表すオフセット (バイト)、文字列、パスワードに、この構造体の先頭から計算されます。 このメンバーは、NULL を指定できます。                                                                                                                                                                                                                             |
|   28   |  4   |    PasswordSize    |       SIZE(0..510)       |                                                                                                                                                                                                                                                                                          サイズ (バイト) のパスワードを使用します。                                                                                                                                                                                                                                                                                          |
|   32   |  4   |    圧縮     |     MBIM_COMPRESSION     |                                                                                                                                                                           ヘッダーとデータのデータ接続に使用する圧縮形式を指定します。 このメンバーは、GSM ベースのデバイスにのみ適用されます。 ホストは、CDMA ベースのデバイス、MBIMCompressionNone にこのメンバーを設定します。 詳細については、MBIM_COMPRESSION テーブルを参照してください。                                                                                                                                                                           |
|   36   |  4   |    AuthProtocol    |    MBIM_AUTH_PROTOCOL    |                                                                                                                                                                                                                                                     PDP ライセンス認証を使用する認証の種類。 詳細については、MBIM_AUTH_PROTOCOL テーブルを参照してください。                                                                                                                                                                                                                                                     |
|   40   |  4   |                    |        DataBuffer        |                                                                                                                                                                                                                                                                                                     DATABUFFER                                                                                                                                                                                                                                                                                                     |

上記の表に、次のデータ構造が使用されます。

MBIM_MS_LTE_ATTACH_STATE では、かどうか、デバイスが現在 LTE ネットワークに接続するかどうかを示します。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MbimMsLteAttachStateDetached | 0 | デバイスが LTE ネットワークに接続されていないことを示します。 |
| MbimMsLteAttachStateAttached | 1 | デバイスが LTE ネットワークに接続されていることを示します。 |

#### <a name="notification"></a>通知

詳細については、MBIM_MS_LTE_ATTACH_STATUS テーブルを参照してください。

### <a name="status-codes"></a>状態コード

クエリおよびセットの操作。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | デバイスがプロビジョニングされているコンテキストを取得できなかったため、操作が失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスは、操作をサポートしていないため、操作が失敗しました。 |
