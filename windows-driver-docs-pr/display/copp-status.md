---
title: COPP 状態
description: COPP 状態
ms.assetid: bec8f6b6-17d0-4797-9898-add0629cba4d
keywords:
- コピー防止 WDK COPP、状態
- ビデオコピー防止 WDK COPP、状態
- COPP WDK DirectX VA、状態
- 保護されたビデオ WDK COPP、状態
- 状態情報 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e26c0c3be928915a0edc074782d057186cddb5f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839035"
---
# <a name="copp-status"></a>COPP 状態


## <span id="ddk_copp_status_gg"></span><span id="DDK_COPP_STATUS_GG"></span>


このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

ビデオミニポートドライバーは、DirectX VA COPP デバイスに関連付けられている物理コネクタで、COPP ステータスの要求を受け取ることができます。

ビデオミニポートドライバーの[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)関数は、要求を含む[**DXVA\_COPPStatusInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)構造体へのポインターを渡します。 *COPPQueryStatus*は、 *poutput*パラメーターが指す[**DXVA\_coppstatusoutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)構造体に状態を書き込みます。 DXVA\_COPPStatusInput の**Guidstatusrequestid**および**statusdata**メンバーは、状態要求を指定します。 要求に応じて、ビデオミニポートドライバーは、 [**DXVA\_COPPStatusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdata)、 [**DXVA\_COPPStatusDisplayData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdisplaydata)、 [**DXVA\_Coppstattordcpkeydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)、または DXVA へのポインターに状態情報をキャストする必要があり[ **@no__% 11_ COPPStatusSignalingCmdData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatussignalingcmddata)構造体。 ビデオミニポートドライバーは、DXVA\_COPPStatusOutput の**coppstatus**配列メンバーに状態情報をコピーする必要があります。

   ドライバーは、DXVA\_COPPStatusData、DXVA\_COPPStatusDisplayData、DXVA\_Coppstattordcpkeydata、または DXVA の**rApp**メンバーで1回使用された128ビット乱数を返す必要がある**ことに注意**してください\_COPPStatusSignalingCmdData。 128ビットの乱数は、送信アプリケーションによって生成され、DXVA\_COPPStatusInput の**rApp**メンバーに指定されました。

 

ドライバーは、指定された要求に対して次の状態データを返します。

-   DXVA\_COPPQueryProtectionType が**Guidstatusrequestid**で設定され、 **statusdata**に何も設定されていない場合は、DXVA\_Coppstatusdata の**dwdata**メンバーで、次の値の有効な論理和の組み合わせを返します。COPP デバイスに関連付けられている物理コネクタで使用できる種類の保護メカニズム:
    -   COPP\_ProtectionType\_不明
    -   COPP\_ProtectionType\_None
    -   COPP\_ProtectionType\_HDCP
    -   \_ProtectionType\_ACP
    -   COPP\_ProtectionType\_CGMSA
-   DXVA\_COPPQueryConnectorType が**Guidstatusrequestid**に設定され、 **statusdata**に何も設定されていない場合は、物理の種類を識別する DXVA\_Coppstatusdata の**dwdata**メンバーの次のいずれかの値を返します。ビデオセッションで使用されるコネクタ:

    -   COPP\_ConnectorType\_不明
    -   COPP\_ConnectorType\_VGA
    -   COPP\_ConnectorType\_SVideo
    -   COPP\_ConnectorType\_CompositeVideo
    -   COPP\_ConnectorType\_ComponentVideo
    -   COPP\_ConnectorType\_DVI
    -   COPP\_ConnectorType\_HDMI
    -   COPP\_ConnectorType\_LVDS
    -   COPP\_ConnectorType\_TMDS
    -   COPP\_ConnectorType\_D\_JPN

    また、ドライバーは、COPP\_ConnectorType\_Internal (0x80000000) 値を上記のいずれかのコネクタの種類の値と組み合わせて、グラフィックスアダプターとディスプレイモニター間の接続が永続的で、アクセスできないことを示します。非ユーザーが保守するエンクロージャの外部から。

-   DXVA\_COPPQueryLocalProtectionLevel または DXVA\_、 **Guidstatusrequestid**で設定された Coppquerylocalprotectionlevel と**statusdata**に設定されている保護の種類によって、の**dwdata**メンバーの保護レベルの値が返されます。DXVA\_COPPStatusData。 可能な保護レベルについては、「 [Copp コマンド](copp-commands.md)」を参照してください。 DXVA\_COPPQueryLocalProtectionLevel 要求では、ビデオセッションに現在設定されている保護レベルが返されます。 DXVA\_COPPQueryGlobalProtectionLevel 要求では、物理コネクタに現在設定されている保護レベルが返されます。

    また、COPP status クエリを実行すると、ビデオミニポートドライバーがいくつかの拡張情報を取得するように要求する場合もあります。

-   DXVA\_**Copstatusrequestid**の場合は DXVA、 **statusdata**では nothing の場合は、グラフィックスによって使用されるバスの種類を識別する\_Coppstatusdata の**dwdata**メンバーの次のいずれかの値を返します。デバイス

    -   COPP\_BusType\_不明
    -   COPP\_BusType\_PCI
    -   COPP\_BusType\_PCIX
    -   COPP\_BusType\_PCIExpress
    -   COPP\_BusType\_AGP

    ドライバーは、グラフィックスアダプターとその他のサブシステムの間で使用可能なコマンドおよび状態インターフェイス信号がない場合に、COPP\_BusType\_Integrated (0x80000000) 値を、上記のいずれかのバス型の値と結合することができます。パブリックに使用可能な仕様と標準コネクタの種類を使用する拡張バス。 メモリバスは、この定義から除外されます。

-   DXVA\_**Copstatusrequestid**に設定され、 **statusdata**に何も設定されていない場合は、シグナルの表示モードを記述する[**DXVA\_coppquerydisplaydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdisplaydata)構造体に情報を返します。DirectX VA COPP デバイスに関連付けられているコネクタを介して送信されます。

-   DXVA\_**Copstatusrequestid**に設定され、 **statusdata**に何も設定されていない場合は、高帯域幅のデジタルコンテンツを記述する[**DXVA\_Coppstattordcpkeydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)構造体に情報を返します。保護 (HDCP) キー選択ベクター (KSV)。

-   DXVA\_**Copstatusrequestid**で設定され、 **statusdata**に何も設定されていない場合、 [**DXVA\_COPPStatusSignalingCmdData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatussignalingcmddata)構造体に情報を返します。このデータ構造では、DirectX VA COPP デバイスに関連付けられている物理コネクタは保護されています。

    また、COPP status クエリを実行すると、ビデオミニポートドライバーがいくつかの拡張情報を取得するように要求する場合もあります。

 

 





