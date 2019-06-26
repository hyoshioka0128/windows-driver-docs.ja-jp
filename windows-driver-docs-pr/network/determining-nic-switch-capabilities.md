---
title: NIC スイッチ機能の判断
description: NIC スイッチ機能の判断
ms.assetid: 5E627E52-2D47-4EA0-80D9-6979891CCE96
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbed439d7678b69f98f3436ceb2db240e72b6fd9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381416"
---
# <a name="determining-nic-switch-capabilities"></a>NIC スイッチ機能の判断


このトピックでは、NDIS および上にあるドライバーを NIC はスイッチ シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの機能を特定する方法について説明します。 このトピックの内容は次のとおりです。

[レポートの中に NIC のスイッチ機能*MiniportInitializeEx*](#reporting-nic-switch-capabilities-during-miniportinitializeex)

[上にあるドライバーによって NIC スイッチ機能の照会](#querying-nic-switch-capabilities-by-overlying-drivers)

**注**  専用の PCI Express (PCIe) 物理機能 (PF)、SR-IOV ネットワーク アダプターのミニポート ドライバーは、NIC のスイッチ機能を報告できます。 PCIe 仮想機能 (Vf) 用のミニポート ドライバーでは、NIC スイッチの SR-IOV 対応のアダプターの機能は報告する必要があります。

 

NIC のスイッチの詳細については、次を参照してください。 [NIC スイッチ](nic-switches.md)します。

## <a name="reporting-nic-switch-capabilities-during-miniportinitializeex"></a>レポートの中に NIC のスイッチ機能*MiniportInitializeEx*


NDIS のミニポート ドライバーの呼び出したときに[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数の場合、ドライバーには、次の NIC はスイッチ機能。

-   NIC のハードウェア機能の完全なセットは、ネットワーク アダプターをサポートできることを切り替えます。

    **注**  NDIS 6.30 以降、1 つだけの NIC のスイッチを作成、ネットワーク アダプター。 このスイッチと呼ばれる、*既定 NIC スイッチ*します。     

-   NIC は、ネットワーク アダプターで現在有効になっている機能を切り替えます。

ミニポート ドライバーを通じて基になるネットワーク アダプターの NIC スイッチ ハードウェア機能の報告、 [ **NDIS\_NIC\_切り替える\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)次のように初期化されている構造体。

1.  ミニポート ドライバーを初期化します、**ヘッダー**メンバー。 ドライバーのセット、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。

    NDIS 6.30 以降、ミニポート ドライバーの設定、**リビジョン**のメンバー**ヘッダー** NDIS に\_NIC\_スイッチ\_機能\_リビジョン\_2 と**サイズ**NDIS メンバー\_SIZEOF\_NIC\_スイッチ\_機能\_リビジョン\_2。

2.  ミニポート ドライバーでは、適切なフラグを設定、 **NicSwitchCapabilities**のメンバー、 [ **NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities) 、SR-IOV ネットワーク アダプターの NIC のスイッチ機能の構造体。 たとえば、ミニポート ドライバーは、NDIS を設定します\_NIC\_スイッチ\_CAP\_1 秒あたり\_VPORT\_INTERRUPT\_モデレート\_サポートされているフラグ NIC。スイッチは、各仮想ポート (VPort) スイッチで作成される割り込み節度をサポートしています。

3.  ミニポート ドライバーの設定の他のメンバー、 [ **NDIS\_NIC\_切り替える\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities) NIC のスイッチ機能の値の範囲の構造体SR-IOV ネットワーク アダプター。 たとえば、ミニポート ドライバーの設定、 **MaxNumVFs**と**MaxNumVPorts** Vf とアダプターをサポートする拡張の最大数をメンバー。

    **注**  ネットワーク アダプターで使用可能なハードウェア リソースに応じて、ミニポート ドライバーを設定できます、 **MaxNumVFs**メンバーである値をより小さい、  **\*NumVFs**キーワード。 このキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

     

NDIS のミニポート ドライバーの呼び出したときに[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数の場合、ドライバーは次の手順に従って、ネットワーク アダプターの NIC のスイッチ機能に登録します。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

    ミニポート ドライバーのセット、 **HardwareNicSwitchCapabilities**前に初期化されたへのポインターをメンバー [ **NDIS\_NIC\_スイッチ\_機能** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体。

    場合のレジストリ設定、  **\*SRIOV** INF キーワードは、1 つの値を持つ、ネットワーク アダプターが NIC スイッチの作成と構成の現在有効になります。 ミニポート ドライバーのセット、 **CurrentNicSwitchCapabilities**同じへのポインターをメンバー [ **NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体。

    場合のレジストリ設定、  **\*SRIOV** INF キーワードが 0 の値を持つ、NIC のスイッチの作成と構成のネットワーク アダプターが現在有効されません。 ミニポート ドライバーを設定する必要があります、 **CurrentNicSwitchCapabilities**メンバーを NULL にします。

    詳細については、  **\*SRIOV** INF キーワードを参照してください[SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

2.  ドライバー呼び出し[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)設定と、 *MiniportAttributes*パラメーターへのポインターを[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)構造体。

アダプターの初期化プロセスの詳細については、次を参照してください。[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。

## <a name="creating-a-nic-switch-without-sr-iov"></a>なし、SR-IOV NIC スイッチの作成

ミニポート ドライバー NDIS 6.60 以降は、SR-IOV が有効でない場合、NIC スイッチおよび VMQ 機能の共存の次の要件に従う必要があります。 SR-IOV が有効にすると、ミニポート ドライバーが前のセクションでは、既存の要件に従う必要があります。

- ミニポート ドライバーでは、NIC のスイッチと VMQ 機能の両方をアドバタイズします。
- NIC は、NIC のスイッチと、NIC を再起動しなくても VMQ モード間で切り替えることができます。
    - NIC は、最初に起動するときに、どちらのモード (NIC スイッチの作成または VMQ キューの作成) する準備ができます。
        - NIC のスイッチを作成すると、任意の後続の VMQ キュー割り当てコールバックをミニポートが失敗します。
        - VMQ キューを最初に作成すると、ミニポート ドライバーは VMQ キューの割り当てが成功するし、NIC スイッチ割り当て呼び出しに失敗します。
    - NIC のスイッチが削除されるか、VMQ のすべてのキューが削除された、ミニポート ドライバー初期状態に戻り、もう一度これらのモードのいずれかに移動する準備ができました。

NIC のスイッチを作成できること、SR-IOV を使用せず、ミニポート ドライバーを提供する設定、 **NDIS_NIC_SWITCH_CAPS_NIC_SWITCH_WITHOUT_IOV_SUPPORTED**フラグ、 **NicSwitchCapabilities**メンバー、 [ **NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体。

## <a name="querying-nic-switch-capabilities-by-overlying-drivers"></a>上にあるドライバーによって NIC スイッチ機能の照会


NDIS パス、ネットワーク アダプターの次のように、ネットワーク アダプターにバインドされるドライバーに関連する NIC のスイッチ機能が現在有効。

-   NDIS が上にあるフィルター ドライバーを呼び出すときに[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)関数、NDIS 渡しますネットワーク アダプターの NIC のスイッチ機能を通じて、 *AttachParameters*パラメーター。 このパラメーターにはへのポインターが含まれています、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体。 **NicSwitchCapabilities**この構造体のメンバーにはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体。

-   NDIS が上位のプロトコル ドライバーを呼び出すときに[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数、NDIS 渡しますネットワーク アダプターの NIC のスイッチ機能を通じて、 *BindParameters*パラメーター。 このパラメーターにはへのポインターが含まれています、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)構造体。 **NicSwitchCapabilities**この構造体のメンバーにはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体。

NDIS も返されます、 [ **NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)のオブジェクト識別子 (OID) のクエリ要求を処理する場合に構造体[OID\_NIC\_スイッチ\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-hardware-capabilities)と[OID\_NIC\_スイッチ\_現在\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-current-capabilities)関連プロトコルまたはフィルター ドライバーによって発行されます。

 

 





