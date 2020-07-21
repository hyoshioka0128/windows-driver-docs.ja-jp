---
title: MB プロビジョニング済みコンテキスト操作
description: MB プロビジョニング済みコンテキスト操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cee79df1a940215e800a7405b5596f0c09572fff
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557771"
---
# <a name="mb-provisioned-context-operations"></a>MB プロビジョニング済みコンテキスト操作

携帯ネットワーク接続デバイスの場合、プロビジョニングは不可欠です。これは、各携帯電話事業者がネットワーク用の APN 構成が異なるためです。 APN の構成は、通常、次の2つのカテゴリに分けられます。

1. この接続を必要とする OS より上位のアプリケーションまたはクライアントがあるため、OS に認識されている APN 構成。
2. APN は os とそのクライアントによって利用されていない接続のためにモデムによって内部で使用されるため、OS に認識されない構成です。

理想的には、モデムは、OS が認識している必要のない APN 構成だけを格納する必要があります。 ただし、IHV および OEM パートナーは従来、インターネットを提供しており、APNs (OS が認識している構成) もモデムで購入しています。 Windows 10 バージョン1703のリリースより前のバージョンでは、インターネット接続を確立するために、インターネットのみを読み取り、APN 構成をモデムから購入します。 Windows 10 バージョン1703以降では、モデムの APN 構成が Windows によって管理される必要がある場合があります。特に、携帯電話の構成を変更する必要があるユーザー設定や OMA-URI などのクライアントが OS にある場合です。 これは、モデムの APN 構成にも影響する可能性があります。 たとえば、ims 経由で SMS の IMS APN を使用している IMS スタックがモデムに存在する可能性があります。 通常、これらの接続は OS に公開されませんが、特定のシナリオでは、IMS APN 構成の変更が必要になる場合があります。 この変更は、OS を使用して行うことができます。 これをサポートするために、Windows 10 バージョン1703以降の OS では、さまざまな種類の APNs をモデムに構成できます。

USB フォーラムの MBIM 1.0 と Microsoft NDIS にはそれぞれ既存の CID と OID があり、OS がモデムで APN の構成を設定して照会することができます。 MBIM 1.0 の場合、この処理は MBIM_CID_PROVISIONED_CONTEXT によって行われますが、NDIS では[OID_WWAN_PROVISIONED_CONTEXTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-provisioned-contexts)によって行われます。 ただし、既存の CID と OID は、電源サイクルや SIM スワップなどさまざまな状況でモデムがどのように動作するかについての明確なガイダンスを使用して設計されていませんでした。 OS をサポートする必要があるデバイスは、今後、モデムでプロビジョニングされたコンテキストの構成と更新を行うために、Windows 10 バージョン1703で CID および OID の新しいバージョンを実装する必要があります。 旧バージョンとの互換性を確保するため、1703より前の OS バージョンで新しいハードウェアをサポートする必要がある場合は、既存の MBIM_CID_PROVISIONED_CONTEXT と OID_WWAN_PROVISIONED_CONTEXTS を引き続きサポートする必要があります。  Windows 10 バージョン1703以降では、デバイスで CID と OID の新しいバージョンがサポートされている場合、OS は、新しいバージョンのコマンドのみを使用して、モデムで APN のコンテキスト構成を照会および設定します。 

## <a name="mb-interface-update-for-provisioned-context-operations"></a>プロビジョニングされたコンテキスト操作のための、MB インターフェイスの更新

MBIM には、モデムに格納されているコンテキストを取得および置換するためのコマンドがありますが、プロファイルを "無効" または "有効" にするためのフィールドはありません。  このため、この機能を使用するには、Windows 10 バージョン1703で既存の MBIM_CID_PROVISIONED_CONTEXT を更新する必要があります。 MBIM にはバージョン管理メカニズムがないため、新しい MSFT 専用 CID が MBIM_CID_MS_PROVISIONED_CONTEXT_V2 として定義されます。

サービス名 =**基本接続拡張機能**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 値 = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

| CID | コマンド コード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_MS_PROVISIONED_CONTEXT_V2 | 1 | Windows 10 Version 1703 |

