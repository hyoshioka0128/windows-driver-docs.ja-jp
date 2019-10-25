---
title: 監視フィルター ドライバーの INF ファイルの構成
description: 監視フィルター ドライバーの INF ファイルの構成
ms.assetid: b45c6f40-7254-4cc1-a007-d40eaa74a290
keywords:
- INF ファイル WDK ネットワーク, フィルタードライバー
- フィルタードライバーの監視のための WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f38636af59c59a1239486f1c427463eb7e6b1791
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835039"
---
# <a name="configuring-an-inf-file-for-a-monitoring-filter-driver"></a>監視フィルター ドライバーの INF ファイルの構成





次の NDIS フィルタードライバーのインストールに関する問題は、監視フィルタードライバーに関連付けられています。

-   INF ファイルの**クラス**inf ファイルエントリを**netservice**に設定します。 次の例は、INF ファイルのサンプル**クラス**エントリを示しています。
    ```INF
    Class = NetService
    ```

-   フィルタードライバーの INF ファイルの*Ddinstall*セクションには、**特性**エントリが必要です。 次の例は、フィルターの INF ファイルで**特性**エントリを定義する方法を示しています。

    ```INF
    Characteristics=0x40000
    ```

    0x40000 値は、NCF\_LW\_FILTER (0x40000) が設定されていることを示します。 フィルタードライバーでは、NCF\_FILTER (0x400) フラグを設定することはできません。 NCF\_ *Xxx*フラグの値は、 *netcfgx*で定義されています。 NCF\_ *Xxx*フラグの詳細については、[ネットワークの INF ファイルの「Ddinstall」セクション](ddinstall-section-in-a-network-inf-file.md)を参照してください。

-   次の例に示すように、INF ファイルに**Netcfginstanceid** inf ファイルエントリを設定します。

    ```INF
    NetCfgInstanceId="{5cbf81bf-5055-47cd-9055-a76b2b4e3697}"
    ```

    *Uuidgen.exe*ツールを使用して、 **netcfginstanceid**エントリの GUID を作成できます。

-   フィルタードライバーの INF ファイルの*Ddinstall*セクションには、 **Ndi**キーの**Addreg**ディレクティブが含まれている必要があります。 INF ファイルでは、 **Ndi**キーの下に**サービス**エントリを指定する必要があります。 INF ファイルの*service-install*セクションの**servicebinary**エントリは、フィルタードライバーのバイナリへのパスを指定します。 詳細については、ネットワークの INF ファイルの「 [Ndi キーにサービス関連の値を追加する](adding-service-related-values-to-the-ndi-key.md)」および「 [Ddinstall. Services」セクション](ddinstall-services-section-in-a-network-inf-file.md)を参照してください。

-   フィルタードライバーの INF ファイルの*Ddinstall*セクションには、 **FilterType**および**filterruntype**エントリが必要です。 監視フィルターを指定するには、次の例に示すように、INF ファイルで**FilterType**エントリを定義します。

    ```INF
    HKR, Ndi,FilterType,0x00010001 ,0x00000001
    ```

    **FilterType**値0x00000001 は、フィルターが監視フィルターであることを示します。

-   次の例に示すように、INF ファイルで**Filterruntype**エントリを定義します。

    ```INF
    HKR, Ndi,FilterRunType,0x00010001 ,0x00000002
    ```

    前の例の0x00000002 値は、フィルターモジュールが省略可能であることを示しています。 必須フィルターモジュールをインストールするには、 **Filterruntype**エントリを0x00000001 に設定します。 詳細については、「[必須フィルタードライバー](mandatory-filter-drivers.md)」を参照してください。

    **注**  オプションの変更なしの lwf ドライバーを使用しない場合は、監視用ライトウェイトフィルター (lwf) ドライバーを必須にしないことを強くお勧めします。 これは、必須の監視用の LWF ドライバーによって、省略可能な LWF ドライバーの変更が[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)に失敗することがあるためです。 監視用の LWF ドライバーは、すべてのレベルでのネットワークトラフィックの監視を容易にするために、フィルターを変更するたびに、設計によってバインドされます。 次のシナリオを考えてみましょう。
    -   必須の監視用の LWF ドライバーのインスタンスは、オプションの変更 LWF ドライバーを介してインストールされます。
    -   省略可能な LWF ドライバーを変更すると、下位のコンポーネントにアタッチできません。 これにより、必須の監視 LWF ドライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)ハンドラーが呼び出されなくなります。
    -   現在、必須の LWF ドライバーのインスタンスが読み込まれていないため、NDIS はインターフェイスや NIC にプロトコル (TCP/IP など) をバインドしないため、インターフェイスを使用できなくなります。

     

-   次の例は、フィルタードライバーの INF ファイルでサービスの名前を指定する方法を示しています。

    ```INF
    HKR, Ndi,Service,,"NdisMon"
    ```

    この例では、"NdisMon" は、NDIS に報告されるドライバーのサービスの名前です。 フィルタードライバーのサービスの名前は、ドライバーのバイナリの名前とは異なる場合がありますが、通常は同じです。

-   次の例では、フィルター INF ファイルが、そのサービスを追加したときにフィルタードライバーのサービスの名前を参照する方法を示します。
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

-   フィルター INF ファイルでは、次の例に示すように、 **Coservices**属性のフィルターのプライマリサービス名を少なくとも1つ指定する必要があります。

    ```INF
    HKR, Ndi,CoServices,0x00010000,"NdisMon"
    ```

    **Coservices**属性の詳細については、「 [ndi キーへのサービス関連値の追加](adding-service-related-values-to-the-ndi-key.md)」を参照してください。

-   フィルタードライバーの INF ファイルの**Filterclass**値によって、フィルターを変更する順序が決定されます。 ただし、監視フィルタードライバーでは、 **Filterclass**キーは定義されません。 代わりに、最初にインストールされる監視フィルターモジュールは、ミニポートアダプターに最も近いものです。

-   ドライバーのバインドを制御するには、監視フィルタードライバーの INF ファイルで次のエントリを定義する必要があります。

    ```INF
    HKR, Ndi\Interfaces,UpperRange,,"noupper"
    HKR, Ndi\Interfaces,LowerRange,,"nolower"
    HKR, Ndi\Interfaces, FilterMediaTypes,,"ethernet"
    ```

    ドライバーのバインドの制御の詳細については、「[フィルタードライバーのバインド関係の指定](specifying-filter-driver-binding-relationships.md)」を参照してください。

-   監視フィルターの INF ファイルでは、フィルタードライバー、特定のアダプターに関連付けられているパラメーター、および特定のインスタンス (フィルターモジュール) に関連付けられているパラメーターの共通パラメーター定義を指定する必要があります。 次の例は、いくつかの一般的なパラメーター定義を示しています。
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

 

 





