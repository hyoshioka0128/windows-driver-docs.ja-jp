---
title: MB LTE アタッチ操作
description: MB LTE アタッチ操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9e9ba5bb5be2b8d92571aefd3cab9e4d8c1584e
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557801"
---
# <a name="mb-lte-attach-operations"></a>MB LTE アタッチ操作

## <a name="lte-attach-apn-configuration-for-mbim-modems"></a>MBIM モデム用の LTE 接続 APN 構成

従来、LTE attach は登録の一部と見なされており、Windows は、直接の LTE アタッチ手順には含まれていませんでした。 ただし、一般的な回線スイッチのネットワーク登録とは異なり、LTE はパケットのスイッチ専用ネットワークであり、デバイスが LTE ネットワークで登録を維持するためには、既定の EPS ベアラーが有効になっている必要があります。

ネットワークで既定の EPS ベアラーを確立するには、デバイスは、アクセスポイント名 (APN) の仕様を必要とする LTE アタッチ手順で PDP コンテキストのアクティブ化を要求する必要があります。 3GPP 標準では、デバイスが LTE 接続を試行するときに APN を指定できるシナリオが4つあります。

1.  デバイスは、特定の LTE 接続 APN を指定します。
2.  デバイスは特定の LTE 接続 APN を指定しますが、ネットワークでは、ローミング時に別の APN にデバイスをアタッチすることを決定します。
3.  デバイスでは、LTE 接続 APN が指定されていないため、ネットワークがデバイスに再び割り当てられるようにします。
4.  デバイスが 2G/3G ネットワークから LTE に登録されており、少なくとも1つのアクティブな PDP コンテキストが既に存在しています。 ネットワークでは、これを LTE 接続 APN として使用します。

現在、すべての LTE 接続 APN 情報は、構成を持つ各プロバイダーのモデムに直接、Ihv および Oem によって提供されています。 ただし、このモデルは、Ihv および Oem が全オペレーターに対して可能なすべての LTE attach APN 設定を全世界で使用できるようにするための完全にスケーラブルなモデルではありません。 Windows 10 バージョン1703以降では、OS からの LTE attach APN 構成をサポートするために、NDIS Oid と MBIM Microsoft 専有 Cid の両方に新しいインターフェイスが定義されています。 

Windows 10 バージョン1703以降では、基になるハードウェアで OS からの LTE attach APN 構成がサポートされている場合、ユーザーは設定から LTE attach APN を構成できます。 既定の LTE 接続 APN 構成を持つハードウェアも、OS で構成を利用できるようにする必要があります。

この機能は、2つの新しい Oid と Cid にを追加することによってサポートされています。  MBIM を実装する IHV パートナーの場合は、CID バージョンのみがサポートされている必要があります。

## <a name="mb-interface-update-for-lte-attach-operations"></a>LTE アタッチ操作用の MB インターフェイス更新プログラム

LTE attach APN の構成を許可する2つの新しい MBIM Cid が作成され、OS はデバイスの最新の LTE 接続状態を取得できるようになりました。 IHV パートナーが OS の既定の LTE 接続 APN 管理をサポートすることを決定した場合、両方のコマンドがサポートされている必要があります。

サービス名 =**基本接続拡張機能**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 値 = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

| CID | コマンド コード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_MS_LTE_ATTACH_CONFIG | 3 | Windows 10 Version 1703 |
| MBIM_CID_MS_LTE_ATTACH_STATUS | 4 | Windows 10 Version 1703 |

## <a name="mbim_cid_ms_lte_attach_config"></a>MBIM_CID_MS_LTE_ATTACH_CONFIG

### <a name="description"></a>説明

LTE アタッチコンテキストは、ネットワークが実行時にデバイスとどのように対話するかによって異なる場合があります。 このドキュメントの残りの部分では、lte アタッチコンテキストは、LTE attach に使用されている現在の PDP コンテキストと呼ばれます。既定の LTE アタッチコンテキストは、他の既存の有効な PDP コンテキストがない場合に、LTE attach を実行するデバイスで構成されているものと呼ばれます。  MBIM_CID_MS_LTE_ATTACH_CONFIG により、OS は、挿入された SIM のプロバイダー (MCC/MNC ペア) の既定の LTE アタッチコンテキストを照会して設定できます。 

