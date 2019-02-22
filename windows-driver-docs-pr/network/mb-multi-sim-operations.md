---
title: MB マルチ SIM 操作
description: MB マルチ SIM 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ed574ad545900fa22d779253824d49c32d4205c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539423"
---
# <a name="mb-multi-sim-operations"></a>MB のマルチ SIM 操作

## <a name="desktop-multi-modem-multi-executor-support"></a>デスクトップのマルチ モデム マルチ Executor のサポート

これまでは、電話以外の Windows デバイスが構成されていないマルチ SIM モデムのフォンよりも少ない物理領域の制約があるためです。 これにより、スマート フォンと同様です。 複数の SIM カードのある 1 つのモデムではなく同時に複数のアクティブな無線を真に活用します。ただし、により、企業内 eSIM とシナリオの登場により、電話以外のデバイスでのマルチ SIM あたりモデム サポートの需要が増加しています。

最も一般的なマルチ SIM phone デバイスでは、デュアル SIM スロットがありますが、1 つプライマリ SIM カード サポート間データに他の唯一のサポート音声機能だけです。 このような制限は、データ接続のすべての SIM カードが使用されるために、電話以外の PC モデルにありません。

この仕様で定義されているフレームワークが、無制限の数のモデムと SIM カード、Windows 10 のサポート理論的にはバージョン 1703 以降デュアル SIM/単一アクティブ シナリオのエンド ツー エンドのみサポートしています。 

## <a name="ndis-modem-interface-specification"></a>NDIS モデム インターフェイスの仕様

### <a name="existing-interface-and-feature-gaps"></a>既存のインターフェイスと機能のギャップ

複数の独立したモデム、各モデムが、別のデバイスと、完全に独立して動作を使用してデュアル SIM デュアル アクティブ機能をサポートできるようになります。 ただし、代わりに、WWAN ミニポート モデムの倍数を表示できると同時に重点を置いたこのドキュメントのスコープ外は、ホストに移動体通信スタックです。 このセクションでは、さまざまなオブジェクトを定義し、マルチ SIM 機能に関連するすべての MB ドキュメントで使用される用語を確立します。

複数の移動体通信ネットワークで同時登録の管理できるデバイス ハードウェアの進歩が発生しました。 、このようなデバイスであると見なされます「移動体通信スタックの複数のインスタンス」は、それぞれの登録を管理することが並列で実行されている、信号の強度を監視、handovers を実行し、受信ページをリッスンします。 この「移動体通信スタック」の各インスタンスとして参照される、 *executor*このドキュメントの残りの部分。 たとえば、2 つのネットワークでの登録を同時に維持できるデバイスでは 2 つの executor がモデム ハードウェアと見なされます。

エグゼキュータがハードウェアと月の論理表現として実際に多重化されている 1 つの 1 つのハードウェア トランシーバーをします。 正確なハードウェアについては、ベンダーの実装の詳細とみなされていてはこの仕様の対象外です。 NDIS ミニポート ドライバーでは、executor は、WWAN ミニポート アダプターの複数のインスタンスとして公開されます。 MBIM モデムの場合は、executor は、列挙型の複合デバイス上の複数の MBIM 関数で表されます。

次の 2 つのイメージは、デュアル SIM モデムの論理ビューを示しています。 各 executor と UICC の考えられる組み合わせを示しています。

![デュアル SIM モデムの論理ビュー](images/multi-SIM_1_dualSimModem.png "デュアル SIM モデムの論理ビュー")

Executor 内で移動体通信スタックを自己完結型以外の場合は、executor のトラフィック (音声やデータ) を実行できない可能性があります、その他の登録を管理するデュアル スタンバイ モデム実装と見なされますほとんどの場合。

次の図は、デュアル スタンバイ モデムの論理ビューを示しています。 Executor 0 の場合、電話でのトラフィックは、登録が失われる Executor 1 とします。

![デュアル スタンバイ モデムの論理ビュー](images/multi-SIM_2_dualExecutors.png "デュアル スタンバイ モデムの論理ビュー")

NDIS 6.7 では、Windows デスクトップ モデム インターフェイス モデルでは、いくつかの暗黙的な前提条件に基づいているため、このようなアーキテクチャを対応していません。

