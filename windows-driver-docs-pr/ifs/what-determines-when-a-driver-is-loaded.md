---
title: ドライバーのロード時期の決定方法
description: ドライバーのロード時期の決定方法
ms.assetid: fe0f27e4-84d4-483e-8b4e-69c39ae332de
keywords:
- フィルター ドライバー WDK ファイル システム、ドライバーの読み込み
- ファイル システム フィルター ドライバー WDK、ドライバーの読み込み
- ドライバー WDK ファイル システムの読み込み
- ドライバー WDK ファイル システムの読み込み
- ドライバー開始の種類の WDK ファイル システム
- 型の WDK ファイル システムを起動します。
- 注文グループ WDK ファイル システムを読み込む
- SERVICE_BOOT_START
- SERVICE_SYSTEM_START
- SERVICE_AUTO_START
- SERVICE_DEMAND_START
- SERVICE_DISABLED
- ブート ドライバー WDK ファイル システム
- ブート開始ドライバー WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48beeb607b42424f5c7337512532b499a23585ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570342"
---
# <a name="what-determines-when-a-driver-is-loaded"></a>ドライバーのロード時期の決定方法


## <span id="ddk_what_determines_when_a_driver_is_loaded_if"></span><span id="DDK_WHAT_DETERMINES_WHEN_A_DRIVER_IS_LOADED_IF"></span>


調べる前にするタイミングと方法、ファイル システム ドライバーは、システムの起動シーケンス中に読み込まれる必要があるドライバーのスタートアップの種類を理解し、注文のグループを読み込めません。

### <a name="span-idddkdriverstarttypesifspanspan-idddkdriverstarttypesifspandriver-start-types"></a><span id="ddk_driver_start_types_if"></span><span id="DDK_DRIVER_START_TYPES_IF"></span>ドライバーのスタートアップの種類

カーネル モード ドライバーの*開始の種類*ドライバーがシステム起動時に読み込まれるかどうかを指定します。 開始の 5 つの種類があります。

<span id="SERVICE_BOOT_START__0x00000000_"></span><span id="service_boot_start__0x00000000_"></span><span id="SERVICE_BOOT_START__0X00000000_"></span>サービス\_ブート\_開始 (0x00000000)  
(OS) のオペレーティング システム ローダーによって開始ドライバーを示します。 ファイル システム フィルター ドライバーは、この開始の種類またはサービスによく使用\_デマンド\_を開始します。 Microsoft Windows XP およびそれ以降のシステムでのフィルターは、新しいを利用するにはこの開始の種類を使用する必要があります[ファイル システム フィルター ロード順序グループ](load-order-groups-for-file-system-filter-drivers.md)します。

<span id="SERVICE_SYSTEM_START__0x00000001_"></span><span id="service_system_start__0x00000001_"></span><span id="SERVICE_SYSTEM_START__0X00000001_"></span>サービス\_システム\_開始 (0x00000001)  
OS の初期化中に、ドライバーの開始を示します。 この開始の種類は、ファイル システムの認識エンジンによって使用されます。 下に示すファイル システムを除く"サービス\_無効にすると、"ファイル システム (ネットワーク ファイル システムのコンポーネントを含む) この開始の種類またはサービスを使用して、一般的\_デマンド\_を開始します。 この開始の種類は、システムの初期化中に列挙がシステムを読み込むため不要の PnP デバイスのデバイス ドライバーによっても使用されます。

<span id="SERVICE_AUTO_START__0x00000002_"></span><span id="service_auto_start__0x00000002_"></span><span id="SERVICE_AUTO_START__0X00000002_"></span>サービス\_自動\_開始 (0x00000002)  
システムの起動時にサービス コントロール マネージャーでの開始ドライバーを示します。 ほとんど使用しません。