LTE 接続 APN は技術的にはコンテキストと見なすことができますが、モデムに格納されている他のすべてのコンテキストとは異なります。 他のすべてのコンテキストのアクティブ化は、登録後に行われ、さまざまな条件に基づき、接続に最適なコンテキストを OS が判断できます。 ただし、lte ネットワークでのデバイス登録の一環として、LTE アタッチコンテキストが有効になっています。 OS は、登録を完了する前にネットワーク関連の状態を取得できません。この制限のため、OS はデバイスのすべてのローミング条件に対して LTE アタッチコンテキストを構成し、ローミングステータスに関係なくデバイスを LTE ネットワークに登録できるようにする必要があります。

ネットワークを使用した LTE アタッチコンテキストのアクティブ化では、すべてのモデムのセルフ開始コンテキストライセンス認証が認識されないため、OS が明示的に接続要求を行う必要はありません。 既定の LTE アタッチコンテキストは、このカテゴリに分類されます。 OS が PDP コンテキストを有効にするために MBIM_CID_CONNECT 要求を発行し、指定された PDP コンテキストが次のすべてに一致した場合、モデムは CID アクティブ化要求を完了する必要があります。その際、ネットワークを使用して新しい無線ベアラーを起動する必要はありません。

1.  モデムによって開始され、OS で使用できない、有効な PDP コンテキストが既に存在します。
2.  PDP コンテキストは、CID 要求内の指定された APN と一致します。
3.  有効な PDP コンテキストの IP の種類は、CID 内の要求された IP の種類と互換性があります。

これは、OS がモデムによって開始されたすべての PDP コンテキストを認識しないため、重要です。 これにより、ネットワークのノイズと負荷が軽減されます。 そうしないと、通常のコンテキストアクティブ化要求に従って、モデムは、新しい無線ベアラー準拠 OS APN 仕様を表示する必要があります。 ここでは、IP 型の互換性について説明します。

| モデム内の有効な PDP コンテキストの IP の種類 | 要求された IP の種類と互換性があります | 要求された IP の種類と互換性がありません |
| --- | --- | --- |
| IPv4 | 標準Ipv4/ipv6IPv4v6;IPv4 と v6 | IPv6 |
| IPv6 | 標準IPv6IPv4v6;IPv4 と v6 | IPv4 |
| IPv4v6 | 標準Ipv4/ipv6IPv6IPv4v6;IPv4 と v6 | None |

> [!NOTE]
> 1つの IP の種類のみが無線で有効になっている場合、モデムは2つ目の PDP コンテキストを表示しないようにする必要があります。 たとえば、IPv4 が有効になっていて、ホストが IPv4 と IPv6 を要求した場合、モデムは IPv6 ベアラーを起動せずにライセンス認証要求を完了する必要があります。

OS が PDP コンテキストを非アクティブ化するために MBIM_CID_CONNECT 要求を発行すると、モデムは次の点を確認する必要があります。

1.  デバイスが LTE に接続されていて、非アクティブ化されるコンテキストが、LTE 登録を維持するために有効な唯一の PDP コンテキストであるかどうか
2.  OS に公開されていないすべてのサービスに対して、非アクティブ化されるコンテキストが内部的にモデムによっても使用されているかどうか

これらのいずれかが true の場合、モデムは CID 非アクティブ化要求を完了する必要がありますが、ネットワークを使用して無線ベアラーを維持し続けます。 そうしないと、通常の非アクティブ化要求に応じて、モデムはコンテキストを非アクティブ化する必要があります。

