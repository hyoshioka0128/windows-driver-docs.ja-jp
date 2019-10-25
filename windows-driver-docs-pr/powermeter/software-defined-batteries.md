---
title: ソフトウェア定義のバッテリ
description: ソフトウェア定義のバッテリ
keywords:
- ソフトウェア定義のバッテリ
- SDB
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cc44dfff5e2fe72b95010538488ee3f0472d156
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829037"
---
# <a name="software-defined-battery"></a>ソフトウェア定義のバッテリ

>[!NOTE]
> 一部の情報はリリース前の製品に関することであり、正式版がリリースされるまでに大幅に変更される可能性があります。 ここに記載された情報について、Microsoft は明示または黙示を問わずいかなる保証をするものでもありません。

## <a name="introduction"></a>概要

このトピックの目的は、ソフトウェアで定義された電池 (SDB) について説明し、Windows SDB アーキテクチャについて説明し、この機能のための Windows API と DDI コントラクトの詳細を説明することです。 

このトピックでは、最初に、仮定の2つのバッテリシステムの単純な Age バランシングの SDB アルゴリズムを紹介します。 これには、SDB アルゴリズムを実装するために必要なアーキテクチャレイアウトと API コントラクトが続きます。

## <a name="nomenclature"></a>区別

- BattC-バッテリクラスドライバー

- CAD-課金調停ドライバー (CAD) は、USB レガシ、USB タイプ C、およびワイヤレス充電ソース間の電源を判別する Microsoft ドライバーです。

- コールドスワップ可能な電池-brownouts または合計電源障害が発生してもシステムから削除できないバッテリ

- [サイクル数]-ACPI 仕様で説明されているように、バッテリによって行われた完全な充電放電サイクルの数

- ホットスワップ可能な電池-システムの動作中に安全に削除できる電池です。 brownouts のリスクはありません。

- HPMI-ハードウェア電源マネージャーインターフェイス

- ホットスワップが可能でない電池-システムに取り付けられている、1つまたは複数のコールドスワップ可能なバッテリ

- スワップできないバッテリ-エンドユーザーによって削除されないように設計されていないバッテリ

