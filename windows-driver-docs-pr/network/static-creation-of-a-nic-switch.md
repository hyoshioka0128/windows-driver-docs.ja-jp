---
title: NIC スイッチの静的作成
description: NIC スイッチの静的作成
ms.assetid: F325B1F8-7655-4044-AF04-32B434574082
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d420205bb40d87e2a6f2d109af53efe651c05f98
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841829"
---
# <a name="static-creation-of-a-nic-switch"></a>NIC スイッチの静的作成


シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターでは、NIC スイッチを作成できる必要があります。 アダプターによっては、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)の呼び出しのコンテキスト内で、NIC スイッチを静的に作成することができます。

アダプターに NIC スイッチを作成できるのは、SR-IOV アダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーだけです。

**注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは*既定の NIC スイッチ*と呼ばれ、NDIS\_既定\_スイッチ\_ID 識別子によって参照されます。

 

既定の NIC スイッチのパラメーターは、レジストリの標準化されたキーワード設定を使用して定義されます。 これらのキーワードの詳細については、「sr-iov[用の標準化](standardized-inf-keywords-for-sr-iov.md)された INF キーワード」を参照してください。

PF ミニポートドライバーは、NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すときに、NIC スイッチを静的に作成します。 通常、ドライバーは初期化シーケンスの一部として NIC スイッチを作成して構成してから、ネットワークアダプターで sr-iov を有効にします。

PF ミニポートドライバーは、NIC スイッチを静的に作成し、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)への呼び出しのコンテキストでネットワークアダプターの sr-iov を有効にするときに、次の手順に従います。

1.  PF ミニポートドライバーは、sr-iov が有効になっているかどうかを判断し、NIC スイッチの構成パラメーターを取得するために、sr-iov の標準化されたキーワードを読み取る必要があります。

    **注**  PF ミニポートドライバーによって[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数へのエントリポイントが登録されている場合、ドライバーは、NDIS が*MiniportSetOptions*を呼び出したときにこれらのパラメーターを以前にレジストリから取得した可能性があります。

     

2.  SR-IOV が有効になっている場合、PF ミニポートドライバーは、レジストリからの NIC スイッチパラメーターを使用してネットワークアダプターを構成します。 ドライバーは、ネットワークアダプターを構成する前に、パラメーターが有効であることを確認する必要があります。 たとえば、ミニポートドライバーは、NIC スイッチに割り当てられている PCIe 仮想関数 (VFs) の最大数が、ネットワークアダプターでサポートされている VFs の数を超えていないことを確認する必要があります。

3.  ミニポートドライバーは、 [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出して sr-iov を有効にし、ネットワークアダプターの VFs の数を設定します。 この関数は、アダプターの PCI 構成領域で sr-iov 拡張機能を構成します。 この関数が NDIS\_STATUS\_SUCCESS を返した場合、SR-IOV が有効になり、VFs が PCIe インターフェイスを介して公開されます。

**注**  PF ミニポートドライバーによって nic スイッチが静的に作成された場合は、NDIS がオブジェクト識別子 (oid) メソッド要求を oid に発行するまでスイッチを使用できません[\_NIC\_スイッチ\_\_スイッチを作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)します。 PF ミニポートドライバーが静的に NIC スイッチを作成した場合は、スイッチパラメーターが OID 要求に指定されていることを確認する必要があります。 これらのパラメーター ( [**NDIS\_NIC\_スイッチ\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)構造に含まれる) は、OID 要求に関連付けられていますが、スイッチの作成に使用されたドライバーのパラメーターと同じである必要があります。

 

[Oid\_nic\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)を処理する方法の詳細については\_\_スイッチ要求の作成に関する詳細については、「 [oid\_Nic\_を処理](handling-the-oid-nic-switch-create-switch-request.md)する\_スイッチ要求を作成する」を参照してください。\_

PF ミニポートドライバーの初期化シーケンスと要件の詳細については、「 [Pf ミニポートドライバーの初期化](initializing-a-pf-miniport-driver.md)」を参照してください。

 

 