### <a name="mbim_cid_ms_provisioned_context_v2"></a>MBIM_CID_MS_PROVISIONED_CONTEXT_V2

#### <a name="description"></a>説明

MBIM 1.0 では、OS とその上位クライアントがモデムでプロビジョニングされたコンテキストを管理する MBIM_CID_PROVISIONED_CONTEXT が定義されていますが、従来はモデムでコンテキストを照会しただけで、OS からは設定していませんでした。 Windows 10 バージョン1703以降では、OS がモデムでコンテキストを構成できる必要が高まっています。 たとえば、OS に対して非透過的な IMS スタックがモデムに存在する場合、OS では、モデムが使用する IMS APN を指定できる必要があります。 各モデム IHV は、独自の独自の方法でモデムにコンテキストを格納できるので、MBIM_CID_PROVISIONED_CONTEXT に示すように、OS が ContextId レベルでプロファイルを管理することは不可能です。 代わりに、OS の観点から、コンテキストの種類ごとに使用するコンテキストを指定することが重要になります。 IMS の例に戻ります。モデムに含まれる既存のプロビジョニング済みのコンテキストの数に関係なく、OS が MBIM_CONTEXT_TYPE = IMS を持つコンテキストを設定した場合は、モデムによって開始されたすべての IMS トラフィックをそのコンテキストでのみ試行する必要があります。

MBIM 1.0 は、挿入された SIM カードのプロバイダー ID (MCC/MBIM ペア) に一致するコンテキストに対してのみ、MBIM_CID_PROVISIONED_CONTEXT が呼び出しを行うことを指定します。 Set 要求の場合、MBIM_CID_PROVISIONED_CONTEXT は、格納するコンテキストのプロバイダー ID を指定できます。  MBIM_CID_MS_PROVISIONED_CONTEXT_V2 は、MBIM 1.0 と類似しているが異なる動作を指定します。 各クエリに対して、OS は、挿入された SIM カードのプロバイダー ID と一致するコンテキストのみが返されることを想定しています。 Set の場合、OS は SIM カードの現在のプロバイダー ID と一致しないコンテキストを設定できなくなります。 Set 要求では、提示された SIM カードの現在のプロバイダー ID のコンテキストを作成する必要があります。 たとえば、ユーザーは SIM 1 から SIM 2 にスワップしてから、SIM 1 に戻します。 最初の SIM スワップ中に、SIM 2 のコンテキストを読み込む前に、モデムがすべてのコンテキストを解決する必要があると想定されています。 ユーザーが SIM 1 にスワップバックすると、SIM 1 の出荷時の既定の構成を復元する必要があります。  モデムが SIM スワップ全体でランタイム構成を保存することは想定されていません。

次の図は、ユーザーが1つの SIM から別の SIM にスワップする場合のサンプルフローを示しています。

![モデムコンテキストプロビジョニングの SIM スワップの例](images/Context_Provision_modem_context_1.png "モデムコンテキストプロビジョニングの SIM スワップの例")

Oem と Ihv は、OS またはユーザーがモデムのコンテキスト設定を元の設定に復元しようとしている場合に備えて、元のファクトリ構成を保持する必要があります。 現在挿入されている SIM のプロバイダー ID の元のファクトリコンテキストだけを復元する必要があります。 元のファクトリ設定の構成済みコンテキストは、OS の構成で上書きされないようにする必要があります。 次の図は、ユーザーがファクトリ設定の復元を選択した場合のフローの例を示しています。

![モデムコンテキストプロビジョニングファクトリのリセットの例](images/Context_Provision_modem_context_2.png "モデムコンテキストプロビジョニングファクトリのリセットの例")

