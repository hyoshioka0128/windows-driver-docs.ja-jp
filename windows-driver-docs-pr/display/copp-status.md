---
title: COPP 状態
description: COPP 状態
ms.assetid: bec8f6b6-17d0-4797-9898-add0629cba4d
keywords:
- WDK COPP、状態の保護をコピーします。
- ビデオのコピー防止 WDK COPP、状態
- COPP WDK DirectX va なので、状態
- ビデオの WDK COPP、状態の保護
- WDK COPP のステータス情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92185cabe1807de07d84ebb32d87232bc0704400
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370268"
---
# <a name="copp-status"></a>COPP 状態


## <span id="ddk_copp_status_gg"></span><span id="DDK_COPP_STATUS_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

ビデオのミニポート ドライバーでは、DirectX VA COPP デバイスに関連付けられた物理コネクタで COPP 状態の要求を受信できます。

ビデオのミニポート ドライバーの[ *COPPQueryStatus* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)関数へのポインターを渡される、 [ **DXVA\_COPPStatusInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusinput)要求を格納する構造体。 *COPPQueryStatus*にステータスを書き込みます、 [ **DXVA\_COPPStatusOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusoutput)構造体、 *pOutput*パラメーター ポイント。 **GuidStatusRequestID**と**StatusData**の DXVA メンバー\_COPPStatusInput 状態要求を指定します。 ビデオのミニポート ドライバーによっては、要求へのポインターにステータス情報をキャストする必要が、 [ **DXVA\_COPPStatusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusdata)、 [ **DXVA\_COPPStatusDisplayData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusdisplaydata)、 [ **DXVA\_COPPStatusHDCPKeyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)、または[ **DXVA\_COPPStatusSignalingCmdData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatussignalingcmddata)構造体。 ビデオのミニポート ドライバーに状態情報をコピーする必要があります、 **COPPStatus**配列メンバーの DXVA\_COPPStatusOutput します。

**注**  ドライバーで 1 回使用される 128 ビットのランダムな数値を返す必要があります、 **rApp**の DXVA メンバー\_COPPStatusData、DXVA\_COPPStatusDisplayData、DXVA\_COPPStatusHDCPKeyData、または DXVA\_COPPStatusSignalingCmdData します。 128 ビットのランダムな数値が、送信元アプリケーションによって生成され、記載されて、 **rApp**の DXVA メンバー\_COPPStatusInput します。

 

ドライバーには、次の状態データを指定された要求が返されます。

-   DXVA の\_COPPQueryProtectionType 設定**guidStatusRequestID**で何も設定と**StatusData**で、次の値の論理和有効な組み合わせを返します、  **。指定**の DXVA メンバー\_COPP デバイスに関連付けられた物理コネクタでの保護メカニズムの使用可能な型を示す COPPStatusData:
    -   COPP\_ProtectionType\_不明
    -   COPP\_ProtectionType\_なし
    -   COPP\_ProtectionType\_HDCP
    -   COPP\_ProtectionType\_ACP
    -   COPP\_ProtectionType\_CGMSA
-   DXVA の\_COPPQueryConnectorType 設定**guidStatusRequestID**で何も設定と**StatusData**で、次のいずれかの値を返します、**指定**メンバーの DXVA\_COPPStatusData ビデオ セッションを使用して物理コネクタの種類を識別します。

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

    ドライバーでは、COPP を組み合わせることができますも\_ConnectorType\_グラフィックス アダプターとディスプレイ モニター間の接続が永続的であることを示す前述のコネクタの種類の値のいずれかの内部 (0x80000000) 値および notユーザーによるエンクロージャの外部からアクセスできます。

-   DXVA の\_COPPQueryLocalProtectionLevel または DXVA\_COPPQueryGlobalProtectionLevel 設定**guidStatusRequestID**で保護の種類を設定および**StatusData**、保護レベル値を返します、**指定**の DXVA メンバー\_COPPStatusData します。 可能な保護レベルは、次を参照してください。 [COPP コマンド](copp-commands.md)します。 DXVA\_COPPQueryLocalProtectionLevel 要求を現在設定されている返しますビデオ セッションの保護レベル。 DXVA\_COPPQueryGlobalProtectionLevel 要求を現在設定されている返します物理コネクタの保護レベル。

    COPP 状態のクエリがビデオのミニポート ドライバーが一部を取得を要求しても情報を拡張します。

-   DXVA の\_COPPQueryBusData 設定**guidStatusRequestID**とでは nothing **StatusData**で、次のいずれかの値を返します、**指定**のメンバーDXVA\_COPPStatusData グラフィックス ハードウェアで使用されるバスの種類を識別します。

    -   COPP\_BusType\_不明
    -   COPP\_BusType\_PCI
    -   COPP\_BusType\_PCIX
    -   COPP\_BusType\_PCIExpress
    -   COPP\_BusType\_AGP

    ドライバーでは、COPP を組み合わせることができますのみ\_BusType\_がないグラフィックス アダプターとその他のサブシステムの間のコマンドおよびステータス インターフェイス シグナルの場合、前述のバスの種類の値のいずれかの (0x80000000) の値を統合公開されている仕様と標準コネクタの種類を使用する拡張バスで使用できます。 メモリ バスは、この定義から除外されます。

-   DXVA の\_COPPQueryDisplayData 設定**guidStatusRequestID**で何も設定と**StatusData**、情報が返されます、 [ **DXVA\_COPPStatusDisplayData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusdisplaydata) DirectX VA COPP デバイスに関連付けられているコネクタ経由で送信される信号の表示モードを記述する構造体。

-   DXVA の\_COPPQueryHDCPKeyData 設定**guidStatusRequestID**で何も設定と**StatusData**、情報が返されます、 [ **DXVA\_COPPStatusHDCPKeyData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatushdcpkeydata)高帯域幅デジタル コンテンツの保護 (HDCP) キーの選択範囲ベクター (KSV) を記述する構造体。

-   DXVA の\_COPPQuerySignaling 設定**guidStatusRequestID**で何も設定と**StatusData**、情報が返されます、 [ **DXVA\_COPPStatusSignalingCmdData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatussignalingcmddata) DirectX VA COPP デバイスに関連付けられた物理コネクタを通過する信号を保護する方法を記述する構造体。

    COPP 状態のクエリがビデオのミニポート ドライバーが一部を取得を要求しても情報を拡張します。

 

 





