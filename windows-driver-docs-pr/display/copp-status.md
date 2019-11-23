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

ビデオミニポートドライバーの[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)関数は、要求を含む[**DXVA\_COPPStatusInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)構造体へのポインターを渡します。 *COPPQueryStatus*は、 *poutput*パラメーターが指す[**DXVA\_coppstatusoutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)構造体に状態を書き込みます。 DXVA\_COPPStatusInput の**Guidstatusrequestid**および**statusdata**メンバーは、状態要求を指定します。 要求に応じて、ビデオミニポートドライバーは、ステータス情報を[**DXVA\_COPPStatusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdata)、 [**DXVA\_COPPStatusDisplayData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdisplaydata)、 [**DXVA\_Coppstattordcpkeydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)、または[**DXVA\_coppstatussignalingcmddata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatussignalingcmddata)構造体へのポインターにキャストする必要があります。 ビデオミニポートドライバーは、DXVA\_COPPStatusOutput の**coppstatus**配列メンバーに状態情報をコピーする必要があります。

   ドライバーは、DXVA\_COPPStatusData、DXVA\_COPPStatusDisplayData、DXVA\_Coppstattordcpkeydata、または DXVA\_COPPStatusSignalingCmdData の**rApp**メンバーで1回使用された128ビット乱数を返す必要がある**ことに注意**してください。 128ビットの乱数は、送信アプリケーションによって生成され、DXVA\_COPPStatusInput の**rApp**メンバーに指定されました。

 

ドライバーは、指定された要求に対して次の状態データを返します。

-   **Guidstatusrequestid**で set DXVA\_COPPQueryProtectionType を設定し、 **statusdata**に何も設定しない場合は、copp デバイスに関連付けられている物理コネクタで使用できる種類の保護メカニズムを示す DXVA\_Coppstatusdata の**dwdata**メンバーの次の値の有効な論理和の組み合わせを返します。
    -   COPP\_ProtectionType\_不明
    -   COPP\_ProtectionType\_None
    -   COPP\_ProtectionType\_HDCP
    -   \_ProtectionType\_ACP
    -   COPP\_ProtectionType\_CGMSA
-   DXVA\_COPPQueryConnectorType が**Guidstatusrequestid**で設定され、 **statusdata**に何も設定されていない場合は、ビデオセッションで使用される物理コネクタの種類を識別する DXVA\_Coppstatusdata の**dwdata**メンバーの次のいずれかの値を返します。

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

    また、ドライバーは、COPP\_ConnectorType\_Internal (0x80000000) 値を上記のいずれかのコネクタ型の値と結合して、グラフィックスアダプターとディスプレイモニター間の接続が永続的であり、ユーザーが使用できないエンクロージャの外部からアクセスできないことを示します。

-   DXVA\_COPPQueryLocalProtectionLevel または DXVA\_、 **Guidstatusrequestid**で設定された Coppquerylocalprotectionlevel と**statusdata**に設定されている保護の種類によって、DXVA\_Coppstatusdata の**dwdata**メンバーの保護レベルの値が返されます。 可能な保護レベルについては、「 [Copp コマンド](copp-commands.md)」を参照してください。 DXVA\_COPPQueryLocalProtectionLevel 要求では、ビデオセッションに現在設定されている保護レベルが返されます。 DXVA\_COPPQueryGlobalProtectionLevel 要求では、物理コネクタに現在設定されている保護レベルが返されます。

    また、COPP status クエリを実行すると、ビデオミニポートドライバーがいくつかの拡張情報を取得するように要求する場合もあります。

-   DXVA\_**Copstatusrequestid**の場合は DXVA、 **statusdata**では nothing の場合は、グラフィックスハードウェアで使用されるバスの種類を識別する\_Coppstatusdata の**dwdata**メンバーの次のいずれかの値を返します。

    -   COPP\_BusType\_不明
    -   COPP\_BusType\_PCI
    -   COPP\_BusType\_PCIX
    -   COPP\_BusType\_PCIExpress
    -   COPP\_BusType\_AGP

    ドライバーは、一般公開されている仕様と標準コネクタの種類を使用する拡張バスで、グラフィックスアダプターとその他のサブシステムの間にコマンドおよび状態インターフェイスの信号が使用できない場合に、COPP\_BusType\_Integrated (0x80000000) 値を、上記のいずれかのバス型値と結合することができます。 メモリバスは、この定義から除外されます。

-   **Guidstatusrequestid**の DXVA\_COPPQueryDisplayData Set と**statusdata**に何も設定されていない場合は、DirectX VA copp デバイスに関連付けられているコネクタを介して送信される信号の表示モードを示す[**DXVA\_coppquerydisplaydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusdisplaydata)構造体に情報を返します。

-   **Guidstatusrequestid**の DXVA\_COPPQueryHDCPKeyData Set と**statusdata**に何も設定されていない場合は、高帯域幅のデジタル Content Protection (HDCP) キー選択ベクター (ksv) を記述する[**DXVA\_Coppstattordcpkeydata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)構造体に情報を返します。

-   DXVA\_**Copstatusrequestid**で設定され、 **statusdata**に何も設定されていない場合は、DirectX VA copp デバイスに関連付けられている物理コネクタを通過する信号が保護される方法を記述する[**DXVA\_COPPStatusSignalingCmdData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatussignalingcmddata)構造体に情報を返します。

    また、COPP status クエリを実行すると、ビデオミニポートドライバーがいくつかの拡張情報を取得するように要求する場合もあります。

 

 