SIM が不足しているか、ロックされているか、プロバイダー ID にアクセスできないときに、モデムがクエリまたは設定要求に失敗することが予想されます。 モデムには、プロバイダー ID ごとに CONTEXT_TYPE ごとに1つのコンテキストのみが必要です。 IHV または OEM がモデムのコンテキストを事前に構成することを決定した場合、それを選択する各プロバイダーに対してコンテキストが正しく構成されていることを確認することが重要です。 挿入された SIM カードに IHV 事前構成済みのコンテキストがない場合、そのモデムには OS の構成のないコンテキストが含まれていてはなりません。 Ihv と Oem は、MbimMsContextSourceModemProvisioned = を MBIM_MS_CONTEXT_SOURCE 確認する必要があります。これにより、OS は接続に対してモデムのコンテキストを使用し、存在する場合は Windows の APN データベースからは上書きしないようにします。

モデムマップがコンテキストをどのように処理し、既存の MBIM_CID_PROVISIONED_CONTEXT を通じて元に戻すかは、各 IHV によって行われ、このドキュメントでは扱いません。

新しい MBIM_CID_MS_PROVISONED_CONTEXT_V2 コマンドは、MBIM 1.0 の既存の MBIM_CID_PROVISIONED_CONTEXT コマンドとほぼ同じですが、いくつか追加されています。 1つ目の方法では、OS は、モデムのコンテキスト型に関連付けられたコンテキストを有効または無効にすることができます。 モデムでコンテキストが無効になっている場合、ネットワークとの接続には、OS に認識されていないものも含めて、保存されたコンテキストを使用しないことが求められます。 OS がモデムの無効なコンテキストに一致する接続を要求した場合、モデムはネットワークに通知せずに直ちに要求を失敗させる必要があります。 照合プロセスは、MBIM_MS_CONTEXT_V2 構造内のすべてのフィールドと一致している必要があります。

MBIM 1.0 の MBIM_CONTEXT_IP_TYPE 構造は、MBIM_CID_CONNECT にのみ使用されます。 MBIM_CID_MS_PROVISIONED_CONTEXT_V2 では、Microsoft が各コンテキストのパラメーターの1つとして IP の種類を追加しました。 指定されたコンテキストに対して構成されていない場合、モデムは MBIMContextIPTypeDefault を報告する必要があります。 

MBIM_CID_MS_PROVISIONED_CONTEXT_V2 をサポートする新しいハードウェアを使用した Windows 10 バージョン1703では、従来の MBIM_CID_PROVISIONED_CONTEXT はファーストパーティコンポーネントからは使用されません。 MBIM_CID_PROVISIONED_CONTEXT を送信する他のレガシクライアント/OS コンポーネントがある場合、モデムは、Windows 10 バージョン1703より前のバージョンの Windows で行ったように、結果を返すことが期待されます。

##### <a name="query"></a>クエリ

MBIM_MS_PROVISIONED_CONTEXTS_INFO は、両方のクエリから返され、InformationBuffer 内の完了メッセージを設定します。 

クエリの場合、InformationBuffer は null になります。

##### <a name="set"></a>オン

Set の場合、InformationBuffer には MBIM_MS_SET_PROVISIONED_CONTEXT_V2 構造体が含まれます。 設定操作では、各モデム IHV がコンテキスト記憶域を管理する独自の方法を持つことができるため、OS では ContextId フィールドが指定されなくなり、適切なスロットにコンテキストがマップされることが求められます。 OS は、コンテキストを設定するときに、指定されたコンテキストの MBIM_CONTEXT_TYPE と一致するすべての接続に対して、そのコンテキストを使用することを想定しています。 MBIM_CONTEXT_TYPE がモデムによって認識されない場合でも、接続できない場合でも、保存されます。

##### <a name="unsolicited-event"></a>一方的なイベント

イベント InformationBuffer には MBIM_MS_PROVISIONED_CONTEXTS_INFO_V2 構造体が含まれています。 場合によっては、プロビジョニングされたコンテキストの一覧がネットワークによって更新されることがあります。これは、OS からの MBIM_CID_MS_PROVISIONED_CONTEXT_V2 コマンドを経由しない無線 (OTA) またはショートメッセージサービス (SMS) によって行われます。 関数は、プロビジョニングされたコンテキストとタグ MBIM_MS_CONTEXT_SOURCE を更新する必要があります。これは、それに応じてプロビジョニングされます。 その後、関数は、更新された一覧と共にこのイベントを使用して、ホストに更新プログラムについて通知する必要があります。

#### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_SET_MS_PROVISIONED_CONTEXT_V2 | 適用なし | 適用なし |
| 応答 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 |

#### <a name="data-structures"></a>データ構造

##### <a name="query"></a>クエリ

InformationBuffer は NULL にする必要があり、InformationBufferLength は0である必要があります。

##### <a name="set"></a>オン

次の MBIM_SET_MS_PROVISIONED_CONTEXT_V2 データ構造は、InformationBuffer で使用する必要があります。


| Offset | サイズ |       フィールド        |              Type               |                                                                                                                                                                                                                                                                                                   説明                                                                                                                                                                                                                                                                                                   |
|--------|------|--------------------|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |     操作      |   MBIM_MS_CONTEXT_OPERATIONS    |                                             SET コマンドを使用する操作の種類を指定します。 MbimMsContextOperationDelete に設定すると、指定した MBIM_CONTEXT_TYPES のコンテキストが削除され、MBIM_SET_MS_PROVISIONED_CONTEXT_V2 内の他のすべてのフィールドは無視されます。  MbimMsContextOperationRestoreFactory に設定されている場合は、OS で作成または変更されたすべてのコンテキストを削除し、既定のファクトリ事前構成済みコンテキストを読み込む必要があります。また、MBIM_SET_MS_PROVISIONED_CONTEXT_V2 内の他のすべてのフィールドは無視する必要があります。                                              |
|   4    |  16  |    ContextType     |       MBIM_CONTEXT_TYPES        |                                                                                                                                                                                                表されるコンテキストの種類を指定します。たとえば、インターネット接続、VPN (企業ネットワークへの接続)、またはボイスオーバー IP (VOIP) などです。 詳細については、MBIM_CONTEXT_TYPES の表を参照してください。                                                                                                                                                                                                |
|   20   |  4   |       IPType       |      MBIM_CONTEXT_IP_TYPES      |                                                                                                                                                                                               表されるコンテキストの種類を指定します。たとえば、インターネット接続、VPN (企業ネットワークへの接続)、またはボイスオーバー IP (VOIP) などです。 詳細については、MBIM_CONTEXT_IP_TYPES の表を参照してください。                                                                                                                                                                                               |
|   24   |  4   |       有効化       |     MBIM_MS_CONTEXT_ENABLE      |                                                                                                                                                                     モデムがコンテキストを使用できるかどうかを指定します。 MbimMsContextDisabled に設定されている場合、コンテキストに一致するすべての OS 接続要求を、ネットワークに通知せずに失敗させる必要があります。 詳細については、MBIM_MS_CONTEXT_ENABLE の表を参照してください。                                                                                                                                                                     |
|   28   |  4   |      ローミング       | MBIM_MS_CONTEXT_ROAMING_CONTROL |                                                                                                                                                                                                                                       このコンテキストでローミングが許可されるかどうかを指定します。 詳細については、MBIM_MS_CONTEXT_ROAMING_CONTROL の表を参照してください。                                                                                                                                                                                                                                        |
|   32   |  4   |     MediaType      |   MBIM_MS_CONTEXT_MEDIA_TYPE    |                                                                                                                                                                                                                                         コンテキストが使用されるメディアトランスポートの種類を指定します。 詳細については、MBIM_MS_CONTEXT_MEDIA_TYPE の表を参照してください。                                                                                                                                                                                                                                         |
|   36   |  4   |       source       |     MBIM_MS_CONTEXT_SOURCE      |                                                                                                                                                                                                                                                    コンテキストの作成ソースを指定します。 詳細については、MBIM_MS_CONTEXT_SOURCE の表を参照してください。                                                                                                                                                                                                                                                    |
|   40   |  4   | AccessStringOffset |             OFFSET              | ネットワークにアクセスするための文字列、AccessString へのデータバッファー内のオフセット。 GSM ベースのネットワークの場合、これは "data.thephone-company.com" などのアクセスポイント名 (APN) 文字列になります。 CDMA ベースのネットワークの場合、これは "#777" などの特別なダイヤルコードや "" などのネットワークアクセス識別子 (NAI) である可能性があり foo@thephone-company.com ます。 ネットワークが既定の APN を割り当てるように要求するには、このメンバーを NULL にすることができます。 注: すべてのネットワークでこの NULL APN 規則がサポートされているわけではありません。そのため、無効な APN によって接続エラーが発生する可能性があります。 文字列のサイズは100文字を超えないようにする必要があります。 |
|   44   |  4   |  AccessStringSize  |          サイズ (0.. 200)           |                                                                                                                                                                                                                                                                                           AccessString に使用されるサイズ。                                                                                                                                                                                                                                                                                           |
|   48   |  4   |   UserNameOffset   |             OFFSET              |                                                                                                                                                                                                                         この構造体の先頭から計算されたユーザー名を表す文字列 (UserName) までのオフセット (バイト単位)。 このメンバーは NULL にすることができます。                                                                                                                                                                                                                         |
|   52   |  4   |    UserNameSize    |          サイズ (0 ~ 510)           |                                                                                                                                                                                                                                                                                            ユーザー名に使用されるサイズ。                                                                                                                                                                                                                                                                                             |
|   56   |  4   |   PasswordOffset   |             OFFSET              |                                                                                                                                                                                                                           この構造体の先頭から、ユーザー名のパスワードを表す文字列 (パスワード) までのオフセット (バイト単位)。 このメンバーは NULL にすることができます。                                                                                                                                                                                                                            |
|   60   |  4   |    PasswordSize    |          サイズ (0 ~ 510)           |                                                                                                                                                                                                                                                                                             パスワードに使用されるサイズ。                                                                                                                                                                                                                                                                                             |
|   64   |  4   |    圧縮     |        MBIM_COMPRESSION         |                                                                                                                                                                         データ接続でヘッダーとデータに使用する圧縮を指定します。 このメンバーは、GSM ベースのデバイスにのみ適用されます。 このメンバーは、CDMA ベースのデバイスの場合、ホストによって MBIMCompressionNone に設定されます。 詳細については、MBIM_COMPRESSION の表を参照してください。                                                                                                                                                                          |
|   68   |  4   |    AuthProtocol    |       MBIM_AUTH_PROTOCOL        |                                                                                                                                                                                                                                                   PDP のアクティブ化に使用する認証の種類。 詳細については、MBIM_AUTH_PROTOCOL の表を参照してください。                                                                                                                                                                                                                                                    |
|   72   |  4   |     DataBuffer     |           DATABUFFER            |                                                                                                                                                                                                                                                                       AccessString、UserName、および Password を含むデータバッファー。                                                                                                                                                                                                                                                                       |