* モデルでは、モデム内で 1 つの実行プログラムがあることを前提としています。
* モデルでは、1 つのモデム ハードウェアに直接関連付けられている UICC カードがあることを前提としています。
* UICC は、単一のアプリケーションの SIM カードの場合と同様に扱われます。

これに対し、Windows mobile、無線インターフェイス層 (RIL) インターフェイスでは、明示的にこのような想定の多重度を公開します。 Windows Mobile でモバイル ブロード バンド インターフェイスは、個別ミニポートを個別に登録する機能を公開し、RIL インターフェイスを通じて、デバイスのいくつかの基本的な構成を実現されていることを前提としています。 同等の機能を提供するには、Windows デスクトップが executor を個別にアクセスする、executor と、スロット間のマッピングを定義して、マップ内のアプリケーションを定義する executor とスロットの数を検出するメカニズムを提供する必要があります。各 executor で使用する UICC カード。

携帯電話のアーキテクチャと Windows 10 Mobile とデスクトップの違いの詳細についてを参照してください[携帯電話のアーキテクチャと実装](cellular-architecture-and-driver-model.md)します。

### <a name="major-objects-and-operations"></a>主なオブジェクトと操作

次の図は、モデムの抽象モデルを示します。

![モデム、Executor、スロットの関係](images/multi-SIM_3_majorObjectsAndOperations.png "モデム、Executor、スロットの関係")

各モデムは、グローバル一意識別子 (GUID) で識別され、それぞれが移動体通信ネットワーク上の独立した登録できる 1 つまたは複数の executor のセットが含まれています。 各 executor には、最初のエグゼキュータの 0 から始まる整数で、関連付けられている executor インデックスがあります。 さらに、モデムは UICC カードを含む可能性のある 1 つまたは複数のスロットを公開します。 スロットの数が executor の数以上であると見なされます。 各スロット、関連付けられているインデックスも先頭 0 を備え、スロットの電源の状態と、カードをスロット (あれば) の可用性の状態に関連して現在の状態。

既存のモデムとの互換性を維持するためには、各 executor は、1 つのスロットで UICC カードによって提供される情報で動作します。 Executor とスロット間の関連付けは、スロットのマッピングは、各 executor を正確に 1 つのスロットにマップによって定義されます。

スロットが UICC カード; を含めることができます。各カードには、1 つ以上の UICC アプリケーションなど、USIM、CSIM、ISIM、またはその他のテレフォニーと NFC のセキュリティで保護された要素の PKCS #15 またはグローバル プラットフォームのアプリケーションなどの非テレフォニー アプリケーションが含まれています。 アドレス指定とこれらの個々 の UICC アプリケーションの使用は、トピックの将来の仕様と、このドキュメントのスコープ外です。

Windows デスクトップの NDIS インターフェイスをモデムには、Oid と NDIS 通知の交換によって分類されます。 ほとんどの場合は、これらの Oid は個々 の executor; に送られますただし、いくつかのコマンドと通知は、モデムにスコープされます。

Windows モバイル オペレーティング システムでは、マルチ executor モデムは、複数の物理 WWAN ミニポート インスタンスで 1 つのデバイスとして表示されます。 各物理ミニポート インスタンスでは、NDIS インスタンスとしての登録を維持できる executor を表します。 実行時コンテキストに固有のパケット データとデバイスのサービスのセッションを管理するのには、追加の仮想インスタンスを作成できます。 WWAN ミニポート NDIS 物理インスタンスを通じてその実行プログラムを表すには、executor に固有のコマンドと通知が交換されます。 モデムに固有のコマンド (つまり、実行プログラムに固有ではないもの) と、対応する通知を送信または任意の物理ミニポート インスタンスに由来する可能性があります。

次の 2 つの図は、executor に固有のコマンドと通知 (最初の図)、コマンドと通知を通過し、同じ実行プログラム、およびモデムに固有のコマンドと通知 (2 番目の図) に由来の違いを示します、、コマンドが、executor を通過し、任意の実行プログラムから可能性があります。

![エグゼキュータに固有のコマンドと通知](images/multi-SIM_4_executorSpecificCommands.png "Executor に固有のコマンドと通知")

![モデムに固有のコマンドと通知](images/multi-SIM_4_modemSpecificCommands.png "モデムに固有のコマンドと通知")

