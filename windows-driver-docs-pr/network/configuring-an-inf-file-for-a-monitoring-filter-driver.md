---
title: 監視フィルター ドライバーの INF ファイルの構成
description: 監視フィルター ドライバーの INF ファイルの構成
ms.assetid: b45c6f40-7254-4cc1-a007-d40eaa74a290
keywords:
- フィルター ドライバーの INF ファイル WDK ネットワーク
- フィルター ドライバー WDK ネットワークの監視
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a87b4a37c9e90a667ab65c51262c5900fd606d3a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570466"
---
# <a name="configuring-an-inf-file-for-a-monitoring-filter-driver"></a>監視フィルター ドライバーの INF ファイルの構成





次の NDIS フィルター ドライバー インストールの問題は、フィルター ドライバーを監視に関連付けられました。

-   設定、**クラス**INF ファイルのエントリを**NetService** INF ファイルにします。 次の例には、サンプルが表示されます。**クラス**INF ファイルのエントリ。
    ```INF
    Class = NetService
    ```

-   *DDInstall*フィルター ドライバーの INF ファイルのセクションがあります、**特性**エントリ。 次の例は、どのように定義する必要がある、**特性**フィルター INF ファイルのエントリ。

    ```INF
    Characteristics=0x40000
    ```

    0x40000 値が示す NCF\_LW\_フィルター (0x40000) を設定します。 フィルター ドライバーは、NCF を設定する必要がありますいない\_フィルター (0x400) フラグ。 値の NCF\_ *Xxx*でフラグが定義されている*Netcfgx.h*。 NCF の詳細については\_ *Xxx*フラグを参照してください[ネットワーク INF ファイルで DDInstall セクション](ddinstall-section-in-a-network-inf-file.md)します。

-   設定、 **NetCfgInstanceId** INF ファイルのエントリとして次の例は、INF ファイルでします。

    ```INF
    NetCfgInstanceId="{5cbf81bf-5055-47cd-9055-a76b2b4e3697}"
    ```

    使用することができます、 *Uuidgen.exe*の GUID を作成するためのツール、 **NetCfgInstanceId**エントリ。

-   *DDInstall*フィルター ドライバーの INF ファイルのセクションを含める必要があります、 **Addreg**ディレクティブを**Ndi**キー。 INF ファイルを指定する必要があります、**サービス**の下のエントリ、 **Ndi**キー。 **ServiceBinary**内のエントリ、*サービス インストール*INF ファイルのセクションは、フィルター ドライバーのバイナリへのパスを指定します。 詳細については、次を参照してください。 [Ndi キーに値を Adding Service-Related](adding-service-related-values-to-the-ndi-key.md)と[ネットワーク INF ファイルで DDInstall.Services セクション](ddinstall-services-section-in-a-network-inf-file.md)。

-   *DDInstall*フィルター ドライバーの INF ファイルのセクションがあります**FilterType**と**FilterRunType**エントリ。 監視のフィルターを指定するには、定義、 **FilterType**として次の例は、INF ファイルのエントリ。

    ```INF
    HKR, Ndi,FilterType,0x00010001 ,0x00000001
    ```

    **FilterType**値 0x00000001 では、監視のフィルターがあることを示します。