<span id="SERVICE_DEMAND_START__0x00000003_"></span><span id="service_demand_start__0x00000003_"></span><span id="SERVICE_DEMAND_START__0X00000003_"></span>サービス\_デマンド\_開始 (0x00000003)  
(デバイス ドライバーの PnP マネージャー、または (ファイル システムとファイル システム フィルター ドライバー) のサービス コントロール マネージャーによって、オンデマンドで開始ドライバーを示します。

<span id="SERVICE_DISABLED__0x00000004_"></span><span id="service_disabled__0x00000004_"></span><span id="SERVICE_DISABLED__0X00000004_"></span>SERVICE\_DISABLED (0x00000004)  
サービス コントロール マネージャー、または PnP マネージャー、OS ローダーによって開始されていないドライバーを示します。 (ときに、ブート ファイル システム) を除くファイル システムの認識エンジンによって読み込まれるファイル システムで使用される (EFS) の場合、または別のファイル システムでします。 このようなファイル システムには、cdfs を含む、EFS、FastFat、NTFS、および UDF が含まれます。 デバッグ中にドライバーを一時的に無効にも使用されます。

### <a name="span-idddkspecifyingstarttypeifspanspan-idddkspecifyingstarttypeifspanspecifying-start-type"></a><span id="ddk_specifying_start_type_if"></span><span id="DDK_SPECIFYING_START_TYPE_IF"></span>開始の種類を指定します。

ドライバー開発者は、次の方法のいずれかでインストール時に開始ドライバーの種類を指定できます。

-   必要な開始の種類を指定することによって、 **StartType**内のエントリ、*サービス-インストール セクション*によって参照される、 [ **AddService** ](https://msdn.microsoft.com/library/windows/hardware/ff546326)ドライバーの INF ファイルでディレクティブです。 このメソッドは、ServiceInstall セクションで説明されています。

-   目的を渡すことによって開始の種類、 *dwStartType*パラメーターを呼び出すときに**CreateService**または**changeserviceconfig が**ユーザー モードのインストール プログラムから。 このメソッドが参照のエントリで説明されている**CreateService**と**changeserviceconfig が**Microsoft Windows SDK ドキュメント。

### <a name="span-idddkdriverloadordergroupsifspanspan-idddkdriverloadordergroupsifspandriver-load-order-groups"></a><span id="ddk_driver_load_order_groups_if"></span><span id="DDK_DRIVER_LOAD_ORDER_GROUPS_IF"></span>ドライバーの読み込み順序グループ

サービス内で\_ブート\_開始とサービス\_システム\_スタートでは、型、ドライバーが読み込まれる相対順序は各ドライバーのによって指定されます*ロード順序グループ*します。

ドライバーはサービスの開始型を持つ\_ブート\_START が呼び出される*ブート (またはブート開始) ドライバー*します。 Microsoft Windows 2000 およびそれ以前のシステムでは、ブート ドライバーであるほとんどのフィルターは、「フィルター」グループに属しています。 Microsoft Windows XP およびそれ以降のシステムでは、一般的に、ブート ドライバーは新しい FSFilter のいずれかに属している、フィルターは、注文のグループを読み込めません。 これらのロード順序グループがで詳しく説明されている[順序グループをファイル システム フィルター ドライバーの読み込み](load-order-groups-for-file-system-filter-drivers.md)します。

ドライバーはサービスの開始型を持つ\_システム\_開始もロード順序グループが所属する順序で読み込まれます。 ただし、システム開始ドライバーが読み込まれていないまですべてのブート ドライバーが読み込まれた後です。

**注**  はサービスの開始型を持つドライバーの読み込み順序グループは無視されます\_自動\_開始、サービス\_デマンド\_開始、またはサービス\_無効になっています。

 

ロード順序グループの完全な順序付きリストが見つかりません、 **ServiceGroupOrder**次のレジストリ キーのサブキー。

**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control**

サービスの使用は、同じロード グループの順序付け\_ブート\_開始とサービス\_システム\_開始ドライバー。 ただし、すべての SERVICE\_ブート\_開始ドライバーが読み込まれ、任意のサービスの前に開始\_システム\_開始ドライバーが読み込まれます。

### <a name="span-idddkspecifyingloadordergroupifspanspan-idddkspecifyingloadordergroupifspanspecifying-load-order-group"></a><span id="ddk_specifying_load_order_group_if"></span><span id="DDK_SPECIFYING_LOAD_ORDER_GROUP_IF"></span>ロード順序グループを指定します。

ドライバー開発者は、次の方法のいずれかでインストール時にドライバーをロード順序グループを指定できます。

-   目的のロード順序グループを指定して、 **LoadOrderGroup**内のエントリ、*サービス-インストール セクション*によって参照される、 **AddService**ドライバーの INF ディレクティブファイルです。 このメソッドは、ServiceInstall セクションで説明されています。

-   目的を渡すことによって開始の種類、 *lpLoadOrderGroup*パラメーターを呼び出すときに**CreateService**または**changeserviceconfig が**ユーザー モードのインストール プログラムから。 このメソッドが参照のエントリで説明されている**CreateService**と**changeserviceconfig が**Microsoft Windows SDK ドキュメント。

ドライバーに関する一般的な情報の読み込み順序と読み込み順グループを参照してください[ドライバーの読み込み順序を指定する](https://msdn.microsoft.com/library/windows/hardware/ff552319)します。

 

 




