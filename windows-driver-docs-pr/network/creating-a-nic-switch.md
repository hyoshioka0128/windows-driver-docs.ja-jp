---
title: NIC スイッチの作成
description: NIC スイッチの作成
ms.assetid: 5A184EBD-95F4-4C11-AACD-49DF04578CA0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f6e183eb75ffdf0fa90329a3cb4837f76b972a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835035"
---
# <a name="creating-a-nic-switch"></a>NIC スイッチの作成


このセクションでは、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターの NIC スイッチを作成するための要件とガイドラインについて説明します。 SR-IOV ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーは、アダプターに NIC スイッチを作成して構成します。

NIC スイッチは、次のいずれかの方法で作成できます。

<a href="" id="static-creation"></a>静的作成  
NIC スイッチは、レジストリ設定によって定義されたスイッチパラメーターのセットを使用して、sr-iov ネットワークアダプターで静的に作成されます。 NIC スイッチを作成した後は、ドライバーの実行中にそのパラメーターを変更することはできません。

PF ミニポートドライバーは、ドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数への呼び出しのコンテキスト内で NIC スイッチを静的に作成します。 ただし、NDIS がオブジェクト識別子 (OID) メソッド要求を Oid に発行するまで、NIC スイッチを使用することはできません[\_nic\_スイッチ\_作成\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)。 NIC スイッチが既に作成されている場合でも、PF ミニポートドライバーは、この OID 要求を処理するときに使用するために、NIC スイッチを有効にしました。

この方法の詳細については、「 [NIC スイッチの静的作成](static-creation-of-a-nic-switch.md)」を参照してください。

<a href="" id="dynamic-creation"></a>動的作成  
NIC スイッチは、 [\_スイッチ\_作成する oid\_nic\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)の oid メソッド要求を通じて、sr-iov ネットワークアダプターに動的に作成されます。 この OID 要求では、 [**NDIS\_nic\_スイッチ\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造体を使用して、nic スイッチパラメーターを定義します。 これらのパラメーターは、staticdefined で定義されたレジストリ設定に基づいていますが、ミニポートドライバーの実行中に動的に変更することもできます。

この方法の詳細については、「 [NIC スイッチの動的作成](dynamic-creation-of-a-nic-switch.md)」を参照してください。

[Oid\_nic\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)を処理する方法の詳細については\_\_スイッチ要求の作成に関する詳細については、「 [oid\_Nic\_を処理](handling-the-oid-nic-switch-create-switch-request.md)する\_スイッチ要求を作成する」を参照してください。

Sr-iov ネットワークアダプターの NIC スイッチの詳細については、「 [Nic スイッチ](nic-switches.md)」を参照してください。

SR-IOV ネットワークアダプター上の PCIe 仮想機能 (VF) のミニポートドライバーでは、NIC スイッチなどのネットワークアダプターのハードウェアリソースが作成または構成されない  に**注意**してください。 詳細については、「 [SR-IOV VF ミニポートドライバーの記述](writing-sr-iov-vf-miniport-drivers.md)」を参照してください。

 

 

 





