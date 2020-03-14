---
title: MB マルチ SIM 操作
description: MB マルチ SIM 操作
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: ec3f386758f6a241f78f09f4b94f3f8085ab7095
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79243025"
---
# <a name="mb-multi-sim-operations"></a>MB のマルチ SIM 操作

## <a name="desktop-multi-modem-multi-executor-support"></a>デスクトップマルチモデムマルチ実行プログラムのサポート

従来、スマートフォン以外の Windows デバイスは、電話よりも物理的な領域の制約が少なくなっているため、マルチ SIM モデム用に構成されていません。 これにより、電話のような複数の SIM カードでモデムを使用する代わりに、複数のアクティブなラジオを同時に使用することができます。ただし、企業の eSIM とシナリオが増加しているため、非電話デバイスでのモデムごとのマルチ SIM サポートの需要が高まっています。

ほとんどの一般的な sim スロットにはデュアル SIM スロットがありますが、1つのプライマリ SIM カードに制限されていますが、他のデバイスは音声機能のみをサポートしています。 このような制限は、すべての SIM カードがデータ接続に使用されるため、非電話 PC モデルには存在しません。

この仕様で定義されているフレームワークは、理論的には無制限の数のモデムと SIM カードをサポートしていますが、Windows 10、バージョン1703以降では、デュアル SIM/シングルアクティブシナリオのみがサポートされます。 

## <a name="ndis-modem-interface-specification"></a>NDIS モデムインターフェイスの仕様

### <a name="existing-interface-and-feature-gaps"></a>既存のインターフェイスと機能のギャップ

複数の独立したモデムを使用して、デュアル SIM/デュアルアクティブ機能をサポートできます。各モデムは独立したデバイスで、完全に独立して動作します。 ただし、これはこのドキュメントの範囲外です。代わりに、複数の同時移動体をホストに提示できる WWAN ミニポートモデムに焦点を当てています。 このセクションでは、さまざまなオブジェクトを定義し、マルチ SIM 機能に関連するすべての MB ドキュメントで使用される用語を確立します。

ハードウェアの進歩によって、複数の携帯ネットワークに同時に登録できるデバイスが作成されました。 このようなデバイスでは、"携帯ネットワークスタックの複数のインスタンス" が並行して実行されていると想定されています。これは、登録の管理、シグナルの強さの監視、handovers の実行、および受信ページのリッスンを行うことができます。 この "携帯電話スタック" の各インスタンスは、このドキュメントの残りの部分の実行*プログラム*と呼ばれます。 たとえば、2つのネットワークへの登録を同時に維持することができるデバイスでは、モデムハードウェアは2つの実行プログラムを持つと見なされます。

実行プログラムはハードウェアの論理的な表現であり、1つのハードウェアトランシーバーが多重化されている場合があります。 正確なハードウェアの仕様はベンダーの実装の詳細と見なされ、この仕様の範囲外です。 NDIS ミニポートドライバーの場合、エグゼキュータは、WWAN ミニポートアダプターの複数のインスタンスとして公開されます。 MBIM モデムの場合、エグゼキュータは列挙された複合デバイス上の複数の MBIM 関数によって表されます。

次の2つのイメージは、デュアル SIM モデムの論理ビューを示しています。 各は、実行プログラムと UICC の組み合わせを示しています。

![デュアル SIM モデムの論理ビュー](images/multi-SIM_1_dualSimModem.png "デュアル SIM モデムの論理ビュー")

実行プログラム内の移動体は、通常、自己完結したものと見なされます。ただし、トラフィック (音声やデータ) を実行している実行プログラムによって、他のユーザーが登録を維持できないようなデュアルスタンバイモデムの実装の場合を除きます。

次の図は、デュアルスタンバイモデムの論理ビューを示しています。 実行プログラム 0 (電話呼び出し) のトラフィックによって、実行プログラム1の登録が失われます。

![デュアルスタンバイモデムの論理ビュー](images/multi-SIM_2_dualExecutors.png "デュアルスタンバイモデムの論理ビュー")

NDIS 6.7 の Windows デスクトップモデムインターフェイスモデルは、いくつかの暗黙的な仮定に基づいているため、このようなアーキテクチャには対応していません。

* このモデルでは、モデム内に実行プログラムが1つあることを前提としています。
* このモデルでは、直接モデムハードウェアに関連付けられている単一の UICC カードがあることを前提としています。
* UICC は、単一アプリケーションの SIM カードであるかのように扱われます。