前の表では、次のデータ構造が使用されています。

MBIM_MS_CONTEXT_ROAMING_CONTROL は、コンテキスト間のローミングポリシーを指定します。 OS では、特定のコンテキストをローミング中に有効にできるかどうかを指定できます。 ローミングの状態が指定された条件を満たさない場合、モデムは OS の介入なしにコンテキストを自己アクティブ化しないようにする必要があります。 モデムがパートナーをサポートしていない場合は、すべてのパートナー構成を home と同等として扱う必要があります。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextRoamingControlHomeOnly | 0 | コンテキストをホームネットワークでのみ使用できるようにするかどうかを示します。 |
| MbimMsContextRoamingControlPartnerOnly | 1 | コンテキストがパートナーローミングネットワークでのみ使用できるかどうかを示します。 |
| MbimMsContextRoamingControlNonPartnerOnly | 2 | コンテキストを非パートナーローミングネットワークでのみ使用できるようにするかどうかを示します。 | 
| MbimMsContextRoamingControlHomeAndPartner | 3 | コンテキストをホームおよびパートナーのローミングネットワークで使用できるかどうかを示します。 |
| MbimMsContextRoamingControlHomeAndNonPartner | 4 | コンテキストを、ホームおよび非パートナーのローミングネットワークで使用できるかどうかを示します。 |
| MbimMsContextRoamingControlPartnerAndNonPartner | 5 | コンテキストをパートナーおよび非パートナーのローミングネットワークで使用できるかどうかを示します。 |
| MbimMsContextRoamingControlAllowAll | 6 | コンテキストをローミング条件で使用できるかどうかを示します。 |

