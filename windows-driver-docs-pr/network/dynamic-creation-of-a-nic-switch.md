---
title: NIC のスイッチの動的な作成
description: NIC のスイッチの動的な作成
ms.assetid: 16B2D94A-AF30-434F-8F14-2F535501A52F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeb05d7d6481c23cc43df34bb7f43645e66a8bf3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548585"
---
# <a name="dynamic-creation-of-a-nic-switch"></a>NIC のスイッチの動的な作成


シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターは、NIC のスイッチを作成できる必要があります。 一部のアダプターでは、NIC スイッチ動的に作成できる、ミニポート ドライバーがへの呼び出しから返された後[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)します。

ミニポート ドライバーを PCI Express (PCIe) 物理機能 (PF) の SR-IOV 対応アダプターだけでは、アダプターで NIC スイッチを作成できます。

**注**  以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、 *NIC スイッチの既定*、NDIS によって参照されている\_既定\_スイッチ\_ID です。

 

オブジェクト識別子 (OID) メソッド要求を発行する NDIS [OID\_NIC\_スイッチ\_作成\_切り替える](https://msdn.microsoft.com/library/windows/hardware/hh451815)SR-IOV ネットワーク アダプターで NIC スイッチを作成します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_切り替える\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)スイッチ パラメーターを含む構造体。

PF のミニポート ドライバーが動的にサポートする場合は、NIC はスイッチの作成、この OID 要求を処理する場合、次の手順に従う必要があります。

1.  PF のミニポート ドライバーでは、これらのパラメーターに基づいて、NIC のスイッチに必要なハードウェアおよびソフトウェア リソースを割り当てます。 ドライバーは、これらのパラメーターでも、ネットワーク アダプターを構成します。

    **注**  動的 NIC スイッチの作成をサポートする PF ミニポート ドライバーには、レジストリで標準化された SR-IOV キーワード設定を使用してスイッチ パラメーターを読み取る必要はありません。 NDIS は初期化するためにこれらのキーワードを読み取り、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)発行前に構造体、 [OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)要求。 これらのキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

     

2.  ミニポート ドライバー呼び出し[ **NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481) SR-IOV を有効にし、ネットワーク アダプターで VFs の数を設定します。 この関数は、アダプターの PCI 構成領域で SR-IOV 対応の拡張機能を構成します。 この関数は、NDIS を返す場合\_状態\_成功した場合、SR-IOV が有効になっているし、VFs が、PCIe インターフェイスを介して公開されます。

詳細を処理する方法について、 [OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)要求を参照してください[OID 処理\_NIC\_スイッチ\_作成\_スイッチ要求](handling-the-oid-nic-switch-create-switch-request.md)します。

 

 