これに対し、Windows Mobile の Microsoft Radio Interface Layer (RIL) インターフェイスでは、これらの仮定の多重度が明示的に公開されます。 Windows Mobile のモバイルブロードバンドインターフェイスでは、個別のミニポートを使用して個別に登録する機能が公開されており、デバイスの一部の基本的な構成は、RIL インターフェイスによって既に実行されていることを前提としています。 同等の機能を提供するために、Windows デスクトップは、エグゼキュータとスロットの数を検出し、エグゼキュータに個別にアクセスするためのメカニズムを提供する必要があります。また、エグゼキュータとスロット間のマッピングを定義し、マップ内のアプリケーションを定義します。各実行プログラムが使用する UICC カード。

携帯ネットワークのアーキテクチャと Windows 10 Mobile とデスクトップの違いの詳細については、「[携帯ネットワークのアーキテクチャと実装](cellular-architecture-and-driver-model.md)」を参照してください。

### <a name="major-objects-and-operations"></a>主要なオブジェクトと操作

次の図は、モデムの抽象モデルを示しています。

![モデム、エグゼキュータ、スロットの関係](images/multi-SIM_3_majorObjectsAndOperations.png "モデム、エグゼキュータ、スロットの関係")

各モデムは、グローバル一意識別子 (GUID) によって識別され、1つまたは複数のエグゼキュータのセットを含みます。これらはそれぞれ、携帯ネットワークに個別に登録できます。 各実行プログラムには、最初の実行プログラムに対して0から始まる、関連付けられた実行プログラムインデックスがあります。 また、モデムは、UICC カードを含む可能性のある1つ以上のスロットを公開します。 これは、スロットの数がエグゼキュータの数以上であることを前提としています。 各スロットには、0から始まるインデックスが関連付けられており、スロットの電源状態とスロットのカード (存在する場合) の状態に関連する現在の状態があります。

既存のモデムとの互換性を維持するために、各実行プログラムは、1つのスロットの UICC カードによって提供される情報を操作します。 実行プログラムとスロット間の関連付けはスロットマッピングによって定義されます。これにより、各実行プログラムが1つのスロットにマップされます。