MBIM_MS_CONTEXT_MEDIA_TYPE が追加され、今後のプラットフォームで Wi-fi オフロードがサポートされるようになったときに、携帯ネットワークまたは iWLAN にコンテキストを使用するかどうかを指定できるようになりました。 たとえば、コンテキストが携帯電話として設定されていて、モデムが現在 Wi-fi オフロードである場合、そのコンテキストを使用して接続を開始することはできません。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextMediaTypeCellularOnly | 0 | 携帯電話で登録されている場合にのみ、コンテキストを使用できるようにするかどうかを示します。 |
| MbimMsContextMediaTypeWifiOnly | 1 | IWLAN (Wi-fi オフロード) で登録されている場合にのみ、コンテキストを使用できるようにするかどうかを示します。 |
| MbimMsContextMediaTypeAll | 2 | 携帯電話または Wi-fi のいずれかを使用して登録した場合に、コンテキストを使用できるかどうかを示します。 |

MBIM_MS_CONTEXT_ENABLE コンテキストが有効か無効かを指定します。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextDisabled | 0 | プロビジョニングされたコンテキストが無効になっています。 このコンテキストでは、オペレーティングシステムからのライセンス認証を有効にしないようにしてください。 |
| MbimMsContextEnabled | 1 | プロビジョニングされたコンテキストが有効になっています。 他の条件が満たされている場合は、コンテキストを有効にすることができます。たとえば、ローミングが許可されていない場合、ローミング中にコンテキストを有効にすることはできません。 |

モデムのコンテキストの作成方法を OS で確認できるように MBIM_MS_CONTEXT_SOURCE が追加されました。 これにより、工場出荷時のリセットなどのさまざまな状況で、OS が正しく動作するようになります。そのため、何を永続化する必要があるか、およびさまざまなオペレーターの要件に基づいて既定の状態に戻す必要があります。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextSourceAdmin | 0 | このコンテキストは、OS から企業の IT 管理者によって作成されています。 |
| MbimMsContextSourceUser | 1 | コンテキストは、ユーザーによって OS 設定を通じて作成されました。 | 
| MbimMsContextSourceOperator | 2 | コンテキストは、OMA-URI またはその他のチャネルを介してオペレーターによって作成されたものです。 |
| MbimMsContextSourceModem | 3 | このコンテキストは、モデムファームウェアに付属していた IHV または OEM によって作成されたものです。 |
| MbimMsContextSourceDevice | 4 | コンテキストは、OS APN データベースによって作成されたものです。 |

MBIM_MS_CONTEXT_OPERATIONS は、OS がモデムのコンテキストを構成するために実行できる操作を指定します。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MbimMsContextOperationDefault | 0 | モデムの既存のコンテキストの追加または置換を含む既定の操作。 |
| MbimMsContextOperationDelete | 1 | 削除操作では、モデムがモデムの既存のコンテキストを削除する必要があります。 | 
| MbimMsContextOperationRestoreFactory | 2 | 現在挿入されている SIM のプロバイダー ID に対して、ファクトリの事前構成済みコンテキストを復元します。 OS によって置換または作成されたすべてのコンテキストを削除して置き換える必要があります。 現在挿入されている SIM プロバイダー ID に対して既定の事前構成済み OS コンテキストがない場合は、モデムでプロビジョニングされたコンテキストを削除する必要があります。 |

