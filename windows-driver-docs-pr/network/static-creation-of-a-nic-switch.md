---
title: NIC スイッチの静的作成
description: NIC スイッチの静的作成
ms.assetid: F325B1F8-7655-4044-AF04-32B434574082
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 707521bf455cc965a666460a6925ef4219936991
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376762"
---
# <a name="static-creation-of-a-nic-switch"></a>NIC スイッチの静的作成


シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターは、NIC のスイッチを作成できる必要があります。 一部のアダプターでは、NIC のスイッチを作成できます静的にへの呼び出しのコンテキスト内で[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)します。

ミニポート ドライバーを PCI Express (PCIe) 物理機能 (PF) の SR-IOV 対応アダプターだけでは、アダプターで NIC スイッチを作成できます。

**注**  以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、 *NIC スイッチの既定*、NDIS によって参照されている\_既定\_スイッチ\_ID です。

 

既定の NIC のスイッチ パラメーターは、レジストリに標準化されたキーワードの設定を使用して定義されます。 これらのキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

PF のミニポート ドライバーは、NDIS ドライバーを呼び出すときに静的に NIC スイッチを作成[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 通常、ドライバーは、作成し、ネットワーク アダプターで SR-IOV を有効にする前に初期化シーケンスの一部として、NIC のスイッチを構成します。

静的に NIC のスイッチを作成し、への呼び出しのコンテキストでネットワーク アダプターで SR-IOV を有効にする場合、PF ミニポート ドライバーが次の手順を次[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize):

1.  PF のミニポート ドライバーには、SR-IOV が有効になっているかどうかを判断し、NIC のスイッチの構成パラメーターを取得する、SR-IOV が標準化されているキーワードを読み取る必要があります。

    **注**  PF ミニポート ドライバーのエントリ ポイントが登録されているかどうか、 [ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数の場合、ドライバー可能性がありますが取得したこれらのパラメーターから、NDIS が呼び出されたときに、レジストリ*MiniportSetOptions*します。

     

2.  SR-IOV が有効になっている場合、PF ミニポート ドライバーは、レジストリから NIC スイッチ パラメーターを使用してネットワーク アダプターを構成します。 ドライバーは、ネットワーク アダプターを構成する前に、パラメーターが有効であることを確認する必要があります。 たとえば、ミニポート ドライバーでは、NIC のスイッチに割り当てられる PCIe 仮想機能 (Vf) の最大数が、ネットワーク アダプターでサポートされている VFs の数を超えないようにする必要がありますを確認します。

3.  ミニポート ドライバー呼び出し[ **NdisMEnableVirtualization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization) SR-IOV を有効にし、ネットワーク アダプターで VFs の数を設定します。 この関数は、アダプターの PCI 構成領域で SR-IOV 対応の拡張機能を構成します。 この関数は、NDIS を返す場合\_状態\_成功した場合、SR-IOV が有効になっているし、VFs が、PCIe インターフェイスを介して公開されます。

**注**  NDIS のオブジェクト識別子 (OID) メソッド要求の発行されるまで、PF ミニポート ドライバーが静的に NIC のスイッチを作成した場合、スイッチは使用できません[OID\_NIC\_スイッチ\_作成\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)します。 PF のミニポート ドライバーが静的に NIC スイッチを作成する場合、OID 要求にスイッチ パラメーターを指定することを確認する必要があります。 これらのパラメーターに含まれるよう、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造 OID 要求に関連付けられていると同じである必要があります、パラメーターは、ドライバー、スイッチを作成するために使用します。

 

詳細を処理する方法について、 [OID\_NIC\_スイッチ\_作成\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)要求を参照してください[OID 処理\_NIC\_スイッチ\_作成\_スイッチ要求](handling-the-oid-nic-switch-create-switch-request.md)します。

PF のミニポート ドライバーの要件と初期化の順序の詳細については、次を参照してください。 [PF ミニポート ドライバーの初期化](initializing-a-pf-miniport-driver.md)します。

 

 