すべての OID セットまたはクエリ ミニポート インスタンスに発行された要求は、モデムおよびミニポートのインスタンスが関連付けられている executor に対して実行されます。 同様に、すべての要請されていない通知およびミニポート インスタンスから送信された要請されていないデバイスのサービス イベントでは、モデムおよびミニポートのインスタンスが関連付けられている executor に適用します。 たとえば、ミニポートからの要請していない NDIS_STATUS_WWAN_REGISTER_STATE または NDIS_STATUS_WWAN_PACKET_SERVICE 通知は、関連付けられているモデムと executor をのみの登録 (またはパケット サービスの状態) を示しの状態とは関係ありません。他のモデムまたはその他の executor(s) します。 

複数のモデムまたはデバイスに複数の executor がある場合は、物理ミニポート アダプターに関連付けられているモデムと executor の組み合わせが特定のモデムと executor に関連するコンテキストに固有の要請していない通知を発行します。組み合わせ。 

同様に、複数のモデムや複数の実行プログラムは、デバイスがある場合、特定のモデムと executor の組み合わせに関連付けられている物理ミニポート アダプター インスタンス要求を受信できるコンテキスト固有 OID クエリそのモデムと executor に関連します。 このようなクエリ要求の受信アダプターは、OID の定義に従って処理します。 ミニポート ドライバーによって選択された場合は、他のプロセスで OID セットまたはアダプターのすべてのインスタンス内の要求は、そのモデムと executor に関連付けられているクエリと同時クエリ要求を処理できます。 同じモデムとエグゼキュータに関連付けられているミニポート アダプターのすべてのインスタンスは、携帯電話のモデムと executor (ラジオ電源の状態、登録の状態、パケットのサービスの状態など) などの同じ状態情報を報告します。  

複数のモデムや複数の executor のあるデバイス、モデムと executor の組み合わせに関連付けられている物理ミニポート アダプター インスタンスはコンテキストに固有の OID のセット要求を受け取ることができます。 ミニポート ドライバーはの追跡、このような要求の進行状況。 このようなセットの 1 つの要求が進行中のすべてのアダプターとがまだ完了して、このような 2 つ目のセットがある場合 (同じモデムとエグゼキュータに関連付けられているアダプター インスタンスは任意) を試行中の要求をキューに以前の要求が完了した後に処理されます。 

このセットの要求の競合状態を処理するために、前の段落で説明されている仕様に準拠して、Windows 10 デスクトップ WMBCLASS ドライバーが、モデムのレイヤーで競合状態が発生した場合、モデムがキューに競合している同じガイダンスに従う必要があります。MBIM 関数場合は、同じ基になるデバイスにリンクされている別の関数を処理中にデバイス全体にわたるコマンド。

## <a name="oids-for-set-and-query-requests"></a>セットとクエリ要求の oid です。

