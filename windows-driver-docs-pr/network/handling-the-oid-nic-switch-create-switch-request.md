---
title: OID_NIC_SWITCH_CREATE_SWITCH の要求を処理
description: OID_NIC_SWITCH_CREATE_SWITCH の要求を処理
ms.assetid: 5C0BC300-8904-483A-A66B-8F5CFE0829B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26b58f98abeabce480002a6e1b10d6739a506407
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532367"
---
# <a name="handling-the-oidnicswitchcreateswitch-request"></a>OID の処理\_NIC\_スイッチ\_作成\_切り替え要求


オブジェクト識別子 (OID) メソッド要求を発行する NDIS [OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)以下を実行します。

-   静的に作成された、ミニポート ドライバーでの PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターで NIC スイッチを有効にします。 PF は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターのハードウェア コンポーネントです。

    呼び出しにコンテキスト内から PF のミニポート ドライバーによって NIC スイッチが作成される静的に[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)します。 ドライバーは、リソースが割り当てられ、レジストリ設定から読み取るパラメーターに基づいて、スイッチを作成します。

-   動的にネットワーク アダプターで NIC スイッチを作成します。

    PF のミニポート ドライバーが静的にサポートしていない場合は、NIC はスイッチの作成、ミニポート ドライバーがリソースの割り当てし、OID 要求で指定されたパラメーターに基づいて、スイッチを作成します。

NDIS ドライバーを呼び出すときに、PF ミニポート ドライバーが SR-IOV インターフェイスのサポートをアドバタイズ[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 PF のミニポート ドライバーが SR-IOV をサポートする場合、NDIS は、レジストリから NIC スイッチの構成を読み取ります。 NDIS の OID メソッド要求を発行する前に[OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)NDIS の書式、PF ミニポート ドライバーを[ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体に次のようにレジストリ情報。

-   NDIS セット、 **SwitchType** NIC スイッチの型にメンバー。

    Windows Server 2012 以降、Windows のみをサポートするスイッチの種類の**NdisNicSwitchTypeExternal**します。 外部スイッチでは、この種類のスイッチに接続されている仮想ポート (拡張) が物理ネットワーク アダプターのポートを介して外部ネットワークをアクセスできることを指定します。

    NIC のスイッチの詳細については、次を参照してください。 [SR-IOV アーキテクチャ](sr-iov-architecture.md)します。

-   NDIS セット、 **SwitchId**メンバー NIC スイッチの id の値にします。 スイッチの識別子は、0 と、ネットワーク アダプターがサポートされているスイッチの数の整数です。 NDIS\_既定\_切り替える\_ID 値を既定の NIC スイッチを示します。

    **注**  以降 Windows Server 2012 では、SR-IOV インターフェイスに対してのみサポートして既定の NIC のスイッチ、ネットワーク アダプター。

     

-   NDIS セット、 **NumVFs**メンバー数を指定するスイッチ PCIe 仮想機能 (Vf)、NIC に割り当てることができます。

OID メソッド要求を受け取ったとき[OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)、PF ミニポート ドライバーは、次を実行する必要があります。

1.  NDIS を呼び出すときは、NIC スイッチを作成しますが、PF ミニポート ドライバーでは、静的スイッチの作成と構成をサポートする場合[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)します。 構成パラメーターを確認する必要があります、ドライバーは、この OID 要求を処理する場合、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体。 パラメーターが呼び出し中に、スイッチを作成する、ドライバーによって使用されるものと同じにする必要があります*MiniportInitializeEx*します。 True でない場合、ドライバーは、OID 要求を失敗する必要があります。

    詳細については、次を参照してください。 [NIC スイッチの作成を静的](static-creation-of-a-nic-switch.md)します。

2.  ドライバーの構成値を検証する必要があります、PF ミニポート ドライバーでは、動的なスイッチの作成と構成をサポートする場合、 [ **NDIS\_NIC\_切り替える\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体し、これらの値に基づいて、NIC のスイッチを作成します。

    詳細については、次を参照してください。 [NIC スイッチの動的な作成](dynamic-creation-of-a-nic-switch.md)です。

3.  PF ミニポート ドライバーでは、NIC のスイッチの既定 VPort のために必要なハードウェアおよびソフトウェア リソースを割り当てる必要があります。

    **注**  VPort がの OID 要求を使って作成された常に既定[OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)OID を削除要求の[OID\_NIC\_スイッチ\_削除\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451817)します。 OID 要求[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)と[OID\_NIC\_スイッチ\_DELETE\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)作成と NIC のスイッチの拡張を既定以外の削除に使用されます。

     

4.  呼び出して、スイッチの SR-IOV 仮想化を有効にする必要があります動的スイッチの作成と構成をサポートしている PF ミニポート ドライバー [ **NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481)します。 この呼び出しを構成、 **NumVFs**メンバーと**VF 有効**アダプターの構成領域の PCI Express (PCIe) の SR-IOV 拡張機能の構造内のビットします。

    SR-IOV 構成領域の詳細については、PCI SIG を参照してください。[シングル ルート I/O 仮想化および共有 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)仕様。

    **注**  スイッチを作成した後は、SR-IOV 仮想化を有効に、PF ミニポート ドライバーでは、静的スイッチの作成をサポートする場合と[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)が呼び出されます.

     

かどうか、PF ミニポート ドライバーが正常が OID メソッド要求 OID の\_NIC\_スイッチ\_作成\_スイッチでは、次のようできます。

-   VFs を割り当てることができますの OID メソッド要求を通じて NIC スイッチ[OID\_NIC\_切り替える\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。

-   既定以外の拡張を作成することができますの OID メソッド要求を通じて NIC スイッチ[OID\_NIC\_切り替える\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。

    ミニポート ドライバーが既定以外の拡張のプールを管理する責任を負います。 ドライバーは、そのプールで既定以外の拡張の数を指定を通じて、 **NumVPorts**のメンバー、 [ **NDIS\_NIC\_スイッチ\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451582)構造体。 ドライバーの OID クエリ要求をこの構造体を返します[OID\_NIC\_スイッチ\_ENUM\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451819)します。

    **注**  ネットワーク アダプターは、PF. のプールから既定 VPort を常に作成する必要があります

     

 

 





