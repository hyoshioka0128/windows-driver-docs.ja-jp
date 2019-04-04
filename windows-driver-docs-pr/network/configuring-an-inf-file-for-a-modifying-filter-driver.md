---
title: 変更フィルター ドライバーの INF ファイルの構成
description: 変更フィルター ドライバーの INF ファイルの構成
ms.assetid: d9eac8f6-a560-41e5-ae71-3bd9d6714c3a
keywords:
- フィルター ドライバーの INF ファイル WDK ネットワーク
- フィルター ドライバー WDK ネットワークを変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e20d6bb441d7afb1452eaf3bf5e0852e2b56d8ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577733"
---
# <a name="configuring-an-inf-file-for-a-modifying-filter-driver"></a>変更フィルター ドライバーの INF ファイルの構成





次の NDIS フィルター ドライバー インストールの問題は、フィルター ドライバーの変更に関連付けられます。 独自の変更のフィルター ドライバーの INF ファイルを作成するには、調整の[NDIS 6.0 フィルター ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)します。

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
    NetCfgInstanceId="{5cbf81bd-5055-47cd-9055-a76b2b4e3697}"
    ```

    使用することができます、 *Uuidgen.exe*の GUID を作成するためのツール、 **NetCfgInstanceId**エントリ。

-   *DDInstall*フィルター ドライバーの INF ファイルのセクションを含める必要があります、 **Addreg**ディレクティブを**Ndi**キー。 INF ファイルを指定する必要があります、**サービス**の下のエントリ、 **Ndi**キー。 **ServiceBinary**内のエントリ、*サービス インストール*INF ファイルのセクションは、フィルター ドライバーのバイナリへのパスを指定します。 詳細については、[追加サービス関連する値を Ndi キー](adding-service-related-values-to-the-ndi-key.md)と[ネットワーク INF ファイルで DDInstall.Services セクション](ddinstall-services-section-in-a-network-inf-file.md)を参照してください。

-   *DDInstall*フィルター ドライバーの INF ファイルのセクションがあります**FilterType**と**FilterRunType**エントリ。 変更のフィルターを指定するには、定義、 **FilterType**として次の例は、INF ファイルのエントリ。

    ```INF
    HKR, Ndi,FilterType,0x00010001 ,0x00000002
    ```

    **FilterType** 0x00000002 の値の場合、フィルターが変更のフィルターであることを示します。

-   定義、 **FilterRunType**として次の例は、INF ファイルのエントリ。

    ```INF
    HKR, Ndi,FilterRunType,0x00010001 ,0x00000001
    ```

    前の例では、0x00000001 値は、フィルター モジュールが必須ことを示します。 オプションのフィルター モジュールをインストールするには、設定、 **FilterRunType** 0x00000002 エントリ。 詳細については、[必須フィルター ドライバー](mandatory-filter-drivers.md)を参照してください。

-   次の例では、変更フィルター ドライバーの INF ファイルで、サービスの名前を指定する方法を示します。

    ```INF
    HKR, Ndi,Service,,"NdisLwf"
    ```

    NDIS することが報告されると、この例では、NdisLwf、ドライバーのサービスの名前です。 ドライバーのバイナリの名前と異なるフィルター ドライバーのサービスの名前であることに注意してください: が通常それらは同じです。

-   次の例では、そのサービスを追加するときに、フィルター INF ファイルが、フィルター ドライバーのサービスの名前を参照する方法を示します。
    ```INF
    [Install.Services]
    AddService=NdisLwf,,NdisLwf_Service_Inst;, common.EventLog 

    [NdisLwf_Service_Inst]
    DisplayName     = %NdisLwf_Desc%
    ServiceType     = 1 ;SERVICE_KERNEL_DRIVER
    StartType       = 1 ;SERVICE_SYSTEM_START
    ErrorControl    = 1 ;SERVICE_ERROR_NORMAL
    ServiceBinary   = %12%\ndislwf.sys
    LoadOrderGroup  = NDIS
    Description     = %NdisLwf_Desc%
    AddReg          = Common.Params.reg
    ```

-   フィルター INF ファイルが少なくとものフィルターの主要なサービス名で指定する必要があります、 **CoServices**属性には、次の例を示します。

    ```INF
    HKR, Ndi,CoServices,0x00010000,"NdisLwf"
    ```

    詳細については、 **CoServices**属性は、「[追加サービス関連する値を Ndi キー](adding-service-related-values-to-the-ndi-key.md)します。

-   **FilterClass** INF ファイルで値のフィルター ドライバーかフィルターのスタック内での順序を指定します。 フィルター ドライバーを定義する必要があります、 **FilterClass**キー。 ドライバーのクラスには、次の表に、値のいずれかを指定できます。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">[値]</th>
    <th align="left">説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>スケジューラ</p></td>
    <td align="left"><p>スケジュール フィルター サービスのパケットです。 フィルター ドライバーのこのクラスは、暗号化クラスのフィルター ドライバー スタックの上に存在できる最上位レベルのドライバーです。 パケット スケジューラは、サービス (QoS) のコンポーネントとスケジューラの信号の品質にパケットに指定されている 802.1p の優先度の分類が優先順位に従って基になるドライバーにそれらのパケット レベルの送信を検出します。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>暗号化 (encryption)</p></td>
    <td align="left"><p>暗号化クラスのフィルター ドライバーは、スケジューラと圧縮クラスのフィルター間に存在します。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>compression</p></td>
    <td align="left"><p>圧縮クラス フィルター ドライバーは、暗号化と vpn クラスのフィルター間に存在します。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>vpn</p></td>
    <td align="left"><p>VPN クラス フィルター ドライバーは、圧縮と負荷分散のフィルター ドライバーとの間存在します。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>loadbalance</p></td>
    <td align="left"><p>フィルターの分散サービスを読み込みます。 フィルター ドライバーのこのクラスは、パケットのスケジュール設定とフェールオーバーのドライバーの間存在します。 負荷分散フィルター サービスは、ミニポート アダプターが基になるは、そのセットに対する作業負荷を分散することによって、パケットの転送には、そのワークロードを分散します。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>フェールオーバー</p></td>
    <td align="left"><p>フィルター サービスのフェールオーバー。 フィルター ドライバーのこのクラスは、負荷分散と診断のドライバーの間存在します。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>診断</p></td>
    <td align="left"><p>以下のスタックのフェールオーバーのドライバー診断フィルター ドライバーが存在します。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>custom</p></td>
    <td align="left"><p>カスタム クラスでフィルター ドライバーがドライバーの診断の下存在します。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>provider_address</p></td>
    <td align="left"><p>プロバイダー アドレス フィルター ドライバーでは、以下のボックスで、HYPER-V ネットワーク仮想化の ms_wnv フィルターが存在し、プロバイダー アドレス (PA) パケットを操作します。</p></td>
    </tr>
    </tbody>
    </table>




**注**固有のクラスの 1 つ以上のフィルター ドライバーは、フィルター ドライバーの変更の複数層のスタックに存在できます。 たとえば、2 つの変更のフィルター ドライバー **FilterClass** "scheduler"が、スタックで同時に存在できます。 以下を以前のインストール時刻のタイムスタンプを持つフィルター ドライバーがインストールされている (つまり、ミニポート アダプターに近い) 以降のタイムスタンプを持つフィルター ドライバー。 ただし、同じクラスを使用して複数のフィルター ドライバーの順序は正確に同じコンピューター上の異なるミニポート アダプターを経由。



次の例には、サンプルが表示されます。 **FilterClass**します。

```INF
HKR, Ndi,FilterClass,, compression
```


- HYPER-V スイッチ拡張機能フィルター ドライバーは、HYPER-V 拡張可能なスイッチで有効なのみです。 HYPER-V 拡張可能スイッチ フィルター ドライバーでは、次の表に、値のいずれかで FilterClass キーを定義する必要があります。

  <table>
  <colgroup>
  <col width="50%" />
  <col width="50%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">値</th>
  <th align="left">説明</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p>ms_switch_capture</p></td>
  <td align="left"><p>NDIS 6.30 以降、ドライバーは、HYPER-V 拡張可能スイッチ ドライバー スタックのパケット トラフィックを監視するをキャプチャします。 カスタム ドライバー スタックの次のフィルター ドライバーには、このクラスが存在します。</p>
  <p>このクラスのドライバーの詳細については、<a href="capturing-extensions.md" data-raw-source="[Capturing Extensions](capturing-extensions.md)">キャプチャ拡張機能</a>を参照してください。</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p>ms_switch_filter</p></td>
  <td align="left"><p>NDIS 6.30 以降では、フィルター ドライバーはパケット トラフィックをフィルター処理しポートを適用するか、拡張可能スイッチ ドライバー スタックを通じてパケット配信ポリシーを切り替えます。 フィルター ドライバーのこのクラスの下にある<strong>ms_switch_capture</strong>スタックのドライバーです。</p>
  <p>このクラスのドライバーの詳細については、<a href="filtering-extensions.md" data-raw-source="[Filtering Extensions](filtering-extensions.md)">拡張機能のフィルタ リング</a>を参照してください。</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p>ms_switch_forward</p></td>
  <td align="left"><p>NDIS 6.30 以降は、同じドライバーのフィルターの実行を転送するフィルター ドライバーとして機能します。 転送のドライバーは、ポートと拡張可能スイッチの間のパケットを転送することも。 フィルター ドライバーのこのクラスの下にある<strong>ms_switch_filter</strong>スタックのドライバーです。</p>
  <p>このクラスのドライバーの詳細については、<a href="forwarding-extensions.md" data-raw-source="[Forwarding Extensions](forwarding-extensions.md)">転送拡張機能</a>を参照してください。</p></td>
  </tr>
  </tbody>
  </table>



- ドライバーのバインディングを制御するため、フィルター ドライバーの INF ファイルが変更では、次のエントリを定義する必要があります。

  ```INF
  HKR, Ndi\Interfaces,UpperRange,,"noupper"
  HKR, Ndi\Interfaces,LowerRange,,"nolower"
  HKR, Ndi\Interfaces, FilterMediaTypes,,"ethernet"
  ```

  ドライバーのバインディングを制御する方法の詳細については、[フィルター ドライバーのバインドのリレーションシップの指定](specifying-filter-driver-binding-relationships.md)を参照してください。

- 変更フィルター INF ファイルには、ドライバーと特定のアダプターに関連付けられているパラメーターの共通のパラメーター定義を指定する必要があります。 次の例では、いくつかの一般的なパラメーター定義を示します。
  ```INF
  [Common.Params.reg]

  HKR, FilterDriverParams\DriverParam,  ParamDesc, , "Driverparam for lwf"
  HKR, FilterDriverParams\DriverParam,  default, , "5"
  HKR, FilterDriverParams\DriverParam,  type,  , "int"

  HKR, FilterAdapterParams\AdapterParam,  ParamDesc, , "Adapterparam for lwf"
  HKR, FilterAdapterParams\AdapterParam,  default, , "10"
  HKR, FilterAdapterParams\AdapterParam,  type,  , "int"
  ```