MBIM 1.0 からの元の MBIM_CONTEXT_TYPES はまだ有効です。 Microsoft では、MBIM 1.0 が定義されて以来、より多くの種類のコンテキストを追加しています。 次の表は、導入される新しい型を定義しています。 Ihv と Oem は、独自の目的のために OS によって認識されない他の一意の UUID 値を持つ他の独自のコンテキストタイプを定義できます。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMMsContextTypeAdmin | 5f7e4c2e-e80b-40a9-a239-f0abcfd11f4b | コンテキストは、デバイス管理などの管理目的で使用されます。 |
| MBIMMSContextTypeApp | 74d88a3d-dfbd-4799-9a8c-7310a37bb2ee | このコンテキストは、モバイルオペレーターによってホワイトリストに登録された特定のアプリケーションに使用されます。 |
| MBIMMsContextTypeXcap | 50d378a7-baa547 a50-b87 2-3fe5bb463411 | このコンテキストは、IMS サービスでの XCAP のプロビジョニングに使用されます。 |
| MBIMMsContextTypeTethering | 5e4e0601-48dc-4e2b-acb8-08b4016bbaac | このコンテキストは、モバイルホットスポットテザリングに使用されます。 |
| MBIMMsContextTypeEmergencyCalling | 5f41adb8-204e-4d31-9da8-b3c970e360f2 | このコンテキストは、IMS 緊急呼び出しに使用されます。 |

##### <a name="response"></a>応答

InformationBuffer では、次の MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 構造体を使用する必要があります。

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | DataBuffer で後に続く MBIM_MS_CONTEXT_V2 構造体の数。 |
| 4 | 8 * EC | MsProvisionedContextV2RefList | OL_PAIR_LIST | ペアの最初の要素は、この MBIM_MS_PROVISIONED_CONTEXTS_INFO_V2 構造体の先頭 (オフセット 0) から MBIM_MS_CONTEXT_V2 構造体までの4バイトオフセット (バイト単位) です (詳細については、MBIM_MS_CONTEXT_V2 テーブルを参照してください)。 ペアの2番目の要素は、対応する MBIM_MS_CONTEXT_V2 構造体へのポインターの4バイトサイズです。 |
| 4 + 8 * EC |  | DataBuffer | DATABUFFER | MBIM_MS_CONTEXT_V2 structuers の配列。 |

前の表で使用されている MBIM_MS_CONTEXT_V2 は、特定のコンテキストに関する情報を提供します。


