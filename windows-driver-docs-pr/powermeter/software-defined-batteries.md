---
title: ソフトウェアには、バッテリが定義されています。
description: ソフトウェアには、バッテリが定義されています。
keywords:
- ソフトウェアには、バッテリが定義されています。
- SDB
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 527c7f1488a855300c65a14951b9a120a27a760a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331863"
---
# <a name="software-defined-battery"></a>ソフトウェアには、バッテリが定義されています。

>[!NOTE]
> 一部の情報はリリース前の製品に関することであり、正式版がリリースされるまでに大幅に変更される可能性があります。 本書に記載された情報について、Microsoft は明示または黙示を問わずいかなる保証をするものでもありません。

## <a name="introduction"></a>概要

このトピックの目的は、ソフトウェア定義されているバッテリ (SDB) を導入し、Windows SDB アーキテクチャをについて説明し、Windows API と DDI コントラクトは、この機能の詳細です。 

トピックは、架空の 2 つのバッテリ システムの有効期間の単純な分散 SDB アルゴリズムを導入することで開始します。 アーキテクチャが続きます SDB アルゴリズムを実装するために必要なレイアウトと API コントラクト。

## <a name="nomenclature"></a>命名規則

- BattC - バッテリ クラス ドライバー

- CAD - 料金調停ドライバー (CAD) は USB レガシ、USB 型-c およびワイヤレスの充電ソース間で電力を調停する Microsoft のドライバー

- コールド ホットスワップ可能なバッテリ - バッテリ サージや総電力障害のリスクを負うことがなく、システムから削除することはできません。

- サイクル カウント - ACPI 仕様」の説明に従って、バッテリによって行われました完全充電放電サイクルの数

- ホット スワップ可能なバッテリのバッテリをシステムがサージの危険を冒さずの操作中に安全に削除できます。

- HPMI - ハードウェアの電源マネージャー インターフェイス

- 非ホット スワップ可能なバッテリの 1 つ以上コールド Swappable と、システムにインストールされている非 Swappable バッテリ

- 非 Swappable バッテリ - バッテリでを設計およびエンド ユーザーによって削除するためのものはありません。

