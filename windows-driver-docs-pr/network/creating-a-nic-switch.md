---
title: NIC スイッチの作成
description: NIC スイッチの作成
ms.assetid: 5A184EBD-95F4-4C11-AACD-49DF04578CA0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ff47db9ba34ed09ae834397eae554c7aa63ebca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571961"
---
# <a name="creating-a-nic-switch"></a>NIC スイッチの作成


このセクションでは、要件とシングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの NIC のスイッチを作成するためのガイドラインについて説明します。 PCI Express (PCIe) 物理機能 (PF)、SR-IOV ネットワーク アダプターのミニポート ドライバーでは、作成し、アダプターで NIC スイッチを構成します。

NIC スイッチは、次のメソッドのいずれかで作成できます。

<a href="" id="static-creation"></a>静的な作成  
NIC のスイッチは、一連のレジストリ設定によって定義されているスイッチ パラメーターを使用して、SR-IOV ネットワーク アダプターに静的に作成されます。 NIC のスイッチを作成すると後、は、ドライバーの実行中にそのパラメーターを変更できません。

PF のミニポート ドライバーがドライバーへの呼び出しのコンテキスト内で NIC スイッチを静的に作成[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 NDIS のオブジェクト識別子 (OID) メソッド要求の発行されるまでに NIC スイッチを使用することはできませんただし、 [OID\_NIC\_切り替える\_作成\_切り替える](https://msdn.microsoft.com/library/windows/hardware/hh451815)します。 NIC スイッチを以前に作成した場合でも PF ミニポート ドライバーは、この OID 要求を処理するときに、NIC スイッチは、使用が有効になります。

この方法の詳細については、[NIC スイッチの作成を静的](static-creation-of-a-nic-switch.md)を参照してください。

<a href="" id="dynamic-creation"></a>動的な作成  
NIC のスイッチがの OID メソッド要求を通じて、SR-IOV ネットワーク アダプターに動的に作成された[OID\_NIC\_スイッチ\_作成\_切り替える](https://msdn.microsoft.com/library/windows/hardware/hh451815)します。 この OID 要求を通じて NIC スイッチ パラメーターを定義する、 [ **NDIS\_NIC\_切り替える\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体。 これらのパラメーターは、staticallydefined レジストリ設定にも基づいていますが、ミニポート ドライバーの実行中に動的に変更できます。

この方法の詳細については、[NIC スイッチの動的な作成](dynamic-creation-of-a-nic-switch.md)を参照してください。

詳細を処理する方法について、 [OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)要求を参照してください[OID 処理\_NIC\_スイッチ\_作成\_スイッチ要求](handling-the-oid-nic-switch-create-switch-request.md)します。

ネットワーク アダプターの SR-IOV NIC スイッチの詳細については、[NIC スイッチ](nic-switches.md)を参照してください。

**注**  の PCIe 仮想機能 (VF)、SR-IOV ネットワーク アダプターのミニポート ドライバーが作成または NIC スイッチなどのネットワーク アダプターのハードウェア リソースを構成していません。 詳細については、[書き込み SR-IOV VF ミニポート ドライバー](writing-sr-iov-vf-miniport-drivers.md)を参照してください。

 

 

 





