---
title: NIC スイッチの作成
description: NIC スイッチの作成
ms.assetid: 5A184EBD-95F4-4C11-AACD-49DF04578CA0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ba182278cb33356cb26de910487f48ec8721c22
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374940"
---
# <a name="creating-a-nic-switch"></a>NIC スイッチの作成


このセクションでは、要件とシングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの NIC のスイッチを作成するためのガイドラインについて説明します。 PCI Express (PCIe) 物理機能 (PF)、SR-IOV ネットワーク アダプターのミニポート ドライバーでは、作成し、アダプターで NIC スイッチを構成します。

NIC スイッチは、次のメソッドのいずれかで作成できます。

<a href="" id="static-creation"></a>静的な作成  
NIC のスイッチは、一連のレジストリ設定によって定義されているスイッチ パラメーターを使用して、SR-IOV ネットワーク アダプターに静的に作成されます。 NIC のスイッチを作成すると後、は、ドライバーの実行中にそのパラメーターを変更できません。

PF のミニポート ドライバーがドライバーへの呼び出しのコンテキスト内で NIC スイッチを静的に作成[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 NDIS のオブジェクト識別子 (OID) メソッド要求の発行されるまでに NIC スイッチを使用することはできませんただし、 [OID\_NIC\_切り替える\_作成\_切り替える](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)します。 NIC スイッチを以前に作成した場合でも PF ミニポート ドライバーは、この OID 要求を処理するときに、NIC スイッチは、使用が有効になります。

この方法の詳細については、次を参照してください。 [NIC スイッチの作成を静的](static-creation-of-a-nic-switch.md)します。

<a href="" id="dynamic-creation"></a>動的な作成  
NIC のスイッチがの OID メソッド要求を通じて、SR-IOV ネットワーク アダプターに動的に作成された[OID\_NIC\_スイッチ\_作成\_切り替える](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)します。 この OID 要求を通じて NIC スイッチ パラメーターを定義する、 [ **NDIS\_NIC\_切り替える\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体。 これらのパラメーターは、staticallydefined レジストリ設定にも基づいていますが、ミニポート ドライバーの実行中に動的に変更できます。

この方法の詳細については、次を参照してください。 [NIC スイッチの動的な作成](dynamic-creation-of-a-nic-switch.md)です。

詳細を処理する方法について、 [OID\_NIC\_スイッチ\_作成\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)要求を参照してください[OID 処理\_NIC\_スイッチ\_作成\_スイッチ要求](handling-the-oid-nic-switch-create-switch-request.md)します。

ネットワーク アダプターの SR-IOV NIC スイッチの詳細については、次を参照してください。 [NIC スイッチ](nic-switches.md)します。

**注**  の PCIe 仮想機能 (VF)、SR-IOV ネットワーク アダプターのミニポート ドライバーが作成または NIC スイッチなどのネットワーク アダプターのハードウェア リソースを構成していません。 詳細については、次を参照してください。[書き込み SR-IOV VF ミニポート ドライバー](writing-sr-iov-vf-miniport-drivers.md)します。

 

 

 