| Offset | サイズ |       フィールド        |              型               |                                                                                                                                                                                                                                                                                                 [説明]                                                                                                                                                                                                                                                                                                  |
|--------|------|--------------------|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |     ContextId      |             UINT32              |                                                                                                                                                                                                                                                                                        このコンテキストの一意の ID。                                                                                                                                                                                                                                                                                         |
|   4    |  16  |    ContextType     |       MBIM_CONTEXT_TYPES        |                                                                                                                                                      表されるコンテキストの種類を指定します。たとえば、インターネット接続、VPN (企業ネットワークへの接続)、またはボイスオーバー IP (VOIP) などです。 空またはプロビジョニング解除されたコンテキストには、デバイスで MBIMContextTypeNone を指定する必要があります。 詳細については、MBIM_CONTEXT_TYPES の表を参照してください。                                                                                                                                                       |
|   20   |  4   |       IPType       |      MBIM_CONTEXT_IP_TYPES      |                                                                                                                                                                                                                                                                         詳細については、MBIM_CONTEXT_IP_TYPES の表を参照してください。                                                                                                                                                                                                                                                                          |
|   24   |  4   |       有効化       |     MBIM_MS_CONTEXT_ENABLE      |                                                                                                                                                                   モデムがコンテキストを使用できるかどうかを指定します。 MbimMsContextDisabled に設定されている場合、コンテキストに一致するすべての OS 接続要求を、ネットワークに通知せずに失敗させる必要があります。 詳細については、MBIM_MS_CONTEXT_ENABLE の表を参照してください。                                                                                                                                                                    |
|   28   |  4   |      ローミング       | MBIM_MS_CONTEXT_ROAMING_CONTROL |                                                                                                                                                                                                                                      このコンテキストでローミングが許可されるかどうかを指定します。 詳細については、MBIM_MS_CONTEXT_ROAMING_CONTROL の表を参照してください。                                                                                                                                                                                                                                      |
|   32   |  4   |     MediaType      |   MBIM_MS_CONTEXT_MEDIA_TYPE    |                                                                                                                                                                                                                                       コンテキストが使用されるメディアトランスポートの種類を指定します。 詳細については、MBIM_MS_CONTEXT_MEDIA_TYPE の表を参照してください。                                                                                                                                                                                                                                        |
|   36   |  4   |       source       |     MBIM_MS_CONTEXT_SOURCE      |                                                                                                                                                                                                                                                  コンテキストの作成ソースを指定します。 詳細については、MBIM_MS_CONTEXT_SOURCE の表を参照してください。                                                                                                                                                                                                                                                   |
|   40   |  4   | AccessStringOffset |             OFFSET              | ネットワークにアクセスするための文字列、AccessString へのデータバッファー内のオフセット。 GSM ベースのネットワークの場合、これは "data.thephone-company.com" などのアクセスポイント名 (APN) 文字列になります。 CDMA ベースのネットワークの場合、これは "#777" などの特別なダイヤルコードや "" などのネットワークアクセス識別子 (NAI) である可能性があり foo@thephone-company.com ます。 このメンバーは NULL にすることができ、ネットワークが既定の APN を割り当てるように要求します。 注: すべてのネットワークでこの NULL APN 規則がサポートされているわけではありません。そのため、無効な APN によって接続エラーが発生する可能性があります。 文字列のサイズは100文字を超えないようにする必要があります。 |
|   44   |  4   |  AccessStringSize  |          サイズ (0.. 200)           |                                                                                                                                                                                                                                                                                         AccessString に使用されるサイズ。                                                                                                                                                                                                                                                                                          |
|   48   |  4   |   UserNameOffset   |             OFFSET              |                                                                                                                                                                                                                       この構造体の先頭から計算されたユーザー名を表す文字列 (UserName) までのオフセット (バイト単位)。 このメンバーは NULL にすることができます。                                                                                                                                                                                                                        |
|   52   |  4   |    UserNameSize    |          サイズ (0 ~ 510)           |                                                                                                                                                                                                                                                                                           ユーザー名に使用されるサイズ。                                                                                                                                                                                                                                                                                           |
|   56   |  4   |   PasswordOffset   |             OFFSET              |                                                                                                                                                                                                                          この構造体の先頭から、ユーザー名のパスワードを表す文字列 (パスワード) までのオフセット (バイト単位)。 このメンバーは NULL にすることができます。                                                                                                                                                                                                                          |
|   60   |  4   |    PasswordSize    |          サイズ (0 ~ 510)           |                                                                                                                                                                                                                                                                                           パスワードに使用されるサイズ。                                                                                                                                                                                                                                                                                            |
|   64   |  4   |    圧縮     |        MBIM_COMPRESSION         |                                                                                                                                                                        データ接続でヘッダーとデータに使用する圧縮を指定します。 このメンバーは、GSM ベースのデバイスにのみ適用されます。 このメンバーは、CDMA ベースのデバイスの場合、ホストによって MBIMCompressionNone に設定されます。 詳細については、MBIM_COMPRESSION の表を参照してください。                                                                                                                                                                        |
|   68   |  4   |    AuthProtocol    |       MBIM_AUTH_PROTOCOL        |                                                                                                                                                                                                                                                  PDP のアクティブ化に使用する認証の種類。 詳細については、MBIM_AUTH_PROTOCOL の表を参照してください。                                                                                                                                                                                                                                                  |
|   72   |      |     DataBuffer     |           DATABUFFER            |                                                                                                                                                                                                                                                                     AccessString、UserName、および Password を含むデータバッファー。                                                                                                                                                                                                                                                                      |

##### <a name="notification"></a>通知

詳細については、MBIM_MS_PROVISIONED_CONTEXT_V2 の表を参照してください。

#### <a name="status-codes"></a>状態コード

クエリおよびセット操作の場合:

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | デバイスがプロビジョニングされたコンテキストを取得できなかったため、操作に失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスで操作がサポートされていないため、操作に失敗しました。 |

Set 操作のみ:

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーターのため、操作に失敗しました。 |
| MBIM_STATUS_WRITE_FAILURE | 更新要求が失敗したため、操作に失敗しました。 |