スロットには UICC カードを含めることができます。各カードには、USIM、CSIM、ISIM、または他のテレフォニーおよびテレフォニー以外のアプリケーション (PKCS # 15、NFC secure 要素用のグローバルプラットフォームアプリケーションなど) が含まれています。 これらの個々の UICC アプリケーションのアドレス指定と使用は、今後の仕様に関するトピックであり、このドキュメントの範囲外です。

モデムへの Windows デスクトップ NDIS インターフェイスは、Oid と NDIS 通知の交換によって特徴付けられています。 ほとんどの場合、これらの Oid は個々のエグゼキュータに送られます。ただし、いくつかのコマンドと通知がモデムに限定されています。

Windows 以外のモバイルオペレーティングシステムでは、複数の物理 WWAN ミニポートインスタンスを持つ1つのデバイスとしてマルチ実行プログラムのモデムが表示されます。 各物理ミニポートインスタンスは、NDIS インスタンスとして登録を維持できる実行プログラムを表します。 コンテキスト固有のパケットデータとデバイスサービスセッションを管理するために、実行時に追加の仮想インスタンスを作成することができます。 実行プログラム固有のコマンドと通知は、その実行プログラムを表す WWAN ミニポート NDIS 物理インスタンスを介して交換されます。 モデム固有のコマンド (実行プログラム固有ではないコマンド) とそれに対応する通知は、物理ミニポートインスタンスに送信されるか、または任意の物理ミニポートインスタンスから送信されることがあります。

次の2つの図は、実行プログラム固有のコマンドと通知 (最初の図) の違いを示しています。ここでは、コマンドと通知を実行し、同じ実行プログラムと、モデム固有のコマンドと通知 (2 番目の図) を使用します。コマンドは任意の実行プログラムを通過し、任意の実行プログラムから取得できます。

![実行プログラム固有のコマンドと通知](images/multi-SIM_4_executorSpecificCommands.png "実行プログラム固有のコマンドと通知")

![モデム固有のコマンドと通知](images/multi-SIM_4_modemSpecificCommands.png "モデム固有のコマンドと通知")

ミニポートインスタンスに対して発行されたすべての OID セットまたはクエリ要求は、ミニポートインスタンスが関連付けられているモデムと実行プログラムに対して実行されます。 同様に、ミニポートインスタンスから送信されたすべての要請されていない通知および要請されていないデバイスサービスイベントは、モデムおよびミニポートインスタンスが関連付けられている実行プログラムに適用されます。 たとえば、ミニポートからの要請されていない NDIS_STATUS_WWAN_REGISTER_STATE または NDIS_STATUS_WWAN_PACKET_SERVICE 通知は、関連付けられているモデムと実行プログラムの登録 (またはパケットサービスの状態) を示します。これは、次の状態には関係ありません。他のモデムまたはその他の実行プログラム。 

1つのデバイスに複数のモデムまたは複数の実行プログラムがある場合、そのモデムと実行プログラムの組み合わせに関連付けられている物理ミニポートアダプターは、特定のモデムと実行プログラムの組み合わせに関連する、非状況依存の非要請通知を発行します。 

同様に、デバイスに複数のモデムまたは複数の実行プログラムがある場合、特定のモデムおよび実行プログラムの組み合わせに関連付けられている物理ミニポートアダプターのインスタンスは、そのモデムおよび実行プログラムに関連する、非状況依存の OID クエリ要求を受け取ることができます。 このようなクエリ要求を受信するアダプターは、OID 定義に従って処理します。 ミニポートドライバーによって選択された場合、このクエリ要求は、そのモデムと実行プログラムに関連付けられているアダプターの任意のインスタンス内の他のすべてのインプロセス OID セットまたはクエリ要求と同時に処理できます。 同じモデムおよび実行プログラムに関連付けられているミニポートアダプターのすべてのインスタンスは、その携帯電話と実行プログラム (無線電源状態、登録状態、パケットサービスの状態など) について同じ状態情報を報告します。  

複数のモデムまたは複数の実行プログラムがあるデバイスの場合、モデムと実行プログラムの組み合わせに関連付けられている物理ミニポートアダプターインスタンスは、非コンテキスト固有の OID セット要求を受け取ることができます。 ミニポートドライバーは、このような要求の進行状況を追跡します。 このようなセット要求がいずれかのアダプターで進行中で、まだ完了していない場合は、そのようなセット要求の試行 (同じモデムおよび実行プログラムに関連付けられているアダプターインスタンスへの要求) が、前の要求が完了した後にキューに登録され、処理される必要があります。 

Windows 10 desktop WMBCLASS ドライバーは、前の段落に記載されている仕様に従ってこのセット要求の競合状態を処理しますが、モデムレイヤーで競合状態が発生した場合、モデムは同じガイダンスに従って競合をキューに入れます。同じ基になるデバイスにリンクされている別の関数がまだ処理されている場合の、MBIM 関数でのデバイス全体のコマンド。

## <a name="oids-for-set-and-query-requests"></a>Set 要求とクエリ要求の Oid

モデム内のデバイス (実行プログラム) とスロットの数、および同時にアクティブになる可能性がある実行プログラムの数を照会するために、ホストは[OID_WWAN_SYS_CAPS](https://go.microsoft.com/fwlink/p/?linkid=841265)を使用します。

実行プログラムの機能を照会するために、ホストは[OID_WWAN_DEVICE_CAPS_EX](https://go.microsoft.com/fwlink/p/?linkid=841266)を使用します。

各実行プログラムにバインドされるスロットを定義したり、現在のマッピングに対してクエリを実行したりするために、ホストは[OID_WWAN_DEVICE_SLOT_MAPPINGS](https://go.microsoft.com/fwlink/p/?linkid=841267)を使用します。

モデムの特定のスロットの状態を照会するために、ホストは[OID_WWAN_SLOT_INFO_STATUS](https://go.microsoft.com/fwlink/p/?linkid=841268)を使用します。

## <a name="per-device-and-per-executor-commands"></a>デバイスごとのコマンドと実行プログラムごとのコマンド

Windows 10 バージョン1703以降では、windows 以外のモバイルデバイスに対して実行プログラムの概念が追加されました。 Oid は、デバイスごとの oid と実行プログラムごとの Oid という2つのカテゴリに分けられるようになりました。 次の表は、どの Oid がどのカテゴリに分類されるかを示しています。

| デバイスごとまたは実行単位| OID 名 |
| --- | --- |
| デバイスごと| OID_WWAN_DRIVER_CAPS |
|  | OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS |
|  | OID_WWAN_ENUMERATE_DEVICE_SERVICES |
|  | OID_WWAN_PRESHUTDOWN |
|  | OID_WWAN_VENDOR_SPECIFIC |
|  | OID_WWAN_SYS_CAPS |
|  | OID_WWAN_DEVICE_SLOT_MAPPINGS |
| 実行プログラムごと | OID_WWAN_AUTH_CHALLENGE |
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
> Windows 10 バージョン1703でも[OID_WWAN_RADIO_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-radio-state)が更新されました。 詳細については、「OID_WWAN_RADIO_STATE」を参照してください。

## <a name="mbim-interface-update-for-multi-sim-operations"></a>マルチ SIM 操作用の MBIM インターフェイスの更新

Windows 以外のモバイルオペレーティングシステムでは、複数の MBIM 機能を備えた1つの USB 複合デバイスとして複数実行プログラムのモデムが表示されます。 各 MBIM 関数は、登録を維持できる実行プログラムを表します。 実行プログラム固有のコマンドと通知は、その実行プログラムを表す MBIM 関数を介して交換されますが、モデム固有のコマンド (つまり、実行プログラムに固有ではないコマンド) とそれに対応する通知を送信または送信することができます。基になる同じ USB 複合デバイスに属する任意の MBIM 関数から。 

MBIM 関数に対して発行されたすべての CID セットまたはクエリ要求は、ミニポートインスタンスが関連付けられているモデムと実行プログラムに対して実行されます。同様に、MBIM 関数から送信されるすべての要請されていない通知は、MBIM 関数が関連付けられているモデムおよび実行プログラムに適用されます。 同様に、ミニポートインスタンスから送信されたすべての要請されていないデバイスサービスイベントは、モデムと、MBIM 関数が関連付けられている実行プログラムに適用されます。 たとえば、MBIM 関数からの要請されていない MBIM_CID_REGISTER_STATE または MBIM_CID_PACKET_SERVICE 通知は、関連するモデム/実行プログラムの登録またはパケットサービスの状態のみを示し、他のモデムまたは他の実行プログラムの状態とは関係がありません。 

1つのデバイスに複数のモデムまたは複数の実行プログラムがある場合、特定のモデムと実行プログラムの組み合わせに関連する非状況依存の非対応の通知は、前述のモデムおよび実行プログラムに関連付けられている MBIM 関数から発行される必要があります。 

複数のモデムまたは複数の実行プログラムがあるデバイスでは、特定のモデムおよび実行プログラムに関連する、非状況依存の CID クエリ要求が、その modem と実行プログラムの組み合わせに関連付けられている MBIM 関数に発行される場合があります。 このようなクエリ要求を受け取る関数は、CID 定義に従って処理する必要があります。 モデムのファームウェアによって選択されている場合、このようなクエリ要求は、そのモデムと実行プログラムに関連付けられている MBIM 関数によって処理される他の CID セットまたはクエリ要求と同時に処理される可能性があります。 同じモデムに関連付けられているすべての MBIM 関数は、それが表す実行プログラムに加えて、その携帯電話モデムについても同じ状態情報を報告します。  

1つのデバイスに複数のモデムまたは複数の実行プログラムがある場合、そのモデムと実行プログラムに関連付けられている MBIM 関数に対して、実行プログラムに固有ではない CID セット要求が発行されることがあります。 モデムは、このような要求の進行状況を全体として追跡します。 このような設定要求がいずれかのアダプターで進行中で、まだ完了していない場合は、そのようなセット要求の試行 (同じモデムおよび実行プログラムに関連付けられているアダプターインスタンスへの要求) が、前の要求が完了した後にキューに登録され、処理される必要があります。

次の図は、2つの異なるモデムにおける WWANSVC と MBIM の機能の間の情報フローを示しています。

![MBIM 関数を使用したモデムの構造](images/multi-SIM_10_MBIMspecification.png "MBIM 関数を使用したモデムの構造")

このセクションには、定義済みのデバイスサービスのモデム全体と実行プログラムごとの詳細な CID の説明が含まれています。 定義は、既存のパブリック MBIM 1.0 仕様への参照を返します。 MBIM 準拠のデバイスは、CID_MBIM_DEVICE_SERVICES によって照会されたときに、次のデバイスサービスを実装して報告します。 既知の既存のサービスは、USB NCM MBIM 1.0 仕様のセクション10.1 で定義されています。 Microsoft はこれを拡張して次のサービスを定義します。

サービス名 =**基本接続拡張機能**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 値 = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

**UUID_MS_BasicConnect**には、次の cid が定義されています。

| CID | コマンドコード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_MS_SYS_CAPS | 5 | Windows 10 Version 1703 |
| MBIM_CID_MS_DEVICE_CAPS_V2 | 6 | Windows 10 Version 1703 |
| MBIM_CID_MS_DEVICE_SLOT_MAPPINGS | 7 | Windows 10 Version 1703 |
| MBIM_CID_MS_SLOT_INFO_STATUS | 8 | Windows 10 Version 1703 |

次の CID セクションのすべてのオフセットは、InformationBuffer MBIM_COMMAND_MSG の先頭から計算されます。

### <a name="mbim_cid_ms_sys_caps"></a>MBIM_CID_MS_SYS_CAPS

#### <a name="description"></a>説明

この CID は、モデムに関する情報を取得します。 これは、USB 関数として公開されている MB のインスタンスのいずれかで送信できます。

##### <a name="query"></a>[クエリ]

MBIM_COMMAND_MSG の InformationBuffer には、MBIM_MS_SYS_CAPS_INFO として応答データが含まれています。

##### <a name="set"></a>設定

該当しない。

##### <a name="unsolicited-event"></a>一方的なイベント

該当しない。

#### <a name="parameters"></a>パラメーター

|  | 設定 | [クエリ] | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | 該当なし | 該当なし |
| 応答 | 該当なし | MBIM_MS_SYS_CAPS_INFO | 該当なし |

#### <a name="data-structures"></a>データ構造

##### <a name="query"></a>[クエリ]

InformationBuffer は null にする必要があり、InformationBufferLength は0である必要があります。

##### <a name="set"></a>設定

該当しない。

##### <a name="response"></a>応答

InformationBuffer では、次の MBIM_SYS_CAPS_INFO 構造体を使用する必要があります。

| [オフセット] | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NumberOfExecutors | UINT32 | このモデムによって報告された MBB インスタンスの数 |
| 4 | 4 | NumberOfSlots | UINT32 | このモデムで使用可能な物理 UICC スロットの数 |
| 8 | 4 | コンカレンシー | UINT32 | 同時にアクティブになる可能性がある MBB インスタンスの数 |
| 12 | 8 | ModemId | UINT64 | 各モデムの一意64ビット識別子 |

*Numberofexecutors*フィールドは、現在の構成でモデムによってサポートされている*エグゼキュータ*の数を表します。 これは、モデムがサポートする "サブフォン" スタックの数に直接マップされます。 

*Numberofslots*フィールドは、モデム上に物理的に存在するスロットの数を表します。 報告される各スロットは、UICC カードを受け取ることができる必要があります (スロット自体は、必要に応じて異種混合にすることができます (ミニ SIM、マイクロ SIM、nano SIM、または ETSI で定義されている標準)。 スロットの数は、サポートされているエグゼキュータの数以上である必要があります。 "大なり" のプロビジョニングでは、セキュリティ、NFC などのために、などの非テレフォニー UICC を使用できます。

*同時実行*フィールドは、同時にアクティブになる可能性がある実行プログラム (MBB インスタンス) の数を表します。 この範囲は、 *1 ≤ Concurrency ≤ NumberOfExecutors*である必要があります。 たとえば、デュアルスタンバイモデムの同時実行性は1で、デュアルアクティブモデムの同時実行数は2になります。

*Modemid*フィールドは、特定のモデムハードウェアの一意の64ビット識別子を表します。 IHV は、それぞれのモデムに対して一意の64ビット値を生成する独自のロジックを実装できます。たとえば、IMEI 番号の1つをハッシュし、64ビットの数値をランダムに生成します。64ビット ID が生成されると、再起動と SIM カードの削除/挿入の間で保持される必要があります。

#### <a name="status-codes"></a>状態コード

この CID は、一般的な状態コードを使用します ([パブリック USB MBIM 標準](https://go.microsoft.com/fwlink/p/?linkid=842064)のセクション9.4.5 の「状態コードの使用」を参照してください)。

### <a name="mbim_cid_ms_device_caps_v2"></a>MBIM_CID_MS_DEVICE_CAPS_V2

#### <a name="description"></a>説明

この CID は、実行プログラムに関連する機能情報を取得します。 この CID は MBIM_CID_DEVICE_CAPS の拡張であるため、ここでは、パブリック USB MBIM 標準のセクション10.5.1 に記載されている MBIM_CID_DEVICE_CAPS からの変更のみを示します。

この CID は引き続きクエリ専用となり、MBIM サービス MSUUID_BASIC_CONNECT および CID MBIM_CID_MS_DEVICE_CAPS_V2 で MBIM_COMMAND_MSG に応答して MBIM_MS_DEVICE_CAPS_INFO_V2 構造が返されます。

#### <a name="parameters"></a>パラメーター

|  | 設定 | [クエリ] | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | 該当なし | 該当なし |
| 応答 | 該当なし | MBIM_MS_DEVICE_CAPS_INFO_V2 | 該当なし |

#### <a name="data-structures"></a>データ構造

##### <a name="query"></a>[クエリ]

10.5.1.4 public USB MBIM standard のセクションと同じです。

##### <a name="set"></a>設定

該当しない。

##### <a name="response"></a>応答

InformationBuffer では、次の MBIM_DEVICE_CAPS_INFO_V2 構造体を使用する必要があります。 パブリック USB MBIM 標準のセクション10.5.1 で定義されている MBIM_CID_DEVICE_CAPS 構造と比較して、次の構造には*Deviceindex*という名前の新しいフィールドがあります。 ここに記載されていない限り、パブリック USB MBIM 標準の表10-14 のフィールドの説明がここに適用されます。

| [オフセット] | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | DeviceType | MBIM_DEVICE_TYPE |  |
| 4 | 4 | CellularClass | MBIM_CELLULAR_CLASS |  |
| 8 | 4 | VoiceClass | MBIM_VOICE_CLASS |  |
| 12 | 4 | シムクラス | MBIM_SIM_CLASS | この CID がサポートされている MBIM モデムの場合は、そのようなクラスは常に Mbimシムクラスとして報告されます。 |
| 16 | 4 | Microsoft.visualstudio.ordesigner.dataclass.member | MBIM_DATA_CLASS |  |
| 20 | 4 | SmsCaps | MBIM_SMS_CAPS |  |
| 24 | 4 | ControlCaps | MBIM_CTRL_CAPS |  |
| 28 | 4 | 最大セッション | UINT32 |  |
| 32 | 4 | CustomDataClassOffset | OFFSET |  |
| 36 | 4 | CustomDataClassSize | サイズ (0. 22) |  |
| 40 | 4 | DeviceIdOffset | OFFSET |  |
| 44 | 4 | DeviceIdSize | サイズ (0. 26) |  |
| 48 | 4 | FirmwareInfoOffset | OFFSET |  |
| 52 | 4 | FirmwareInfoSize | サイズ (0 ~ 60) |  |
| 56 | 4 | ハードウェアの配信 Ooffset | OFFSET |  |
| 60 | 4 | ハードウェアのインフォサイズ | サイズ (0 ~ 60) |  |
| 64| 4 | ExecutorIndex | UINT32 | 実行プログラムのインデックス。 この値の範囲は*0* ~ *n-1*です。 *n*は、MBIM モデムに含まれる MBB インスタンスの数です。 値は常に定数で、列挙の順序とは無関係です。 |
| 68 |  | DataBuffer | DATABUFFER | *CustomDataClass*、 *DeviceId*、 *FirmwareInfo*、およびの各メンバーを格納*している*データバッファー。 |

#### <a name="status-codes"></a>状態コード

この CID は、一般的な状態コードを使用します (パブリック USB MBIM 標準のセクション9.4.5 の「状態コードの使用」を参照してください)。

### <a name="mbim_cid_ms_device_slot_mappings"></a>MBIM_CID_MS_DEVICE_SLOT_MAPPINGS

#### <a name="description"></a>説明

この CID は、デバイススロットのマッピングを設定または返します (つまり、実行プログラムとスロットのマッピング)。

##### <a name="query"></a>[クエリ]

MBIM_COMMAND_MSG の InformationBuffer は使用されません。 MBIM_COMMAND_DONE の InformationBuffer に MBIM_MS_DEVICE_SLOT_MAPPING_INFO が返されます。

##### <a name="set"></a>設定

MBIM_COMMAND_MSG の InformationBuffer に MBIM_MS_DEVICE_SLOT_MAPPING_INFO が含まれています。 MBIM_COMMAND_DONE の InformationBuffer に MBIM_MS_DEVICE_SLOT_MAPPING_INFO が返されます。 Set CID が成功したか失敗したかにかかわらず、応答に含まれる MBIM_MS_DEVICE_SLOT_MAPPING_INFO は、現在のデバイススロットマッピングを表します。

##### <a name="unsolicited-events"></a>一方的なイベント

該当しない。

#### <a name="parameters"></a>パラメーター

|  | 設定 | [クエリ] | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | 該当なし | 該当なし |
| 応答 | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | 該当なし |

#### <a name="data-structures"></a>データ構造

##### <a name="query"></a>[クエリ]

InformationBuffer は null にする必要があり、InformationBufferLength は0である必要があります。

##### <a name="set"></a>設定

InformationBuffer では、次の MBIM_MS_DEVICE_SLOT_MAPPING_INFO 構造体を使用する必要があります。

| [オフセット] | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | MapCount (MC) | UINT32 | マッピングの数。これは、常にデバイス/エグゼキュータの数と等しくなります。 |
| 4 | 8 * MC | SlotMapList | OL_PAIR_LIST | このリストの*i 番目*のペア。ここで、(0 < = i < = (MC-1)) は、 *i 番目*のデバイス/実行プログラムに現在マップされているスロットのインデックスを記録します。 ペアの最初の要素は、4バイトのフィールドであり、この MBIM_MS_DEVICE_SLOT_MAPPINGS_INFO 構造体の先頭 (オフセット 0) から UINT32 に計算された DataBuffer へのオフセットが含まれます。 ペアの2番目の要素は、レコード要素の4バイトサイズです。 スロットインデックスの種類は UINT32 であるため、ペアの2番目の要素は常に4です。 |
| 4 + (8 * MC) | 4 * MC | DataBuffer | DATABUFFER | *SlotMapList*を格納するデータバッファー。 スロットのサイズは4バイトで、MC はスロットインデックスの数と同じであるため、DataBuffer の合計サイズは 4 * MC になります。 |

##### <a name="response"></a>応答

Set で使用される MBIM_MS_DEVICE_SLOT_MAPPING_INFO は、応答のために InformationBuffer でも使用されます。

#### <a name="status-codes"></a>状態コード

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_BUSY | デバイスがビジー状態のため、操作に失敗しました。 関数からの明示的な情報がない場合、この条件をクリアするために、ホストは、失敗した操作を再試行するヒントとして、関数 (通知やコマンド入力候補など) による後続のアクションを使用できます。 |
| MBIM_STATUS_FAILURE | 操作が失敗しました (一般的なエラー)。 |
| MBIM_STATUS_VOICE_CALL_IN_PROGRESS | 音声通話が進行中のため、操作に失敗しました。 |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーター (マッピングの範囲外または重複する値など) が原因で、操作に失敗しました。 |

### <a name="mbim_cid_ms_slot_info_status"></a>MBIM_CID_MS_SLOT_INFO_STATUS

#### <a name="description"></a>説明

この CID は、指定された UICC スロットとその中のカード (存在する場合) の高レベルの集計された状態を取得します。 また、いずれかのスロットの状態が変化したときに、要請されていない通知を配信するためにも使用できます。

##### <a name="query"></a>[クエリ]

MBIM_COMMAND_MSG の InformationBuffer に MBIM_MS_SLOT_INFO_REQ 構造体が含まれています。 MBIM_COMMAND_DONE メッセージの InformationBuffer に MBIM_MS_SLOT_INFO 構造体が含まれています。

##### <a name="set"></a>設定

該当しない。

##### <a name="unsolicited-events"></a>一方的なイベント

イベント InformationBuffer には MBIM_MS_SLOT_INFO 構造体が含まれています。 関数は、複合スロットとカードの状態が変化した場合にこのイベントを送信します。

#### <a name="parameters"></a>パラメーター

|  | 設定 | [クエリ] | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | MBIM_MS_SLOT_INFO_REQ | 該当なし |
| 応答 | 該当なし | MBIM_MS_SLOT_INFO | MBIM_MS_SLOT_INFO |

#### <a name="data-structures"></a>データ構造

##### <a name="query"></a>[クエリ]

InformationBuffer では、次の MBIM_MS_SLOT_INFO_REQ 構造体を使用する必要があります。

| [オフセット] | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SlotIndex | UINT32 | 照会するスロットのインデックス。 |

##### <a name="set"></a>設定

該当しない。

##### <a name="response"></a>応答

InformationBuffer では、次の MBIM_MS_SLOT_INFO 構造体を使用する必要があります。

| [オフセット] | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SlotIndex | UINT32 | スロットのインデックス。 |
| 4 | 4 | 状態 | MBIM_MS_UICC_SLOT_STATE | スロットとカードの状態 (該当する場合)。 |

次の MBIM_MS_UICCSLOT_STATE 構造は、スロットの可能な状態を示します。

| 状態 | 値 | 説明 |
| --- | --- | --- |
| UICCSlotStateUnknown | 0 | モデムはまだ初期化中のため、SIM スロットの状態は決定的ではありません。 |
| UICCSlotStateOffEmpty | 1 | UICC スロットが電源オフになっていて、カードが存在しません。 電源がオフになっているスロットにカードが存在するかどうかを判断できない実装は、その状態を UICCSlotStateOff として報告します。 |
| UICCSlotStateOff | 2 | UICC スロットの電源がオフになっています。 |
| UICCSlotStateEmpty | 3 | UICC スロットが空です (カードがありません)。 |
| UICCSlotStateNotReady | 4 | UICC スロットが占有され、電源がオンになっていますが、その中のカードはまだ準備ができていません。 |
| UICCSlotStateActive | 5 | UICC スロットが占有され、そのスロット内のカードの準備ができています。 |
| UICCSlotStateError | 6 | UICC スロットは使用されており、電源が入っていますが、カードがエラー状態であるため、次にリセットされるまで使用できません。 |
| UICCSlotStateActiveEsim | 7 | スロットのカードは、アクティブなプロファイルを持つ eSIM で、コマンドを受け入れる準備ができています。 |
| UICCSlotStateActiveEsimNoProfiles | 8 | スロットのカードは、プロファイルがない (またはアクティブなプロファイルがない) eSIM で、コマンドを受け入れる準備ができています。 |

##### <a name="mbim_ms_uiccslot_state-transition-guidance-for-multi-sim-devices"></a>マルチ sim デバイスの MBIM_MS_UICCSLOT_STATE の移行に関するガイダンス

正しい UICC スロットの状態遷移に準拠することで、OS がすべての変更を正しく処理し、正しいトースト通知がユーザーに表示されるようになります。

Sim によって*挿入*されたトースト通知の場合、OS では埋め込みスロット (SIM2/スロット 1) が選択され、物理スロット (SIM1/スロット 0) に SIM が挿入されるときに、次の状態遷移が発生します。

| SIM 挿入前のスロット0の有効な値 | SIM 挿入後のスロット0の有効な値 |
| --- | --- |
| UICCSlotStateEmpty | UICCSlotStateActive |
| UICCSlotStateOffEmpty | <ul><li>UICCSlotStateActiveEsim</li><li>UICCSlotStateActiveEsimNoProfile</li></ul> |

Sim によって*削除さ*れるトースト通知については、OS は、sim が挿入された状態で物理スロット (SIM1/スロット 0) が選択され、物理スロット (SIM1/スロット 0) から sim を削除したときに次の状態遷移が行われることを前提としています。

| SIM を削除する前のスロット0の有効な値 | SIM 削除後のスロット0の有効な値 |
| --- | --- |
| UICCSlotStateActive | UICCSlotStateEmpty |
| <ul><li>UICCSlotStateActiveEsim</li><li>UICCSlotStateActiveEsimNoProfile</li></ul> | UICCSlotStateOffEmpty |

#### <a name="status-codes"></a>状態コード

この CID は、一般的な状態コードを使用します (パブリック USB MBIM 標準のセクション9.4.5 の「状態コードの使用」を参照してください)。

### <a name="non-ndis-mapping-of-per-executor-and-per-modem-mbim-cids"></a>実行プログラムごととモデムごとの MBIM Cid の非 NDIS マッピング

ほとんどの MBIM Cid マップまたは NDIS Oid に関連していますが、NDIS に対応していない Windows WMB クラスドライバーによって使用されるコマンドがいくつかあります。  このセクションでは、これらのコマンドがモデム単位か実行単位かを明確に説明します。  

| デバイスごとまたは実行単位 | CID 名 |
| --- | --- |
| デバイスごと | CID_MBIM_MSEMERGENCYMODE |
|  | CID_MBIM_MSHOSTSHUTDOWN |
| 実行プログラムごと | CID_MBIM_MSIPADDRESSINFO |
|  | CID_MBIM_MSNETWORKIDLEHINT |
|  | CID_MBIM_MULTICARRIER_CURRENT_CID_LIST |