## <a name="sdb-overview"></a>SDB の概要
ソフトウェアで定義されている電池の MSR research のドキュメントについては、「 [https://www.microsoft.com/research/wp-content/uploads/2016/02/multibattery_sosp2015.pdf](https://www.microsoft.com/research/wp-content/uploads/2016/02/multibattery_sosp2015.pdf)」を参照してください。 

このトピックでは、このホワイトペーパーで説明されているアイデアを選択し、ノート pc やその他のモバイルデバイスでのソフトウェアベースのバッテリ寿命分散機能のビューを示します。 

2つのバッテリシステムを想像してください。 1つのバッテリがリムーバブルバッテリ以外で、SOC の横にある場合は、この*内部バッテリ*を呼び出します。 もう1つのバッテリは、ホットスワップが可能なバッテリで、リムーバブルキーボードの横にあります。この*外部バッテリ*を呼び出します。 

*マルチバッテリシステム*

![内部および外部のバッテリを示すマルチバッテリシステム](images/powermeter-multi-battery.png)

キーボードが接続されると、一定の時間にわたって接続が切断されるため、2つの電池の有効期間が異なります。 これにより、SDB の単純な age 均衡アルゴリズムを採用して、バッテリと長引くシステムの使いやすさをバランスを調整するためのスコープが作成されます。

## <a name="simple-age-balancing-sdb-algorithm"></a>単純な Age バランシングの SDB アルゴリズム

このアルゴリズムは、バッテリの寿命とのバランスを取るため、*単純な age 分散*と呼ばれます。 単純な age 均衡アルゴリズムによって、システムは最低でも期限切れになったバッテリの放電を優先します。 低いサイクルカウントを持つバッテリは、電力を保持するための容量が増加するだけでなく、一般に電力を供給する場合にも効率的です。 これにより、システムがバッテリで維持できる時間が長引くます。

*単純な Age バランシングの SDB アルゴリズム*

![単純な Age バランシングの SDB アルゴリズム](images/powermeter-simple-age-balancing-algorithm.png)

単純な年齢分散アルゴリズムの基礎となる中心的な考え方は、上のフローチャートの決定ボックス (2) で示されているように、バッテリ残量が少なくなるバッテリを使用することです。 この例の架空のシステムでは、内部または外部のバッテリを排他的に使用することができます。 ただし、すべてのシステムでこれが当てはまるとは限りません。 その他のシステムは、柔軟性が高くない場合や、バッテリの使用に対して電気的な制限を受ける場合があります。 このような場合、アルゴリズムでは、最大限のバランスを取る必要があります。 たとえば、次の点を考慮してください。  

1. 外部バッテリ上で排他的に電力を維持できないシステム (外付けバッテリが補助電源専用になるように設計されていることが原因である可能性があります)。 このシステムでは、上のフローチャートで、プロセスブロック (A) の内部バッテリと外部電池の両方を同時に放電することで、単純な age バランシングアルゴリズムを実装できます。

2. 外部のバッテリを必要とするシステムは、いつでも使用できます (リムーバブルキーボードの電源を維持するために追加の電源描画があることが原因である可能性があります)。このシステムは、単純な期間分散アルゴリズムを同時に実装する場合があります。上のフローチャートで、プロセスブロック (B) の内部バッテリと外部電池の両方を放電します。

単純な age バランスアルゴリズムは、システムを実行するための十分な料金が内部および外部のバッテリに存在する場合にのみ使用することができます。決定ボックス (1) は、上記のフローチャートでこの条件チェックを表します。 たとえば (この場合も、仮に仮定のシステムに戻ります)、外部バッテリに課金されない場合は、バッテリの寿命と、判断ボックス (1) によって "NO" 分岐が発生するという範囲はありません。

OEM は、内部または外部の電池の電源が入っていない場合を含めて、単純な年齢バランスアルゴリズムを有効にしない場合に、制約と条件を自由に選択できます。 たとえば、次の場合には、OEM は年齢分散を実行しないように選択できます。

1.  SOC/プロセッサは高パフォーマンスモードで実行されています
2.  システムがサーマル不安定

単純な age 均衡アルゴリズムが使用されない場合 (上記の1つ以上の条件により)、ロジックは、前述のフローチャートの「プロセスボックス (3)」に示されているように、OEM の独自のバッテリ使用ポリシーに戻ります。 プロセスボックス (3) は、SDB がサポートされていない場合に、ロジックが有効になります。


## <a name="span-idadapting-sdbspanspan-idadapting-sdbspanadapting-sdb-algorithm-for-use-with-hot-swappable-batteries"></a><span id="adapting-sdb"></span><span id="ADAPTING-SDB"></span>ホットスワップが可能な電池で使用する SDB アルゴリズムを適合させる

Simple age balancing SDB アルゴリズムでは、healthiest のバッテリを使用しようとしますが、この方法は長期のバッテリ寿命を向上させるのに適していますが、次のシナリオで説明するように、システムの短期的な有用性に深刻な影響を与える可能性があります。

上記で説明した2つのバッテリシステムでは、次の状況を考慮してください。

1.  ユーザーは、内部と外部の両方のバッテリが消費されるまで、システムを十分に使用することを想定しています。

2.  外部のバッテリが、内部のバッテリと比較して期限切れになっています。

このシステムで simple age balancing アルゴリズムが実行されると、最初に内部のバッテリに格納されている料金を消費します (上記の条件 #1 と #2 に基づいて)。 ユーザーがしばらくした後に外部バッテリを切断することを決定した場合、内部バッテリが使用されているために外部バッテリが切断されると、使用可能なバッテリ容量が大幅に減少するため、ユーザーエクスペリエンスが悪くなります。

SDB 以外のシステムでは、通常、この問題は発生しません。これは、ほとんどの場合、内部バッテリが使用される前に外部バッテリが使い果たされるためです。

このため、上記のシナリオが発生する可能性が高い場合は、単純な age 均衡アルゴリズムを選択的に無効にする必要があります。 

要約すると、ユーザーが外部のバッテリを取り外した長時間にシステムを使用することが予想される場合は、SDB アルゴリズムを無効にして、OEM バッテリ使用ポリシーを使用するように戻すことをお勧めします (通常は、最初に外部バッテリの使用を優先します)。

Windows によってバッテリの可用性が計算され、"ホットスワップされていない電池を保持する" ヒントが生成されます。 このヒントが SDB アルゴリズムによって使用される場合、次のフロー図の決定ボックス (X) に示されます。

*ホットスワップが可能な電池用に適応した、シンプルな Age バランシングの SDB アルゴリズム*

![ホットスワップが可能な電池用に適応した、シンプルな Age バランシングの SDB アルゴリズム](images/powermeter-simple-age-balancing-algorithm-hot-swap.png)


## <a name="span-idimplementing-sdbspanspan-idimplementing-sdbspanimplementing-sdb-algorithm-in-firmware"></a><span id="implementing-sdb"></span><span id="IMPLEMENTING-SDB"></span>ファームウェアでの SDB アルゴリズムの実装

このセクションでは、システムファームウェアに実装されているバッテリ放電制御ロジック全体を示します。 これは、前に説明したバッテリの使用期間分散ロジックに基づいており、(Y) ブロックでマークされた) 既存のマルチバッテリ放電ロジックがどのように組み込まれるかを示しています。

これは、SDB アルゴリズムを Oem が実装する方法を示すものではなく、SDB の動作を示すために使用される、このセクションで説明する単純な仮定のマルチバッテリデバイスの包括的な例であることに注意してください。


*Simple Age Balancing SDB アルゴリズムの完全なファームウェア実装*

![Simple Age Balancing SDB アルゴリズムの完全なファームウェア実装](images/powermeter-firmware-age-balancing-algorithm-hot-swap.png)


## <a name="power-stack-architecture"></a>電源スタックのアーキテクチャ

このセクションでは、電源スタックに参加しているすべてのコンポーネントのコンポーネントレイアウトと、それらの相対的な関係について説明します。

![HPMI を示す電源スタックのアーキテクチャ](images/powermeter-hpmi-stack-architecture.png)


### <a name="battery-miniport"></a>バッテリミニポート

バッテリミニポートインターフェイスは変わりません。

SDB インターフェイスは、ACPI/CmBatt メカニズムに依存したり、独自のミニポートを開発したりする OEM の要望に影響を与えることはありません。

注: Windows は、すべての[IOCTL_BATTERY_SET_INFORMATION](https://docs.microsoft.com/windows/desktop/Power/ioctl-battery-set-information)コマンドを、システムで列挙されたすべてのバッテリデバイスに転送します。

### <a name="hpmi"></a>HPMI

ハードウェア電源マネージャーインターフェイス (HPMI) は、パワースタックで導入された新しいコンポーネントです。

HPMI は、OEM/デバイスの製造元によって開発および所有されているドライバーです。

HPMI は、基礎となるハードウェアの構成と状態に関する知識を持っており、システムファームウェアにアクセスできます。 

SDB 機能を実装するために、HPMI ドライバーは次のことを行います。

1.  それ自体を Windows に登録します。
2.  SDB のサポートを提供します。
3.  Windows によって提供される SDB コントロールパラメーターを使用します。

前もって HPMI インターフェイスを実装するには、SDB をサポートするマルチバッテリシステムが必要です。 HPMI API プロトコルは、複数のバッテリシステムを実装するための新しい標準です。

今後、他の課金、放電、および課金の管理機能をサポートするように HPMI が更新される予定です。

### <a name="driver-characteristics"></a>ドライバーの特性

システム上には、HPMI ドライバーのインスタンスが1つだけ存在している必要があります。
HPMI は、ユーザーモードまたはカーネルモードドライバーとして実装されている場合があります。

### <a name="installation"></a>インストール

HPMI は、OEM の裁量により、ACPI デバイスとして、または他の OEM サービス/ドライバーのいずれかによって、ルートとして列挙される場合があります。

### <a name="implementation-of-sdb-algorithm"></a>SDB アルゴリズムの実装

次の図は、ファームウェアコンポーネントが多数のバッテリ制御ロジックを既にホストしている場合に、SDB アルゴリズムを実装する方法の2つの例を示しています。

![HPMI とファームウェアの例 SDB アルゴリズムスタックの例](images/powermeter-firmware-and-hpmi-implementation.png)


### <a name="hpmi-implements-sdb-algorithm"></a>HPMI での SDB アルゴリズムの実装

HPMI では、SDB アルゴリズムを実装することを選択できます。これには、料金/放電ヒントをファームウェアに転送するために HPMI が必要です。 

### <a name="firmware-implements-sdb-algorithm"></a>ファームウェアが SDB アルゴリズムを実装する

または、HPMI はフォワーダーとして機能し、前の図に示すように、SDB アルゴリズムが実装されているファームウェアに Windows バッテリ使用率ヒントを転送するだけです。 このモデルの使用は、次の理由で推奨されます。

1. SDB アルゴリズムを実装するために必要な情報は、すぐに使用できます。この情報を HPMI に渡す必要はありません。

2. SDB アルゴリズムは、マルチバッテリシステムに既に実装されている放電ロジックの拡張です。

SDB アルゴリズムの実装方法を示す完全なフローチャートモデルは、[ファームウェアでの Sdb アルゴリズムの実装](#IMPLEMENTING-SDB)に示されています。



## <a name="interface-definitions"></a>インターフェイスの定義

HPMI デバイス用の新しいデバイスインターフェイスクラス GUID が導入されました。 HPMI デバイスは、[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)を実装するものとして識別する必要があります。 詳細については、「WDK での[デバイスインターフェイスの使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)」を参照してください。

Windows では、HPMI デバイスのクエリと構成にデバイスの到着通知を使用します。

```cpp
//
// HPMI Device Interface Class.
//

// {DEDAE202-1D20-4C40-A6F3-1897E319D54F}
DEFINE_GUID(GUID_DEVINTERFACE_HPMI, 
            0xdedae202, 0x1d20, 0x4c40, 0xa6, 0xf3, 0x18, 0x97, 0xe3, 0x19, 0xd5, 0x4f);
```

HPMI では、複数の同時 IOCTL 呼び出しを行うことができます。

デバイスインデックスは0に設定する必要があることに注意してください。

### <a name="feature-discovery"></a>機能の検出

[IOCTL_HPMI_QUERY_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ni-hpmi-ioctl_hpmi_query_capabilities)は、hpmi でサポートされている機能を検出するために使用されます。 IOCTL_HPMI_QUERY_CAPABILITIES は必須の IOCTL です。

新しい HPMI ドライバーインスタンスが検出された後、Windows はこの IOCL を HPMI に発行します。 


```cpp
//
// Query command sent to HPMI to query features supported by HPMI and Windows
// services requested by HPMI.
//
// This IOCTL may be issued multiple times, HPMI must respond with same 
// information in HPMI_QUERY_CAPABILITIES_RESPONSE, as a response to all
// subsequent IOCTL calls.
//

#define IOCTL_HPMI_QUERY_CAPABILITIES                     
    CTL_CODE(FILE_DEVICE_BATTERY, 0x200, 
             METHOD_BUFFERED, FILE_READ_ACCESS | FILE_WRITE_ACCESS)
```

```cpp
//
// IOCTL_HPMI_QUERY_CAPABILITIES - Command.
//

typedef struct _HPMI_QUERY_CAPABILITIES {

    //
    // Set to HPMI_QUERY_CAPABILITIES_VERSION_1.
    //

    ULONG Version;

} HPMI_QUERY_CAPABILITIES, *PHPMI_QUERY_CAPABILITIES;
```

```cpp
#define HPMI_QUERY_CAPABILITIES_VERSION_1                   
    (1)
#define HPMI_QUERY_CAPABILITIES_SIZEOF_VERSION_1         
    sizeof(HPMI_QUERY_CAPABILITIES)
```

```cpp
//
// IOCTL_HPMI_QUERY_CAPABILITIES - Response.
//

#define HPMI_REQUEST_SERVICE_NONE                           
    (0x00000000)    // No Windows services is requested.
#define HPMI_REQUEST_SERVICE_BATTERY_UTILIZATION_HINTS      
    (0x00000001)    // Battery utilization hints requested from Windows.

#define HPMI_CAPABILITY_NOT_SUPPORTED                       
    (0x00000000)    // HPMI supports no capabilities.
#define HPMI_CAPABILITY_SDB_OEM_SIMPLE_AGE_BALANCING        
    (0x00000001)    // OEM device specific age balancing SDB support
```

```cpp
typedef struct _HPMI_QUERY_CAPABILITIES_RESPONSE {

    //
    // Set to HPMI_QUERY_CAPABILITIES_RESPONSE_VERSION_1.
    //

    ULONG Version;

    //
```


### <a name="command-format"></a>コマンドの形式

Windows は、この IOCTL と[HPMI_QUERY_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ns-hpmi-_hpmi_query_capabilities)を発行します。

バージョンは HPMI_QUERY_CAPABILITIES_VERSION_1 に設定されています。


### <a name="response-format"></a>応答形式 

HPMI は STATUS_SUCCESS コードを返す必要があります。

HPMI は、 [HPMI_QUERY_CAPABILITIES_RESPONSE](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ns-hpmi-_hpmi_query_capabilities_response)構造体で次の値を設定することによって応答します。

- バージョンは HPMI_QUERY_CAPABILITIES_RESPONSE_VERSION_1 に設定されています。
- RequestService は HPMI_REQUEST_SERVICE_BATTERY_UTILIZATION_HINTS に設定され、HPMI ドライバーが[IOCTL_HPMI_BATTERY_UTILIZATION_HINT](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ni-hpmi-ioctl_hpmi_battery_utilization_hint)を受け取るようにします。
- SdbCapabilities は HPMI_CAPABILITY_SDB_OEM_SIMPLE_AGE_BALANCING に設定され、バッテリの残量分散のサポートを示します。


#### <a name="battery-utilization"></a>バッテリ使用率

Windows では、最新のバッテリ使用状況に関するヒントを提供するために HPMI に[IOCTL_HPMI_BATTERY_UTILIZATION_HINT](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ni-hpmi-ioctl_hpmi_battery_utilization_hint)があります。 IOCTL_HPMI_BATTERY_UTILIZATION_HINT は必須の IOCTL です。

HPMI では、内蔵の電池を節約するために、「[ホットスワップ可能な電池で使用する SDB アルゴリズムの適応](#ADAPTING-SDB)」で説明されているように、PreserveNonHotSwappableBatteries ヒントを利用できます。

```cpp
//
// Set command sent to HPMI to provide battery utilization hints.
//
// This IOCTL may be issued multiple times if HPMI requests
// HPMI_REQUEST_SERVICE_BATTERY_UTILIZATION_HINTS service.
//

#define IOCTL_HPMI_BATTERY_UTILIZATION_HINT                 
    CTL_CODE(FILE_DEVICE_BATTERY, 0x201, 
             METHOD_BUFFERED, FILE_READ_ACCESS | FILE_WRITE_ACCESS)

//
// Boolean type value.
//

typedef enum _HPMI_HINT_BOOL {
    // No data is available.
    HpmiBoolUnavailable = 0,

    // Condition is asserted to be false.
    HpmiBoolFalse,

    // Condition is asserted to be true.
    HpmiBoolTrue,

    // Value not used.
    HpmiBoolMax

} HPMI_HINT_BOOL, *PHPMI_HINT_BOOL;
```

```cpp
//
// IOCTL_HPMI_BATTERY_UTILIZATION_HINT - Command.
//

typedef struct _HPMI_BATTERY_UTILIZATION_HINT {

    //
    // Set to HPMI_BATTERY_UTILIZATION_HINT_VERSION_1.
    //

    ULONG Version;

    //
    // This hint indicates if the OEM Battery Manager should attempt to save as
    // much charge as possible in the non-hot swappable batteries (i.e. the
    // batteries are generally referred to as "internal batteries", these
    // batteries cannot be removed while system is operational).
    //
    // Interpretation of values:
    //  - HpmiBoolUnavailable:
    //      Battery utilization hint is unavailable at the moment.
    //  - HpmiBoolFalse:
    //      It is not necessary to preserve charge in the internal batteries
    //      at the moment.
    //  - HpmiBoolTrue:
    //      Every attempt should be made to save as much charge as possible in
    //      the internal batteries.
    //

    HPMI_HINT_BOOL PreserveNonHotSwappableBatteries;

} HPMI_BATTERY_UTILIZATION_HINT, *PHPMI_BATTERY_UTILIZATION_HINT;
```

```cpp
#define HPMI_BATTERY_UTILIZATION_HINT_VERSION_1              
    (1)
#define HPMI_BATTERY_UTILIZATION_HINT_SIZEOF_VERSION_1       
    sizeof(HPMI_BATTERY_UTILIZATION_HINT)
```


### <a name="command-format"></a>コマンドの形式 

Windows は、この IOCTL と HPMI_BATTERY_UTILIZATION_HINT を発行します。 バージョンは*HPMI_BATTERY_UTILIZATION_HINT_VERSION_1*に設定されています。

[HPMI_BATTERY_UTILIZATION_HINT](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ns-hpmi-_hpmi_battery_utilization_hint)

PreserveNonHotSwappableBatteries は、次のいずれかの値に設定されます。

- Hpmiブール使用不可: バッテリ使用状況のヒントを提供できない場合に設定します。 応答として、HPMI/Fimware は、一般に事実上の放電ポリシーに関与する必要があります。
- Hpmiブール値: Windows がバッテリのいえるを発生させるタイミングを決定するときに設定します。
- Hpmiブール True: Windows が内部のバッテリに格納されているエネルギーを節約する必要がある場合に設定します。

### <a name="response-format"></a>応答形式

HPMI は STATUS_SUCCESS コードを返す必要があります。

応答にデータが返されません。


## <a name="sample-interface-contract"></a>サンプルインターフェイスコントラクト

ここで説明するインターフェイス定義の完全な (サンプル) API コントラクトについては、 [Hmpi .h](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/index)を参照してください。



>[!NOTE]
> このドキュメントの内容は、予告なしに変更される可能性があります。



