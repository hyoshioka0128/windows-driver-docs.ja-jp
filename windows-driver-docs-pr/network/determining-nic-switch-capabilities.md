---
title: NIC スイッチ機能の判断
description: NIC スイッチ機能の判断
ms.assetid: 5E627E52-2D47-4EA0-80D9-6979891CCE96
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 798279568e9a5b5629eb075164bf8a6116229464
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834913"
---
# <a name="determining-nic-switch-capabilities"></a>NIC スイッチ機能の判断


このトピックでは、NDIS およびそれ以降のドライバーが、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターの NIC スイッチ機能をどのように決定するかについて説明します。 このトピックには、次の情報が含まれています。

[*MiniportInitializeEx*中の NIC スイッチ機能の報告](#reporting-nic-switch-capabilities-during-miniportinitializeex)

[それまでのドライバーによる NIC スイッチ機能のクエリ](#querying-nic-switch-capabilities-by-overlying-drivers)

**注**  sr-iov ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーのみが、NIC スイッチの機能を報告できます。 PCIe 仮想機能 (VFs) のミニポートドライバーは、SR-IOV アダプターの NIC スイッチ機能を報告しないようにする必要があります。

 

NIC スイッチの詳細については、「 [Nic スイッチ](nic-switches.md)」を参照してください。

## <a name="reporting-nic-switch-capabilities-during-miniportinitializeex"></a>*MiniportInitializeEx*中の NIC スイッチ機能の報告


NDIS がミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ドライバーは次の NIC スイッチ機能を提供します。

-   ネットワークアダプターがサポートできる NIC スイッチのハードウェア機能の完全なセット。

    **注**  NDIS 6.30 以降では、ネットワークアダプター上に1つの NIC スイッチのみが作成されます。 このスイッチは、既定の*NIC スイッチ*と呼ばれます。     

-   ネットワークアダプターで現在有効になっている NIC スイッチの機能。

ミニポートドライバーは、次の方法で初期化される[**NDIS\_nic\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の構造を通じて、基になるネットワークアダプターの nic スイッチのハードウェア機能を報告します。

1.  ミニポートドライバーは、**ヘッダー**メンバーを初期化します。 ドライバーは、**ヘッダー**の**type**メンバーを、既定\_\_型の NDIS\_OBJECT に設定します。

    NDIS 6.30 以降では、ミニポートドライバーは、**ヘッダー**の**リビジョン**メンバーを NDIS\_NIC\_スイッチ\_機能\_リビジョン\_2 および**SIZE**メンバーを ndis\_SIZEOF\_nic に設定します。\_スイッチ\_の機能\_リビジョン\_2。

2.  ミニポートドライバーは、 [**NDIS\_nic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の**NicSwitchCapabilities**メンバーの適切なフラグを、SR-IOV ネットワークアダプターの nic スイッチ機能に\_の機能構造\_切り替えます。 たとえば、ミニポートドライバーは、各仮想ポートでの割り込みモデレーションを NIC スイッチがサポートしている場合、NDIS\_NIC\_スイッチ\_CAP\_\_を設定します。VPort) を作成します。

3.  ミニポートドライバーは、 [**NDIS\_nic\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の構造体の他のメンバーを、sr-iov ネットワークアダプターの nic スイッチ機能の値の範囲に設定します。 たとえば、ミニポートドライバーは、アダプターがサポートできる VFs と VPorts の最大数に**Maxnumvfs**および**maxnumvports**メンバーを設定します。

    **注**  ネットワークアダプターの使用可能なハードウェアリソースによっては、ミニポートドライバーは、 **maxnumvfs**メンバーを **\*numvfs**キーワードよりも小さい値に設定できます。 このキーワードの詳細については、「sr-iov[用の標準化](standardized-inf-keywords-for-sr-iov.md)された INF キーワード」を参照してください。

     

NDIS がミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ドライバーは次の手順に従ってネットワークアダプターの NIC スイッチ機能を登録します。

1.  ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の構造を初期化します。

    ミニポートドライバーは、以前に初期化された[**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の構造体へのポインターに、**ハード**ドライブメンバーを設定します。

    **\*SRIOV** INF キーワードのレジストリ設定の値が1の場合、ネットワークアダプターは現在、NIC スイッチの作成と構成に対して有効になっています。 ミニポートドライバーは、 **CurrentNicSwitchCapabilities**メンバーを、同じ[**NDIS\_NIC\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造へのポインターに設定します。

    **\*SRIOV** INF キーワードのレジストリ設定の値が0の場合、ネットワークアダプターは現在、NIC スイッチの作成と構成に対して有効になっていません。 ミニポートドライバーでは、 **CurrentNicSwitchCapabilities**メンバーを NULL に設定する必要があります。

    **\*SRIOV** INF キーワードの詳細については、「sr-iov[用の標準化](standardized-inf-keywords-for-sr-iov.md)された inf キーワード」を参照してください。

2.  ドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出し、 *miniportattributes*パラメーターを[**NDIS\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)へのポインターに設定します。\_ハードウェア\_\_属性の構造をサポートします。

アダプター初期化プロセスの詳細については、「[ミニポートアダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

## <a name="creating-a-nic-switch-without-sr-iov"></a>Sr-iov を使用せずに NIC スイッチを作成する

NDIS 6.60 以降のミニポートドライバーは、SR-IOV が有効になっていない場合に、NIC スイッチと VMQ 機能を共存させるための次の要件に従う必要があります。 SR-IOV が有効になっている場合、ミニポートドライバーは、前のセクションの既存の要件に準拠している必要があります。

- ミニポートドライバーは、NIC スイッチと VMQ の両方の機能をアドバタイズします。
- Nic を再起動せずに nic スイッチと VMQ モードを切り替えることができます。
    - 最初に NIC が開始されると、いずれかのモード (NIC スイッチを作成するか、VMQ キューを作成するか) になります。
        - NIC スイッチが作成されると、ミニポートは、後続の VMQ キュー割り当てコールバックに失敗します。
        - VMQ キューが最初に作成された場合、ミニポートドライバーは VMQ キュー割り当てに成功し、NIC スイッチ割り当て呼び出しが失敗します。
    - NIC スイッチが削除されるか、すべての VMQ キューが削除されると、ミニポートドライバーが初期状態に戻り、これらのモードのいずれかに再度アクセスできるようになります。

SR-IOV を使用せずに NIC スイッチを作成できることを提供するために、ミニポートドライバーは、NDIS\_NIC の**NicSwitchCapabilities**メンバーの**NDIS_NIC_SWITCH_CAPS_NIC_SWITCH_WITHOUT_IOV_SUPPORTED**フラグを設定し[ **\_\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の構造を切り替えます。

## <a name="querying-nic-switch-capabilities-by-overlying-drivers"></a>それまでのドライバーによる NIC スイッチ機能のクエリ


NDIS は、ネットワークアダプターの現在有効な NIC スイッチ機能を、次のようにネットワークアダプターにバインドするドライバーに渡します。

-   NDIS が後続のフィルタードライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出すと、Ndis は*attachparameters*パラメーターを使用してネットワークアダプターの NIC スイッチ機能を渡します。 このパラメーターには、\_PARAMETERS 構造体を[**アタッチ\_ための NDIS\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)へのポインターが含まれています。 この構造体の**NicSwitchCapabilities**メンバーには、 [**NDIS\_NIC\_SWITCH\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体へのポインターが含まれています。

-   NDIS がプロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すと、Ndis は*bindparameters*パラメーターを使用してネットワークアダプターの NIC スイッチ機能を渡します。 このパラメーターには、\_PARAMETERS 構造体を[**アタッチ\_ための NDIS\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)へのポインターが含まれています。 この構造体の**NicSwitchCapabilities**メンバーには、 [**NDIS\_NIC\_SWITCH\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体へのポインターが含まれています。

また、NDIS は、オブジェクト識別子 (OID) のクエリ要求を処理するときに、 [**ndis\_nic\_スイッチ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)の構造を返します。これは、ハードウェア\_の機能および oid を\_[\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-hardware-capabilities)です。 [\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-current-capabilities)によって、プロトコルまたはフィルタードライバーによって発行された現在の\_機能\_ます。

 

 