-   定義、 **FilterRunType**として次の例は、INF ファイルのエントリ。

    ```INF
    HKR, Ndi,FilterRunType,0x00010001 ,0x00000002
    ```

    前の例で 0x00000002 値は、フィルター モジュールが省略可能なことを示します。 必須のフィルター モジュールをインストールするには、設定、 **FilterRunType** 0x00000001 のエントリ。 詳細については、[必須フィルター ドライバー](mandatory-filter-drivers.md)を参照してください。

    **注**  制御された環境で使用する、場所がありますしないオプションがない限りに監視の lightweight filter (LWF) ドライバーを必須にしないことを強くお勧め LWF ドライバーを変更します。 これは必須の監視 LWF ドライバーが原因であるために失敗する LWF ドライバーを変更する省略可能な[ *FilterAttach*](https://msdn.microsoft.com/library/windows/hardware/ff549905)します。 監視 LWF ドライバーは、すべてのレベルでネットワーク トラフィックの監視を容易にするように設計上すべての変更のフィルターとバインディングにバインドされます。 次のシナリオを考えてみましょう。
    -   必須の監視 LWF ドライバーのインスタンスは、オプションの変更 LWF ドライバー経由でインストールされます。
    -   下位の変更の省略可能な LWF ドライバーは、下位のコンポーネントにアタッチに失敗します。 これにより、必須監視 LWF ドライバーの[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)ハンドラーが呼び出されない。
    -   これで、必須の LWF ドライバーのインスタンスが読み込まれていない、ために、NDIS はインターフェイスまたは NIC、つまり使用できないインターフェイスをレンダリングする任意のプロトコル (TCP/IP など) をバインドできません。

     

-   次の例では、フィルター ドライバーの INF ファイルで、サービスの名前を指定する方法を示します。

    ```INF
    HKR, Ndi,Service,,"NdisMon"
    ```

    NDIS することが報告されると、この例では、"NdisMon"、ドライバーのサービスの名前です。 フィルター ドライバーのサービスの名前をドライバーのバイナリの名前と異なることができますが、通常、これらが同じことに注意してください。

-   次の例では、そのサービスを追加するときに、フィルター INF ファイルが、フィルター ドライバーのサービスの名前を参照する方法を示します。
    ```INF
    [Install.Services]
    AddService=NdisMon,,NdisMon_Service_Inst

    [NdisMon_Service_Inst]
    DisplayName     = %NdisMon_Desc%
    ServiceType     = 1 ;SERVICE_KERNEL_DRIVER
    StartType       = 1 ;SERVICE_SYSTEM_START
    ErrorControl    = 1 ;SERVICE_ERROR_NORMAL
    ServiceBinary   = %12%\ndisMon.sys
    LoadOrderGroup  = NDIS
    Description     = %NdisMon_Desc%
    AddReg          = Common.Params.Reg
    ```

-   フィルター INF ファイルが少なくとものフィルターの主要なサービス名で指定する必要があります、 **CoServices**属性には、次の例を示します。

    ```INF
    HKR, Ndi,CoServices,0x00010000,"NdisMon"
    ```

    詳細については、 **CoServices**属性は、「 [Ndi キーに値を Adding Service-Related](adding-service-related-values-to-the-ndi-key.md)します。

-   **FilterClass** INF ファイルで値のフィルター ドライバーかのフィルターを変更するスタック内での順序を指定します。 ただし、監視のフィルター ドライバーは定義しないでください、 **FilterClass**キー。 代わりに、監視のフィルター モジュールがインストールされている最初に最も近いミニポート アダプターです。

-   ドライバーのバインディングを制御するため、フィルター ドライバーの INF ファイルが監視では、次のエントリを定義する必要があります。

    ```INF
    HKR, Ndi\Interfaces,UpperRange,,"noupper"
    HKR, Ndi\Interfaces,LowerRange,,"nolower"
    HKR, Ndi\Interfaces, FilterMediaTypes,,"ethernet"
    ```

    ドライバーのバインディングを制御する方法の詳細については、[フィルター ドライバーのバインドのリレーションシップの指定](specifying-filter-driver-binding-relationships.md)を参照してください。

-   監視フィルター INF ファイルには、フィルター ドライバー、特定のアダプターに関連付けられているパラメーターおよび特定のインスタンス (フィルター モジュール) に関連付けられているパラメーターの共通のパラメーター定義を指定する必要があります。 次の例では、いくつかの一般的なパラメーター定義を示します。
    ```INF
    [Common.Params.reg]

    HKR, FilterDriverParams\DriverParam, ParamDesc, ,"Driverparam for filter"
    HKR, FilterDriverParams\DriverParam, default, ,"5"
    HKR, FilterDriverParams\DriverParam, type,  ,"int"

    HKR, FilterAdapterParams\AdapterParam, ParamDesc, ,"Adapterparam for filter"
    HKR, FilterAdapterParams\AdapterParam, default, ,"10"
    HKR, FilterAdapterParams\AdapterParam, type,  ,"int"

    HKR, FilterInstanceParams\InstanceParam, ParamDesc, ,"Instance param for filter"
    HKR, FilterInstanceParams\InstanceParam, default, ,"15"
    HKR, FilterInstanceParams\InstanceParam, type,  ,"int"
    ```

 

 