## <a name="sdb-overview"></a>SDB の概要
ソフトウェア定義されているバッテリで MSR 研究論文をこちら: [ https://www.microsoft.com/research/wp-content/uploads/2016/02/multibattery_sosp2015.pdf](https://www.microsoft.com/research/wp-content/uploads/2016/02/multibattery_sosp2015.pdf)します。 

このトピックでこのホワイト ペーパーで説明されている選択のアイデアを再開し productizing 分散ラップトップの機能とその他のモバイル デバイス ベースのソフトウェアのバッテリ寿命のビューに提示します。 

2 つのバッテリ システムを想像してください。 1 つのバッテリが SOC – の横にある、非リムーバブル バッテリましょうこの*内部バッテリ*します。 その他のバッテリがホット スワップ可能なバッテリ、このリムーバブル キーボード – の横にあるましょう*外部バッテリ*します。 

*複数のバッテリ システム*

![内部および外部のバッテリを示す複数のバッテリ システム](images/powermeter-multi-battery.png)

キーボードは期間のアタッチ、デタッチ、異なる方法で時代には、2 つのバッテリを強制します。 これには、年齢、バッテリを分散して、分散アルゴリズム SDB シンプル有効期間を使用し、システムの使いやすさの期間を延長するためのスコープが作成されます。

## <a name="simple-age-balancing-sdb-algorithm"></a>単純な年齢分散 SDB アルゴリズム

アルゴリズムと呼ばれる*年齢の単純な分散*しようとするバッテリ寿命のバランスを取るためです。 分散アルゴリズムの単純な時代は、期限切れが最も低いのバッテリの放電を優先するシステムです。 バッテリが小さい方のサイクル数を計上するには、保持、電源ですがも通常より効率的に機能を提供するために容量の増加だけでなくが。 これにより、システムがバッテリで維持できる時間を延長します。

*単純な年齢分散 SDB アルゴリズム*

![単純な年齢分散 SDB アルゴリズム](images/powermeter-simple-age-balancing-algorithm.png)

分散アルゴリズムの単純な時代の背後にあるという考え方は、単に最小限のバッテリ サイクルが発生する、バッテリを使用するカウントで意思決定ボックス (2) 上記のフローチャートで示したします。 この例では、仮想的なシステムは、内蔵または外付けのバッテリを排他的に使用できます。 ただし、これができないのすべてのシステムの場合は true。 その他のシステムでは、柔軟性ができないか、バッテリの使用方法の電気の制約があります。 このような場合は、アルゴリズムには、年齢の分散の最善の試みが期待しています。 たとえば、次の点を検討してください。  

1. 電源 (補助 power ソースのみを使用する外部のバッテリが設計されているので可能性があります)、外部のバッテリを排他的に耐えることがあるシステム。 このシステムは、分散アルゴリズムを同時に両方のプロセス ブロック (A) 上のフローチャートで内部および外部バッテリは放電してで単純な時代を実装することができます。

2. 存在するときに、外部のバッテリを必要とするシステムを使用する (電源がオンにリムーバブル キーボードの維持に関連する追加の電力が原因ででもかまいません)。このシステムは、分散アルゴリズムを同時に両方のプロセス ブロック (B) 上のフローチャートで内部および外部のバッテリは放電してで単純な時代を実装することができます。

意思決定のボックス (1) 上のフローチャートには、この条件チェックを示し、システムを実行する内部および外部のバッテリに存在するための十分な料金がある場合にのみ使用する分散アルゴリズムの単純な時代を配置することがあります。 例 (もう一度仮想的なシステムに移動) は、外部のバッテリの充電がなければ、バッテリの分散の有効期間の範囲はありませんし、意思決定ボックス (1) は"NO"ブランチの結果は。

OEM では自由に分散アルゴリズムの単純な時代には配置されません効果、それに内蔵または外付けのバッテリが電源がときに、制約と条件を選択します。 たとえば、OEM は、年齢の分散を実行しないように選択できます。

1.  SOC/プロセッサが高パフォーマンス モードで実行されています。
2.  システムが不安定サーマル

分散アルゴリズムの単純な時代は (上記 1 つまたは複数の条件) のため配置で使用しない、ロジックは OEM の独自のバッテリ使用ポリシーによってプロセス ボックス (3) 上のフローチャートの図のように戻ります。 プロセス ボックス (3) は、OEM が有効になる SDB がサポートされていない場合、ロジックです。


## <a name="span-idadapting-sdbspanspan-idadapting-sdbspanadapting-sdb-algorithm-for-use-with-hot-swappable-batteries"></a><span id="adapting-sdb"></span><span id="ADAPTING-SDB"></span>SDB アルゴリズムを適合させるホット スワップ可能なバッテリでの使用

分散 SDB アルゴリズムの単純な時代は、この方法は、動作が良好、バッテリを使用しようとしました。 長期的なバッテリの寿命を向上させるために深刻な影響を与える可能性、システムの短期的なユーザビリティ次のシナリオで説明したようにします。

上記で説明した 2 つのバッテリ システムでは、次のような状況を考慮してください。

1.  内部および外部の両方のバッテリの充電がなくなるまで、十分な長さのシステムを使用して、ユーザーが必要です。

2.  外部のバッテリは内部のバッテリと比較してよりを期限切れです。

分散アルゴリズムの単純な時代がこのシステムで実行されるときに最初のバッテリを内部に格納されている料金 (1 と 2 上に示したに基づいて条件) を使い果たすを試みます。 デタッチをユーザーが決定したときに内部のバッテリ使用すると、しばらくすると、この結果は不正なユーザー エクスペリエンスを外部 1 回のバッテリが大幅に削減するバッテリ容量が使用できるため、外部のバッテリが切り離されます。

SDB 以外のシステムでは、この一般には発生しません、内部のバッテリが使用する前にほとんどの場合、外部のバッテリが使い果たされているためです。

選択的に負荷分散アルゴリズムのシナリオを超える場合に発生する可能性が単純な時代を無効にする必要があるためです。 

まとめると、外部のバッテリを削除に長い期間をシステムを使用するユーザーが期待どおりたびに、SDB アルゴリズムを無効にして、OEM のバッテリ使用ポリシー (これは通常、最初に、外部のバッテリを使用が優先されます) を使用してに最適な方法があります。

Windows では、バッテリの可用性を計算し、「保持する非ホット スワップ可能なバッテリ」ヒントを生成します。 このヒントが SDB アルゴリズムによって使用される次のフロー図では決定ボックス (X) で示すようにします。

*単純な有効期間がホット スワップ可能なバッテリの応用 SDB アルゴリズムの分散*

![単純な有効期間がホット スワップ可能なバッテリの応用 SDB アルゴリズムの分散](images/powermeter-simple-age-balancing-algorithm-hot-swap.png)


## <a name="span-idimplementing-sdbspanspan-idimplementing-sdbspanimplementing-sdb-algorithm-in-firmware"></a><span id="implementing-sdb"></span><span id="IMPLEMENTING-SDB"></span>ファームウェアで SDB アルゴリズムを実装します。

このセクションでは、システム ファームウェアで実装された完全なバッテリの放電制御ロジックを示しています。 これは、バッテリ寿命を分散して ((Y) のブロックにマークされている) 既存の複数のバッテリの放電ロジックを組み込むと方法をデモンストレーションするための前述のロジックに基づいています。

SDB 動作を説明するために使用されるこのセクションで説明されている単純な仮想的な複数のバッテリのデバイスの包括的な例ではなく、Oem によって SDB アルゴリズムを実装する方法の処方ではないことに注意してください。


*分散 SDB アルゴリズムの単純な有効期間の完全なファームウェアの実装*

![分散 SDB アルゴリズムの単純な有効期間の完全なファームウェアの実装](images/powermeter-firmware-age-balancing-algorithm-hot-swap.png)


## <a name="power-stack-architecture"></a>スタックの電源のアーキテクチャ

このセクションでは、電源スタックとの相対関係で相互に参加しているすべてのコンポーネントのコンポーネントのレイアウトについて説明します。

![HPMI を示す power スタック アーキテクチャ](images/powermeter-hpmi-stack-architecture.png)


### <a name="battery-miniport"></a>バッテリ ミニポート

バッテリのミニポート インターフェイスは、同じになります。

SDB インターフェイスに影響を与えるまたはしないで ACPI/CmBatt メカニズムに依存する、または、独自のミニポートを開発する OEM の要望に影響を与えます。

注:Windows 転送すべて[IOCTL_BATTERY_SET_INFORMATION](https://msdn.microsoft.com/library/windows/desktop/aa372701.aspx)システムに列挙されているすべてのバッテリ デバイスにコマンド。

### <a name="hpmi"></a>HPMI

ハードウェアの電源マネージャー インターフェイス (HPMI) は、電源のスタックで導入された新しいコンポーネントです。

HPMI は、開発および OEM/デバイスの製造元によって所有されているドライバーです。

HPMI は、基になるハードウェアの構成と状態に関する詳細な知識を備え、システム ファームウェアにアクセスします。 

HPMI ドライバーは SDB 機能を実装するには。

1.  Windows の登録にします。
2.  SDB サポートを提供します。
3.  Windows で提供される SDB 制御パラメーターを使用します。

SDB をサポートする複数のバッテリ システムは、今後 HPMI インターフェイスを実装する必要があります。 HPMI API プロトコルは、複数のバッテリ システムを実装するための新しい標準です。

プランがあるその他の充電中、放電をサポートし、管理機能の課金 HPMI を更新できる、将来、ようにします。

### <a name="driver-characteristics"></a>ドライバーの特性

HPMI ドライバーの複数のインスタンスは、システムに存在する必要があります。
HPMI は、ユーザー モードまたはカーネル モード ドライバーのいずれかとして実装することがあります。

### <a name="installation"></a>インストール

HPMI は、ACPI デバイスとして明示可能性があります。 またはルートのいずれかの他のサービス/oem が OEM の裁量によって列挙します。

### <a name="implementation-of-sdb-algorithm"></a>SDB アルゴリズムの実装

ファームウェア コンポーネントは、バッテリの制御ロジックの大部分を既にホストされている場合、SDB アルゴリズムが実装する方法の 2 つの例を次の図に示します。

![HPMI およびファームウェア例 SDB アルゴリズム スタックの使用例](images/powermeter-firmware-and-hpmi-implementation.png)


### <a name="hpmi-implements-sdb-algorithm"></a>HPMI 実装 SDB アルゴリズム

HPMI SDB アルゴリズムを実装することもできます、これには、ファームウェアに転送の料金/放電ヒントに HPMI が必要です。 

### <a name="firmware-implements-sdb-algorithm"></a>ファームウェアの実装 SDB アルゴリズム

または、HPMI は、フォワーダとして機能し、Windows バッテリを単に、SDB アルゴリズムが実装されているファームウェアへの使用率のヒント転送上の図に示すように可能性があります。 このモデルの使用は、次の理由からお勧めします。

1. SDB アルゴリズムを実装するために必要な情報がすぐに使用できる – HPMI までには、この情報を渡す必要はありません。

2. SDB アルゴリズムは、複数のバッテリ システムで既に実装されているロジックを退院の拡張機能です。

完全なフローチャート モデルをした SDB アルゴリズムを実装する方法を示すを示した[ファームウェアで SDB アルゴリズムを実装する](#IMPLEMENTING-SDB)します。



## <a name="interface-definitions"></a>インターフェイスの定義

HPMI デバイスの新しいデバイスのインターフェイスのクラス GUID が導入されました。 実装として自身 HPMI デバイスを識別する必要があります、[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)します。 詳細については、次を参照してください。[を使用してデバイスのインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)WDK に含まれています。

Windows では、クエリを実行すると、HPMI デバイスを構成するデバイスの組み込みの通知を使用します。

```cpp
//
// HPMI Device Interface Class.
//

// {DEDAE202-1D20-4C40-A6F3-1897E319D54F}
DEFINE_GUID(GUID_DEVINTERFACE_HPMI, 
            0xdedae202, 0x1d20, 0x4c40, 0xa6, 0xf3, 0x18, 0x97, 0xe3, 0x19, 0xd5, 0x4f);
```

HPMI のことができるようサービスの複数の同時 IOCTL 呼び出し。

デバイスのインデックスを 0 に設定することに注意してください。

### <a name="feature-discovery"></a>機能の検出

[IOCTL_HPMI_QUERY_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/mt828475.aspx) HPMI でサポートされる機能を検出するために使用します。 IOCTL_HPMI_QUERY_CAPABILITIES では、必要な IOCTL です。

Windows は発行この IOCL HPMI に 1 回新しい HPMI ドライバーのインスタンスが検出されるとします。 


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

Windows の問題では、この IOCTL [HPMI_QUERY_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/mt828472.aspx)します。

バージョンは、HPMI_QUERY_CAPABILITIES_VERSION_1 に設定されます。


### <a name="response-format"></a>応答の形式 

HPMI は、STATUS_SUCCESS コードを返す必要があります。

HPMI の応答で、次の値を設定して[HPMI_QUERY_CAPABILITIES_RESPONSE](https://msdn.microsoft.com/library/windows/hardware/mt828473.aspx)構造体。

- HPMI_QUERY_CAPABILITIES_RESPONSE_VERSION_1 にバージョンが設定されています。
- RequestService HPMI ドライバーを受け取るように HPMI_REQUEST_SERVICE_BATTERY_UTILIZATION_HINTS に設定されている[IOCTL_HPMI_BATTERY_UTILIZATION_HINT](https://msdn.microsoft.com/library/windows/hardware/mt828474.aspx)します。
- SdbCapabilities は HPMI_CAPABILITY_SDB_OEM_SIMPLE_AGE_BALANCING のバッテリ寿命の分散のサポートを示すために設定します。


#### <a name="battery-utilization"></a>バッテリの使用率

Windows 問題[IOCTL_HPMI_BATTERY_UTILIZATION_HINT](https://msdn.microsoft.com/library/windows/hardware/mt828474.aspx) HPMI に更新されたバッテリ最も使用率のヒントを提供します。 IOCTL_HPMI_BATTERY_UTILIZATION_HINT では、必要な IOCTL です。

」の説明に従って、HPMI は PreserveNonHotSwappableBatteries ヒントを利用できる[適応 SDB アルゴリズムを使用してホット スワップ可能なバッテリ](#ADAPTING-SDB)内部のバッテリを節約するためにします。

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

Windows では、この IOCTL HPMI_BATTERY_UTILIZATION_HINT を発行します。 設定されているバージョン*HPMI_BATTERY_UTILIZATION_HINT_VERSION_1*します。

[HPMI_BATTERY_UTILIZATION_HINT](https://msdn.microsoft.com/library/windows/hardware/mt828469.aspx)

PreserveNonHotSwappableBatteries は、次の値のいずれかに設定されます。

- HpmiBoolUnavailable:バッテリの使用率のヒントを指定しない場合に設定します。 応答として HPMI/ファームウェアは、事実上放電ポリシーを一般に連携する必要があります。
- HpmiBoolFalse:Windows はバッテリの寿命が発生する分散のチャンスが判断した場合に設定します。
- HpmiBoolTrue:Windows が判断した場合のセットは、内部のバッテリに格納されているエネルギーを節約するために必要があります。

### <a name="response-format"></a>応答の形式

HPMI は、STATUS_SUCCESS コードを返す必要があります。

応答には、データは返されません。


## <a name="sample-interface-contract"></a>サンプル インターフェイス コントラクト

参照してください[HMPI.h](https://msdn.microsoft.com/library/windows/hardware/mt828470.aspx)完全 (サンプル) API コントラクト インターフェイスの定義をここで説明をします。



>[!NOTE]
> このドキュメントの内容は、予告なく変更される可能性が。