OS によって提供されるすべての既定の LTE 接続 APN 構成はプロバイダー単位であり、挿入された SIM カードのホームプロバイダー ID (MCC/MNC ペア) と一致します。 モデムは、照会時に現在挿入されている SIM のプロバイダー ID に対して、構成された LTE アタッチコンテキストのみを提供する必要があります。 モデムは、挿入された SIM のプロバイダー ID と一致する既定の3つの既定の LTE アタッチコンテキストを常に返す必要があります (各ローミング条件 (ホーム/パートナー/非パートナー)。

SIM をスワップすると、次の SIM カードの構成を適用する前に、モデムが既定の LTE アタッチコンテキストをクリアする必要があることが予想されます。 新しく挿入された SIM カードに既定の LTE アタッチコンテキスト構成がない場合、デバイスは、コンテキストを有効にしたまま、すべてのローミング条件に対して、LTE アタッチコンテキストの APN に対して NULL の空の文字列を返す必要があります。 コンテキストが無効になっている場合は、デバイスが LTE にアタッチされないことが想定されています。これは、LTE アタッチに使用できる構成がないためです。 デバイスで事前に構成された SIM カードにユーザーがスワップバックすると、モデムは、SIM カードの工場出荷時の既定の LTE アタッチ構成を復元する必要があります。 実行時の構成は、SIM スワップ間で保持されることは想定されていません。 常に、ローミング条件 (ホーム/パートナー/非パートナー) ごとに、モデムに既定の LTE アタッチ APN が1つだけ存在する必要があります。  

OS は、Set コマンドの発行時に、各ローミング条件に1つずつ、3つの既定の LTE アタッチコンテキストすべてを常に設定します。 OS によって提供されるリストが正確に3つもない場合は、Set コマンドを拒否する必要があります。 指定された既定の LTE アタッチコンテキストのいずれかが、ローミング条件が現在の登録ステータスと一致する OS によって構成されている場合、モデムはネットワークから切断し、新しく指定された LTE アタッチコンテキストで LTE アタッチを再実行する必要があります。 それ以外の場合、デバイスは、ローミング条件が次に一致するときに、指定された既定の LTE アタッチコンテキストを使用することを想定しています。  デバイスによって指定された既定の LTE アタッチコンテキストが、LTE ネットワークに登録できない場合は、必要に応じて、デバイスが 3G/2G に戻される必要があります。 モデムがパートナーネットワークと非パートナーネットワークを区別できない場合は、すべてのローミングシナリオに対して、パートナー以外の既定の LTE アタッチコンテキストを使用する必要があります。 OS で既定の LTE アタッチコンテキストが IP type = default として構成されている場合は、モデムが LTE アタッチコンテキストに最適な IP の種類を割り当てることが想定されます。  ただし、OS では、モデムがパートナーのローミング条件を返し、構成を正確に反映する LTE アタッチコンテキストの IP の種類を返すことを期待しています。

Ihv および Oem は、モデムで既定の構成として LTE アタッチコンテキストを事前に構成できますが、これらのコンテキストには MBIM_MS_CONTEXT_SOURCE = MbimMsContextSourceModemProvisioned というタグを付ける必要があります。  

既定の LTE アタッチコンテキストは、3GPP 標準に従って、UE-V によって開始された2つのカテゴリに分けられます。 デバイスが NULL の空のアクセス文字列で構成されている場合、デバイスは、ネットワークに LTE アタッチコンテキストを提供しないようにし、ネットワークがデバイスに再び割り当てられるのを待ちます。 MBIM 1.0 で規定されているように、LTE アタッチコンテキストの IP の種類が既定に構成されている場合、モデムは内部アルゴリズムに基づいて最適な IP の種類を選択する必要があります。

次の図は、LTE アタッチ構成のフローの例を示しています。

![LTE アタッチ構成のフローの例](images/LTE_attach_1.png "LTE アタッチ構成のフローの例")

#### <a name="query"></a>クエリ

完了したクエリから MBIM_MS_LTE_ATTACH_CONFIG_INFO が返され、InformationBuffer にメッセージが設定されます。 クエリの場合、InformationBuffer は NULL になります。

#### <a name="set"></a>オン

Set の場合、InformationBuffer には MBIM_MS_SET_LTE_ATTACH_CONFIG が含まれます。

#### <a name="unsolicited-events"></a>一方的なイベント

イベント InformationBuffer には MBIM_MS_LTE_ATTACH_CONFIG_INFO 構造体が含まれています。 場合によっては、既定の LTE アタッチコンテキストがネットワークによって更新されることがあります。これは、OS からの MBIM_CID_MS_LTE_ATTACH_CONFIG コマンドを経由しない無線 (OTA) またはショートメッセージサービス (SMS) によって行われます。 関数は、既定の LTE アタッチコンテキストとタグ MBIM_MS_CONTEXT_SOURCE を更新する必要があります。それに応じてプロビジョニングされます。 その後、関数は、このイベントを使用する更新プログラムについて、更新された一覧を使用してホストに通知する必要があります。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_MS_LTE_ATTACH_CONFIG | 適用なし | 適用なし |
| 応答 | MBIM_MS_LTE_ATTACH_CONFIG_INFO | MBIM_MS_LTE_ATTACH_CONFIG_INFO | MBIM_MS_LTE_ATTACH_CONFIG_INFO |

### <a name="data-structures"></a>データ構造

#### <a name="query"></a>クエリ 

InformationBuffer は NULL にする必要があり、InformationBufferLength は0である必要があります。

#### <a name="set"></a>オン

InformationBuffer では、次の MBIM_MS_SET_LTE_ATTACH_CONFIG 構造体を使用する必要があります。 Set コマンドが有効になるのは、リストの要素数が各ローミング条件 (ホーム/パートナー/非パートナー) につき3である場合のみです。

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | 操作 | MBIM_MS_LTE_CONTEXT_OPERATIONS | Set コマンドを使用する操作の種類を指定します。 MbimMsLteAttachContextOperationRestoreFactory に設定すると、他のすべてのフィールドは無視されます。 OS で作成または変更された既定の LTE アタッチコンテキストを削除し、既定のファクトリ事前構成済みの既定の LTE アタッチコンテキストを読み込む必要があります。 モデムに既定の構成がない場合は、すべてのローミング条件の既定の LTE アタッチコンテキストを空の APN 文字列に設定し、IP type = default に設定する必要があります。 |
| 4 | 4 | ElementCount (EC) | UINT32 | DataBuffer で後に続く MBIM_MS_LTE_ATTACH_CONTEXT 構造体の数。 現在、このコンポーネントは、ローミング条件ごとに1つ (ホーム/パートナー/非パートナー) に指定されています。 |
| 8 | 8 * EC | MsLteAttachContextRefList | OL_PAIR_LIST | ペアの最初の要素は4バイトオフセットで、この MBIM_MS_LTE_ATTACH_CONFIG_INFO 構造体の先頭 (オフセット 0) から MBIM_MS_LTE_ATTACH_CONTEXT 構造体に計算されます (詳細については、MBIM_MS_LTE_ATTACH_CONTEXT テーブルを参照してください)。 ペアの2番目の要素は、対応する MBIM_MS_LTE_ATTACH_CONTEXT 構造体へのポインターの4バイトサイズです。 |
| 8 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_LTE_ATTACH_CONTEXT 構造体の配列。 |

上記の表では、次の構造が使用されています。

MBIM_MS_LTE_ATTACH_CONTEXT_OPERATIONS は、Set コマンドで使用できる操作の種類について説明します。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MbimMsLteAttachContextOperationDefault | 0 | モデムの既存の既定の LTE アタッチコンテキストを上書きするための既定の操作です。 OS は、ローミング条件の3つの既定の LTE アタッチコンテキストすべてを常に置き換えます。 |
| MbimMsLteAttachContextOperationRestoreFactory | 1 | 現在挿入されている SIM のプロバイダー ID に対して、工場で事前に構成された既定の LTE アタッチコンテキストを復元します。 OS によって置き換えられるか、または作成されるすべての既定の LTE アタッチコンテキストは、削除して置き換える必要があります。 現在挿入されている SIM プロバイダー ID に対して、1つまたは複数のローミング条件を持つ既定の事前構成済みの既定の LTE アタッチコンテキストがない場合、既定の LTE アタッチは空の APN 文字列と IP type = default を返します。 |

MBIM_MS_LTE_ATTACH_CONTEXT は、LTE アタッチ構成に使用するコンテキストを指定します。

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | IPType | MBIM_CONTEXT_IP_TYPE | 詳細については、MBIM_CONTEXT_IP_TYPE の表を参照してください。 |
| 4 | 4 | ローミング | MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL | この既定の LTE アタッチコンテキストに適用されるローミング条件を示します。 詳細については、MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL の表を参照してください。 |
| 8 | 4 | source | MBIM_MS_CONTEXT_SOURCE | コンテキストの作成ソースを指定します。 詳細については、MBIM_MS_CONTEXT_SOURCE の表を参照してください。 |
| 12 | 4 | AccessStringOffset | OFFSET | ネットワークにアクセスするための文字列、AccessString へのデータバッファー内のオフセット。 GSM ベースのネットワークの場合、これは "data.thephone-company.com" などのアクセスポイント名 (APN) 文字列になります。 文字列のサイズは100文字を超えないようにする必要があります。 AccessString が空の場合、デバイスはネットワークに対して、デバイスにアクセス文字列を割り当てるように要求します。 この場合も、IP の種類を指定する必要があります。 |
| 16 | 4 | AccessStringSize | サイズ (0.. 200) | AccessString に使用されるサイズ。 デバイスがネットワークによってデバイスにアクセス文字列を割り当てて LTE attach を要求する場合、この値は0にする必要があります。 |
| 20 | 4 | UserNameOffset | OFFSET | この構造体の先頭から計算されたユーザー名を表す文字列 (UserName) までのオフセット (バイト単位)。 このメンバーは NULL にすることができます。 |
| 24 | 4 | UserNameSize | サイズ (0 ~ 510) | ユーザー名に使用されるサイズ。 |
| 28 | 4 | PasswordOffset | OFFSET | この構造体の先頭から、ユーザー名のパスワードを表す文字列 (パスワード) までのオフセット (バイト単位)。 このメンバーは NULL にすることができます。 |
| 32 | 4 | PasswordSize | サイズ (0 ~ 510) | パスワードに使用されるサイズ。 |
| 36 | 4 | 圧縮 | MBIM_COMPRESSION | データ接続でヘッダーとデータに使用する圧縮を指定します。 このメンバーは、GSM ベースのデバイスにのみ適用されます。 このメンバーは、CDMA ベースのデバイスの場合、ホストによって MBIMCompressionNone に設定されます。 詳細については、MBIM_COMPRESSION の表を参照してください。 |
| 40 | 4 | AuthProtocol | MBIM_AUTH_PROTOCOL | PDP のアクティブ化に使用する認証の種類。 詳細については、MBIM_AUTH_PROTOCOL の表を参照してください。 |
| 44 |  | DataBuffer | DATABUFFER | AccessString、UserName、および Password を含むデータバッファー。 |

MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL は、この既定の LTE アタッチコンテキストに適用されるローミング条件を示します。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MbimMsLteAttachContextRoamingControlHome | 0 | 既定の LTE アタッチコンテキストがホームネットワークでの使用を許可されているかどうかを示します。 |
| MbimMsLteAttachContextRoamingControlPartner | 1 | コンテキストがパートナーローミングネットワークで使用できるかどうかを示します。 |
| MbimMsLteAttachContextRoamingControlNonPartner | 2 | 非パートナーローミングネットワークでコンテキストを使用できるかどうかを示します。 |

MBIM_MS_CONTEXT_SOURCE コンテキストの作成ソースを指定します。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextSourceAdmin | 0 | このコンテキストは、OS から企業の IT 管理者によって作成されています。 |
| MbimMsContextSourceUser | 1 | コンテキストは、ユーザーによって OS 設定を通じて作成されました。 |
| MbimMsContextSourceOperator | 2 | コンテキストは、OMA-URI またはその他のチャネルを介してオペレーターによって作成されたものです。 | 
| MbimMsContextSourceModem | 3 | コンテキストは、IHV または OEM によって作成されたものです。 |
| MbimMsContextSourceDevice | 4 | コンテキストは、OS APN データベースによって作成されたものです。 |

#### <a name="response"></a>応答

InformationBuffer では、次の MBIM_MS_LTE_ATTACH_CONFIG_INFO 構造体を使用する必要があります。

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | DataBuffer で後に続く MBIM_MS_LTE_ATTACH_CONTEXT 構造体の数。 現在、このコンポーネントは、ローミング条件ごとに1つ (ホーム/パートナー/非パートナー) に指定されています。 |
| 4 | 8 * EC | MsLteAttachContextRefList | OL_PAIR_LIST | ペアの最初の要素は4バイトオフセットで、この MBIM_MS_LTE_ATTACH_CONFIG_INFO 構造体の先頭 (オフセット 0) から MBIM_MS_LTE_ATTACH_CONTEXT 構造体に計算されます (詳細については、MBIM_MS_LTE_ATTACH_CONTEXT テーブルを参照してください)。 ペアの2番目の要素は、対応する MBIM_MS_LTE_ATTACH_CONTEXT 構造体へのポインターの4バイトサイズです。 |
| 4 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_LTE_ATTACH_CONTEXT 構造体の配列。 |

#### <a name="notification"></a>通知

詳細については、MBIM_MS_LTE_ATTACH_CONFIG_INFO の表を参照してください。

### <a name="status-codes"></a>状態コード

クエリおよびセット操作の場合:

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | デバイスがプロビジョニングされたコンテキストを取得できなかったため、操作に失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスで操作がサポートされていないため、操作に失敗しました。 |

Set 操作のみ: 

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーターのため、操作に失敗しました。 |
| MBIM_STATUS_WRITE_FAILURE  | 更新要求が失敗したため、操作に失敗しました。 |

## <a name="mbim_cid_ms_lte_attach_status"></a>MBIM_CID_MS_LTE_ATTACH_STATUS

### <a name="description"></a>説明

3GPP の要件ごとに、デバイスは、有効な PDP コンテキストを使用せずに LTE をネットワークに接続するときに使用する既定の LTE アタッチコンテキストを指定できますが、デバイスに構成されている既定の LTE アタッチコンテキストとは異なる PDP コンテキストでデバイスが LTE される場合があります。 考えられるすべてのシナリオの一覧を次に示します。

1.  UE-V は、特定の LTE 接続 APN を指定します。
2.  UE-V は特定の LTE 接続 APN を指定しますが、ネットワークでは、ローミング時に別の APN にデバイスをアタッチすることを決定します。
3.  UE-V は、LTE 接続 APN を指定せず、ネットワークがデバイスに再び割り当てられるようにします。
4.  UE-V/3G ネットワークから LTE に登録され、アクティブな PDP コンテキストが少なくとも1つは既に存在していました。 ネットワークでは、これを LTE 接続 APN として使用します。

デバイスの既定の LTE がアタッチされるときに、最新の LTE 添付ファイルの PDP コンテキストの詳細を提供するために、OS に MBIM_CID_MS_LTE_ATTACH_STATUS の通知を送信する必要があります。 既定の LTE アタッチは、次のいずれかのシナリオが満たされた場合に発生します。

1.  デバイスは最初に LTE ネットワークに接続します。
2.  デバイスは、以前に有効にした PDP コンテキストを使用せずに、2G/3G から LTE にデバイスを渡します。

MBIM_CID_LTE_ATTACH_STATUS から返された LTE アタッチコンテキストは、次のいずれかになります。

1.  モデムに格納されている既定の LTE アタッチコンテキスト。
2.  ネットワークから割り当てられた既定の LTE アタッチコンテキスト。

実行時に、OS は最後に使用されたアタッチ情報が既定の LTE アタッチに対してどのようなものであったかも照会できる必要があります。 モデムは、最後に認識された既定の LTE アタッチコンテキストを返すことが想定されています。  デバイスが LTE から 2G/3G ネットワークに渡された場合は、以前の LTE 接続に使用されていたコンテキストがモデムによって返されることが想定されます。 デバイスがネットワークから解除するたびに、APN が空になることが予想されます。

次の図は、LTE アタッチステータスのメッセージフローの例を示しています。

![LTE アタッチステータスのフローの例](images/LTE_attach_2.png "LTE アタッチステータスのフローの例")

#### <a name="query"></a>クエリ

InformationBuffer 内のクエリ完了メッセージから MBIM_MS_LTE_ATTACH_STATUS が返されます。 クエリの場合、InformationBuffer は NULL になります。

#### <a name="set"></a>オン 

設定操作はサポートされていません。

#### <a name="unsolicited-events"></a>一方的なイベント

イベント InformationBuffer には MBIM_MS_LTE_ATTACH_STATUS 構造体が含まれています。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 適用なし | 適用なし | 適用なし |
| 応答 | 適用なし | MBIM_MS_LTE_ATTACH_STATUS | MBIM_MS_LTE_ATTACH_STATUS |

### <a name="data-structures"></a>データ構造

#### <a name="query"></a>クエリ

InformationBuffer は NULL にする必要があり、InformationBufferLength は0である必要があります。

#### <a name="set"></a>オン

設定操作はサポートされていません。

#### <a name="response"></a>応答

InformationBuffer では、次の MBIM_MS_LTE_ATTACH_STATUS 構造体を使用する必要があります。


| Offset | サイズ |       フィールド        |           Type           |                                                                                                                                                                                                                                                                                                    説明                                                                                                                                                                                                                                                                                                     |
|--------|------|--------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |   LteAttachState   | MBIM_MS_LTE_ATTACH_STATE |                                                                                                                                                                                                                                    デバイスが現在 LTE ネットワークに接続されているかどうかを示します。  詳細については、MBIM_MS_LTE_ATTACH_STATE の表を参照してください。                                                                                                                                                                                                                                     |
|   4    |  4   |       IPType       |  MBIM_CONTEXT_IP_TYPES   |                                                                                                                                                                                                                                                                             詳細については、MBIM_CONTEXT_IP_TYPE の表を参照してください。                                                                                                                                                                                                                                                                              |
|   8    |  4   | AccessStringOffset |          OFFSET          | ネットワークにアクセスするための文字列、AccessString へのデータバッファー内のオフセット。 GSM ベースのネットワークの場合、これは "data.thephone-company.com" などのアクセスポイント名 (APN) 文字列になります。 CDMA ベースのネットワークの場合、これは "#777" などの特別なダイヤルコードや "" などのネットワークアクセス識別子 (NAI) である可能性があり foo@thephone-company.com ます。 ネットワークが既定の APN を割り当てるように要求するには、このメンバーを NULL にすることができます。 注: すべてのネットワークがこの NULL APN 規則をサポートしているわけではありません。 そのため、APN が無効であるという接続エラーが発生する可能性があります。 文字列のサイズは100文字を超えないようにする必要があります。 |
|   12   |  4   |  AccessStringSize  |       サイズ (0.. 200)       |                                                                                                                                                                                                                                                                                        AccessString に使用されるサイズ (バイト単位)。                                                                                                                                                                                                                                                                                        |
|   16   |  4   |   UserNameOffset   |          OFFSET          |                                                                                                                                                                                                                          この構造体の先頭から計算されたユーザー名を表す文字列 (UserName) までのオフセット (バイト単位)。 このメンバーは NULL にすることができます。                                                                                                                                                                                                                           |
|   20   |  4   |    UserNameSize    |       サイズ (0 ~ 510)       |                                                                                                                                                                                                                                                                                          ユーザー名に使用されるサイズ (バイト単位)。                                                                                                                                                                                                                                                                                          |
|   24   |  4   |   PasswordOffset   |          OFFSET          |                                                                                                                                                                                                                             この構造体の先頭から、ユーザー名のパスワードを表す文字列 (パスワード) までのオフセット (バイト単位)。 このメンバーは NULL にすることができます。                                                                                                                                                                                                                             |
|   28   |  4   |    PasswordSize    |       サイズ (0 ~ 510)       |                                                                                                                                                                                                                                                                                          パスワードに使用されるサイズ (バイト単位)。                                                                                                                                                                                                                                                                                          |
|   32   |  4   |    圧縮     |     MBIM_COMPRESSION     |                                                                                                                                                                           データ接続でヘッダーとデータに使用する圧縮を指定します。 このメンバーは、GSM ベースのデバイスにのみ適用されます。 このメンバーは、CDMA ベースのデバイスの場合、ホストによって MBIMCompressionNone に設定されます。 詳細については、MBIM_COMPRESSION の表を参照してください。                                                                                                                                                                           |
|   36   |  4   |    AuthProtocol    |    MBIM_AUTH_PROTOCOL    |                                                                                                                                                                                                                                                     PDP のアクティブ化に使用する認証の種類。 詳細については、MBIM_AUTH_PROTOCOL の表を参照してください。                                                                                                                                                                                                                                                     |
|   40   |  4   |                    |        DataBuffer        |                                                                                                                                                                                                                                                                                                     DATABUFFER                                                                                                                                                                                                                                                                                                     |

前の表では、次のデータ構造が使用されています。

MBIM_MS_LTE_ATTACH_STATE デバイスが現在 LTE ネットワークに接続されているかどうかを示します。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MbimMsLteAttachStateDetached れた | 0 | デバイスが LTE ネットワークに接続されていないことを示します。 |
| MbimMsLteAttachStateAttached | 1 | デバイスが LTE ネットワークに接続されていることを示します。 |

#### <a name="notification"></a>通知

詳細については、MBIM_MS_LTE_ATTACH_STATUS の表を参照してください。

### <a name="status-codes"></a>状態コード

クエリおよびセット操作の場合:

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | デバイスがプロビジョニングされたコンテキストを取得できなかったため、操作に失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスで操作がサポートされていないため、操作に失敗しました。 |