デバイス (実行プログラム) とモデムのスロットの数と同時にアクティブにできる executor の数を照会するには、ホストが使用して[OID_WWAN_SYS_CAPS](https://go.microsoft.com/fwlink/p/?linkid=841265)します。

ホストが使用するには、executor の機能を照会するには、 [OID_WWAN_DEVICE_CAPS_EX](https://go.microsoft.com/fwlink/p/?linkid=841266)します。

ホストが使用するには、各 executor または現在のマッピングをクエリにバインドされているスロットを定義するには、 [OID_WWAN_DEVICE_SLOT_MAPPINGS](https://go.microsoft.com/fwlink/p/?linkid=841267)します。

ホストが使用するには、モデムの特定のスロットの状態を照会するには、 [OID_WWAN_SLOT_INFO_STATUS](https://go.microsoft.com/fwlink/p/?linkid=841268)します。

## <a name="per-device-and-per-executor-commands"></a>デバイス数と executor あたりのコマンド

Executor の概念を Windows 10 バージョン 1703 以降で非 Windows モバイル デバイスの追加 Oid はこれで 2 つのカテゴリに分割します。 デバイスごとの Oid と executor あたりの Oid。 次の表では、Oid がどのカテゴリに分類するについて説明します。

| デバイスごとまたは実行プログラムあたり| OID の名前 |
| --- | --- |
| デバイス数| OID_WWAN_DRIVER_CAPS |
|  | OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS |
|  | OID_WWAN_ENUMERATE_DEVICE_SERVICES |
|  | OID_WWAN_PRESHUTDOWN |
|  | OID_WWAN_VENDOR_SPECIFIC |
|  | OID_WWAN_SYS_CAPS |
|  | OID_WWAN_DEVICE_SLOT_MAPPINGS |
| 実行プログラムあたり | OID_WWAN_AUTH_CHALLENGE |
|  | OID_WWAN_CONNECT |
|  | OID_WWAN_DEVICE_CAPS |
|  | OID_WWAN_DEVICE_CAPS_EX |
|  | OID_WWAN_DEVICE_SERVICE_COMMAND |
|  | OID_WWAN_DEVICE_SERVICE_SESSION |
|  | OID_WWAN_DEVICE_SERVICE_SESSION_WRITE |
|  | OID_WWAN_DEVICE_SERVICES |
|  | OID_WWAN_HOME_PROVIDER |
|  | OID_WWAN_NETWORK_IDLE_HINT |
|  | OID_WWAN_PACKET_SERVICE |
|  | OID_WWAN_PIN |
|  | OID_WWAN_PIN_EX |
|  | OID_WWAN_PIN_LIST |
|  | OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS |
|  | OID_WWAN_PREFERRED_PROVIDERS |
|  | OID_WWAN_PROVISIONED_CONTEXTS |
|  | OID_WWAN_RADIO_STATE |
|  | OID_WWAN_READY_INFO |
|  | OID_WWAN_REGISTER_STATE |
|  | OID_WWAN_SERVICE_ACTIVATION |
|  | OID_WWAN_SIGNAL_STATE |
|  | OID_WWAN_SMS_CONFIGURATION |
|  | OID_WWAN_SMS_DELETE |
|  | OID_WWAN_SMS_READ |
|  | OID_WWAN_SMS_SEND |
|  | OID_WWAN_SMS_STATUS |
|  | OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS |
|  | OID_WWAN_USSD |
|  | OID_WWAN_VISIBLE_PROVIDERS |
|  | OID_WWAN_SLOT_INFO_STATUS |

> [!NOTE]
> [OID_WWAN_RADIO_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569832)の Windows 10 バージョン 1703 も更新されました。 詳細については、OID_WWAN_RADIO_STATE を参照してください。

## <a name="mbim-interface-update-for-multi-sim-operations"></a>MBIM インターフェイスの更新プログラムのマルチ SIM 操作

Windows モバイル オペレーティング システムでは、マルチ executor モデムは、複数の MBIM 関数と 1 つの USB 複合デバイスとして表示されます。 各 MBIM 関数は、登録を維持できる executor を表します。 Executor に固有のコマンドと通知がモデムに固有のコマンド (つまり、実行プログラムに固有ではないもの) の中に、その実行プログラムを表す MBIM 関数経由で交換されると、対応する通知を送信または付属する可能性があります。同じ基になる USB 複合デバイスが属する MBIM 関数。 

すべての CID セットまたはクエリ MBIM 関数に発行された要求は、モデムおよびミニポートのインスタンスが関連付けられている executor に対して実行されます。同様に、MBIM 関数から送信されるすべての不要な通知は、モデムおよび MBIM 関数が関連付けられている executor に適用されます。 同様に、ミニポート インスタンスから送信されたすべての要請されていないデバイスのサービス イベントは、モデムおよび MBIM 関数が関連付けられている executor に適用されます。 たとえば、MBIM 関数からの要請していない MBIM_CID_REGISTER_STATE または MBIM_CID_PACKET_SERVICE 通知は、関連付けられているモデム/エグゼキュータのみの登録またはパケットのサービスの状態を示しは他のモデムの状態に関連付けられていない、またはその他のexecutor(s) します。 

複数のモデムまたはデバイスに複数の executor コンテキストに固有の不要な通知に関連する特定のモデムと executor の組み合わせは、前述のモデムに関連付けられている MBIM 関数から発行されているものとし、実行プログラム。 

複数のモデムや複数の executor と、デバイスでこのモデムと executor の組み合わせに関連付けられている MBIM 関数にコンテキスト固有 CID のクエリ要求に関連する特定のモデムと executor を発行できます。 このようなクエリ要求の受信関数を CID の定義に従って処理されます。 その他の同時モデムのファームウェア、このようなクエリ要求によって選択を処理する可能性がありますので場合は、CID を設定またはクエリは、そのモデムとエグゼキュータに関連付けられているすべての MBIM 関数によって処理される要求。 同じモデムに関連付けられているすべての MBIM 関数では、executor 表しているだけでなく携帯電話をモデムの同じ状態情報が報告されます。  

複数のモデムまたはデバイスに複数の executor がある場合は、そのモデムとエグゼキュータに関連付けられている MBIM 関数に executor 固有 CID セット要求を発行する場合があります。 モデムはの追跡、全体としては、このような要求の進行状況。 このようなセットの 1 つの要求が進行中のすべてのアダプターとがまだ完了して、このような 2 つ目のセットがある場合 (同じモデムとエグゼキュータに関連付けられているアダプター インスタンスは任意) を試行中の要求をキューに、以前の要求が完了した後に処理されます。

次の図は、2 つのさまざまなモデムで WWANSVC と MBIM 関数の間で情報の流れを示しています。

![MBIM 関数を使用した構造をモデム](images/multi-SIM_10_MBIMspecification.png "MBIM 関数を使用した構造のモデム")

このセクションには、定義済みのデバイスのサービスの詳細なモデム全体に適用され、executor あたり CID の説明が含まれています。 既存のパブリック MBIM1.0 仕様に定義の参照。 MBIM 準拠のデバイスでは、実装し、CID_MBIM_DEVICE_SERVICES によりクエリを実行すると、次のデバイス サービスを報告します。 既存の既知のサービスは、USB NCM MBIM 1.0 仕様のセクション 10.1 で定義されます。 Microsoft は、これを次のサービスの定義を拡張します。

サービス名 = **Basic 拡張機能の接続**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 値 = **3d01dcc5 fef5-4 d 05-0d3abef7058e9aaf**

次の Cid が定義されている**UUID_MS_BasicConnect**:

| CID | コマンド コード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_MS_SYS_CAPS | 5 | Windows 10 Version 1703 |
| MBIM_CID_MS_DEVICE_CAPS_V2 | 6 | Windows 10 Version 1703 |
| MBIM_CID_MS_DEVICE_SLOT_MAPPINGS | 7 | Windows 10 Version 1703 |
| MBIM_CID_MS_SLOT_INFO_STATUS | 8 | Windows 10 Version 1703 |

InformationBuffer MBIM_COMMAND_MSG の先頭からは、次の CID のセクションでは、すべてのオフセットが計算されます。

### <a name="mbimcidmssyscaps"></a>MBIM_CID_MS_SYS_CAPS

#### <a name="description"></a>説明

この CID は、モデムの情報を取得します。 これは、USB 関数として公開 MB インスタンスのいずれかに送信できます。

##### <a name="query"></a>クエリ

MBIM_COMMAND_MSG で InformationBuffer には、MBIM_MS_SYS_CAPS_INFO として応答データが含まれています。

##### <a name="set"></a>設定

適用できません。

##### <a name="unsolicited-event"></a>要請されていないイベント

適用できません。

#### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | 該当なし | 該当なし |
| 応答 | 該当なし | MBIM_MS_SYS_CAPS_INFO | 該当なし |

#### <a name="data-structures"></a>データ構造体

##### <a name="query"></a>クエリ

InformationBuffer は null にして、InformationBufferLength を 0 にする必要があります。

##### <a name="set"></a>設定

適用できません。

##### <a name="response"></a>応答

次の MBIM_SYS_CAPS_INFO 構造、InformationBuffer で使用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NumberOfExecutors | UINT32 | このモデムによって報告された MBB インスタンスの数 |
| 4 | 4 | NumberOfSlots | UINT32 | このモデムで利用可能な物理の UICC スロットの数 |
| 8 | 4 | 同時実行 | UINT32 | 同時にアクティブにできる MBB インスタンスの数 |
| 12 | 8 | ModemId | UINT64 | 各モデムの 64 ビット一意識別子 |

*NumberOfExecutors*フィールドの数を表しています*executor*現在の構成でモデムでサポートされています。 これは、モデムがサポートする 'サブ電話' スタックの数に直接マップされます。 

*NumberofSlots*フィールドは、モデムに物理的に存在するスロットの数を示します。 報告された各スロット UICC カード (スロット自体は、異種混在 – ミニ SIM、micro SIM、nano SIM または ETSI で定義されている任意の標準が必要な場合を指定できます) を受信できる必要があります。 スロットの数は、サポートされる executor の数以上である必要があります。 'より大きい' のプロビジョニングが使用できるように、NFC、セキュリティなどの非テレフォニー UICC など。

*同時実行*フィールドは同時にアクティブな可能性がある (MBB インスタンス) の executor の数を示します。 これは、範囲である必要があります*1 ≤ 同時実行 ≤ NumberOfExecutors*します。 たとえば、デュアル スタンバイ モデムは 1 の同時実行性にがデュアル アクティブ モデムは 2 の同時実行性

*ModemId*フィールドが特定のモデム ハードウェアの一意の 64 ビットの識別子を表します。 IHV は、各モデムの一意の 64 ビット値を生成する、独自のロジックを実装できます。たとえば、64 ビットの番号などのランダムに生成、IMEI 番号のいずれかをハッシュします。64 ビットの ID が生成されるは、再起動や SIM カードの削除/挿入の間で保持する必要があります。

#### <a name="status-codes"></a>状態コード

この CID は汎用のステータス コードを使用して (の 9.4. 5. のセクションでは状態コードの使用を参照してください。[パブリック USB MBIM 標準](https://go.microsoft.com/fwlink/p/?linkid=842064))。

### <a name="mbimcidmsdevicecapsv2"></a>MBIM_CID_MS_DEVICE_CAPS_V2

#### <a name="description"></a>説明

この CID executor に関連する機能の情報を取得します。 この CID が MBIM_CID_DEVICE_CAPS の拡張機能であるため、ここから MBIM_CID_DEVICE_CAPS 標準 USB MBIM 公開の 10.5.1 のセクションで説明したように変更のみに表示されます。

この CID が引き続きクエリ専用にして、MBIM_MS_DEVICE_CAPS_INFO_V2 が返されます、MBIM で MBIM_COMMAND_MSG への応答の構造体サービス MSUUID_BASIC_CONNECT と CID MBIM_CID_MS_DEVICE_CAPS_V2 します。

#### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | 該当なし | 該当なし |
| 応答 | 該当なし | MBIM_MS_DEVICE_CAPS_INFO_V2 | 該当なし |

#### <a name="data-structures"></a>データ構造体

##### <a name="query"></a>クエリ

10.5.1.4 USB MBIM 標準のパブリックのと同じです。

##### <a name="set"></a>設定

適用できません。

##### <a name="response"></a>応答

次の MBIM_DEVICE_CAPS_INFO_V2 構造、InformationBuffer で使用されます。 パブリックの USB MBIM 標準の 10.5.1 で定義されている MBIM_CID_DEVICE_CAPS 構造と比べると、次の構造がという名前の新しいフィールド*DeviceIndex*します。 ここで説明すると、しない限り、標準の USB MBIM 公開の 10 ~ 14 でフィールドの説明はここに適用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | DeviceType | MBIM_DEVICE_TYPE |  |
| 4 | 4 | CellularClass | MBIM_CELLULAR_CLASS |  |
| 8 | 4 | VoiceClass | MBIM_VOICE_CLASS |  |
| 12 | 4 | SimClass | MBIM_SIM_CLASS | この CID をサポートする MBIM モデム、SimClass は常に MBIMSimClassSimRemovable として報告されます。 |
| 16 | 4 | dataClass | MBIM_DATA_CLASS |  |
| 20 | 4 | SmsCaps | MBIM_SMS_CAPS |  |
| 24 | 4 | ControlCaps | MBIM_CTRL_CAPS |  |
| 28 | 4 | MaxSessions | UINT32 |  |
| 32 | 4 | CustomDataClassOffset | オフセット |  |
| 36 | 4 | CustomDataClassSize | SIZE(0..22) |  |
| 40 | 4 | DeviceIdOffset | オフセット |  |
| 44 | 4 | DeviceIdSize | SIZE(0..26) |  |
| 48 | 4 | FirmwareInfoOffset | オフセット |  |
| 52 | 4 | FirmwareInfoSize | SIZE(0..60) |  |
| 56 | 4 | HardwareInfoOffset | オフセット |  |
| 60 | 4 | HardwareInfoSize | SIZE(0..60) |  |
| 64| 4 | ExecutorIndex | UINT32 | Executor のインデックス。 これは、範囲から*0*に*n-1*場所*n* MBIM モデムに含まれている MBB インスタンスの数です。 その値は、定数と列挙順序に関係なく常にします。 |
| 68 |  | DataBuffer | DATABUFFER | データ バッファーを含む、 *CustomDataClass*、 *DeviceId*、 *FirmwareInfo*、および*HardwareInfo*メンバー。 |

#### <a name="status-codes"></a>状態コード

この CID は、汎用の状態コード (標準パブリック USB MBIM の 9.4. 5. のセクションではステータス コードの使用を参照してください) を使用します。

### <a name="mbimcidmsdeviceslotmappings"></a>MBIM_CID_MS_DEVICE_SLOT_MAPPINGS

#### <a name="description"></a>説明

この CID を設定またはデバイスのスロットのマッピング (つまり、executor スロット マッピング) を返します。

##### <a name="query"></a>クエリ

MBIM_COMMAND_MSG で InformationBuffer は使用されません。 MBIM_COMMAND_DONE の InformationBuffer MBIM_MS_DEVICE_SLOT_MAPPING_INFO が返されます。

##### <a name="set"></a>設定

MBIM_COMMAND_MSG InformationBuffer には MBIM_MS_DEVICE_SLOT_MAPPING_INFO が含まれています。 MBIM_COMMAND_DONE の InformationBuffer MBIM_MS_DEVICE_SLOT_MAPPING_INFO が返されます。 設定 CID が成功したか失敗したかに関係なく、応答に含まれている MBIM_MS_DEVICE_SLOT_MAPPING_INFO は現在のデバイスのスロットのマッピングを表します。

##### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

#### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | 該当なし | 該当なし |
| 応答 | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | 該当なし |

#### <a name="data-structures"></a>データ構造体

##### <a name="query"></a>クエリ

InformationBuffer は null にして、InformationBufferLength を 0 にする必要があります。

##### <a name="set"></a>設定

次の MBIM_MS_DEVICE_SLOT_MAPPING_INFO 構造、InformationBuffer で使用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | MapCount (MC) | UINT32 | デバイス/executor の数と等しくは常に、マッピングの数。 |
| 4 | 8 * MC | SlotMapList | OL_PAIR_LIST | *I*ペアは、この一覧の場所 (0 < = i < = (MC 1)) に現在マップされているスロットのインデックスを記録、 *i*デバイス/実行プログラム。 ペアの最初の要素は、計算されるこの MBIM_MS_DEVICE_SLOT_MAPPINGS_INFO 構造体の先頭 (オフセット 0) から、UINT32 へ、DataBuffer にオフセットを含む 4 バイト フィールドです。 ペアの 2 番目の要素は、レコード要素のサイズが 4 バイトです。 スロット インデックスの種類は、UINT32 であるため、ペアの 2 番目の要素は常に 4 にです。 |
| 4 + (8 * MC) | 4 * MC | DataBuffer | DATABUFFER | データ バッファーを含む*SlotMapList*します。 DataBuffer の合計サイズが 4 でスロットのサイズは 4 バイトであり、MC はスロット インデックスの数と等しく、ため * MC します。 |

##### <a name="response"></a>応答

セットで使用される MBIM_MS_DEVICE_SLOT_MAPPING_INFO は、応答、InformationBuffer でも使用されます。

#### <a name="status-codes"></a>状態コード

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_BUSY | デバイスがビジー状態、操作が失敗しました。 この状態をクリアする関数からの明示的な情報がない場合は、ホストを使用できます、後続のアクション (通知やコマンドの入力候補など)、関数によってヒントとして、失敗した操作を再試行してください。 |
| MBIM_STATUS_FAILURE | 操作には、(一般的なエラー) が失敗しました。 |
| MBIM_STATUS_VOICE_CALL_IN_PROGRESS | 音声通話が進行中のため、操作が失敗しました。 |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーター (マッピングに重複する値または範囲外のスロット番号など) ため、操作が失敗しました。 |

### <a name="mbimcidmsslotinfostatus"></a>MBIM_CID_MS_SLOT_INFO_STATUS

#### <a name="description"></a>説明

この CID は、指定された UICC スロットおよび (指定されている場合) 内でカードの高度な集計された状態を取得します。 スロットのいずれかの状態が変更されたときに、請求の通知を配信するも使用可能性があります。

##### <a name="query"></a>クエリ

MBIM_COMMAND_MSG InformationBuffer には MBIM_MS_SLOT_INFO_REQ 構造体が含まれています。 MBIM_COMMAND_DONE メッセージの InformationBuffer には MBIM_MS_SLOT_INFO 構造体が含まれています。

##### <a name="set"></a>設定

適用できません。

##### <a name="unsolicited-events"></a>要請されていないイベント

イベント InformationBuffer には MBIM_MS_SLOT_INFO 構造体が含まれています。 関数は、イベントで複合スロット/カードの状態の変更に、このイベントを送信します。

#### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | MBIM_MS_SLOT_INFO_REQ | 該当なし |
| 応答 | 該当なし | MBIM_MS_SLOT_INFO | MBIM_MS_SLOT_INFO |

#### <a name="data-structures"></a>データ構造体

##### <a name="query"></a>クエリ

次の MBIM_MS_SLOT_INFO_REQ 構造、InformationBuffer で使用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SlotIndex | UINT32 | クエリを実行するスロットのインデックス。 |

##### <a name="set"></a>設定

適用できません。

##### <a name="response"></a>応答

次の MBIM_MS_SLOT_INFO 構造、InformationBuffer で使用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SlotIndex | UINT32 | スロットのインデックス。 |
| 4 | 4 | 状態 | MBIM_MS_UICC_SLOT_STATE | カード (該当する) 場合、スロットの状態。 |

次の MBIM_MS_UICCSLOT_STATE 構造では、スロットの可能な状態について説明します。

| 状態 | Value | 説明 |
| --- | --- | --- |
| UICCSlotStateUnknown | 0 | モデムは、SIM スロットの状態が明確ではありませんのでを初期化中には、まだです。 |
| UICCSlotStateOffEmpty | 1 | UICC スロットは電源がオフとカードが存在しません。 電源がオフのスロットでカードの有無を確認することはない実装 UICCSlotStateOff の状態を報告します。 |
| UICCSlotStateOff | 2 | UICC スロットの電源がオフにします。 |
| UICCSlotStateEmpty | 3 | UICC スロットが空 (カードがないが)。 |
| UICCSlotStateNotReady | 4 | UICC スロットが占有されているし、電源をオンにしますが、その中のカードがまだできていません。 |
| UICCSlotStateActive | 5 | UICC スロットを占有され、その中のカードが整います。 |
| UICCSlotStateError | 6 | UICC スロットが占有されている、電源が入ってが、カードがエラー状態と、次にリセットされるまでは使用できません。 |
| UICCSlotStateActiveEsim | 7 | カードをスロットに、アクティブなプロファイルで、esim 状でありコマンドも受け入れるようになります。 |
| UICCSlotStateActiveEsimNoProfiles | 8 | カードをスロットにプロファイルがありません (またはアクティブなプロファイルがありません)、esim 状でありコマンドも受け入れるようになります。 |

#### <a name="status-codes"></a>状態コード

この CID は、汎用の状態コード (標準パブリック USB MBIM の 9.4. 5. のセクションではステータス コードの使用を参照してください) を使用します。

### <a name="non-ndis-mapping-of-per-executor-and-per-modem-mbim-cids"></a>実行プログラムあたりとモデムの MBIM Cid の NDIS 以外のマッピング

MBIM Cid のほとんどは、マップまたは NDIS の Oid に関係があるいくつかのコマンド Windows WMB クラス ドライバーによって使用される、NDIS 対応がないです。  このセクションでは、これらのコマンドがモデムごとまたは executor あたりのかどうかをわかりやすくするためを提供します。  

| デバイスごとまたは実行プログラムあたり | CID 名 |
| --- | --- |
| デバイス数 | CID_MBIM_MSEMERGENCYMODE |
|  | CID_MBIM_MSHOSTSHUTDOWN |
| 実行プログラムあたり | CID_MBIM_MSIPADDRESSINFO |
|  | CID_MBIM_MSNETWORKIDLEHINT |
|  | CID_MBIM_MULTICARRIER_CURRENT_CID_LIST |

