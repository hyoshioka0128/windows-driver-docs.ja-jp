---
title: NIC スイッチのパラメーターの設定
description: NIC スイッチのパラメーターの設定
ms.assetid: 79B4B0B7-32AB-4AE4-ACD2-CE17C93573BA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f2c7905c31b1ed1b406e8fd3f353f3bf922a45e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382897"
---
# <a name="setting-the-parameters-of-a-nic-switch"></a>NIC スイッチのパラメーターの設定


上位のドライバーには、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターで作成された NIC スイッチ パラメーターを変更できます。 オブジェクト識別子 (OID) を設定するドライバーの問題の要求の[OID\_NIC\_スイッチ\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451823)これらのパラメーターを変更します。 ミニポート ドライバーを PCI Express (PCIe) 物理機能 (PF) の SR-IOV 対応アダプターだけでは、この OID セット要求を処理します。

上にあるドライバーは、この OID セット要求を発行、前に初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)パラメーターの設定を含む構造体NIC のスイッチで変更します。 ドライバーを初期化し、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710) OID 要求、およびセットの構造、 **InformationBuffer**メンバーをポインター、 **NDIS\_NIC\_スイッチ\_パラメーター**構造体。

NIC のスイッチの構成パラメーターの一部のサブセットのみを変更できます。 上にあるドライバーの次のメンバーを設定して変更するパラメーターを指定します、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体。

-   **SwitchId**メンバー NIC スイッチ パラメーターを持つは変更の識別子に設定されます。

    **注**  以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、*既定 NIC スイッチ*します。 **SwitchId** NDIS にメンバーを設定する必要があります\_既定\_スイッチ\_id。

     

-   適切な NDIS\_NIC\_スイッチ\_パラメーター\_*Xxx*\_変更されたフラグが設定されて、**フラグ**メンバー。 メンバー、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)構造体は、対応する NDIS 場合にのみ変更できます\_NIC\_スイッチ\_パラメーター\_*Xxx*\_Ntddndis.h で変更されたフラグが定義されています。

-   メンバー、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587) NDIS に対応する構造体\_NIC\_スイッチ\_パラメーター\_*Xxx*\_で変更されたフラグを設定、**フラグ**メンバーを変更する NIC のスイッチの構成パラメーターを使用して設定されます。

    **注**  以降、Windows Server 2012 でのみ、 **SwitchName**のメンバー、 [ **NDIS\_NIC\_スイッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451587)の OID セットの要求で構造を変更できます[OID\_NIC\_スイッチ\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451823)します。

     

PF のミニポート ドライバーは、の OID のセット要求を受け取ったときにこれらのガイドラインに従う必要があります[OID\_NIC\_スイッチ\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451823)

-   ドライバーがハードウェアに、変更が適用され、NDIS に OID 要求が完了した場合は、PF ミニポート ドライバーでは、ネットワーク アダプターの再初期化を必要とせず、変更を適用できます、\_状態\_成功します。

    この状態コードが返された場合、NDIS は、レジストリ内の NIC スイッチの構成情報を更新します。

-   ドライバーが NDIS に OID 要求を完了すると、PF ミニポート ドライバーには、変更を適用するネットワーク アダプターの再初期化が必要とする場合\_状態\_REINIT\_必要な作業です。

    この状態コードが返されます、NDIS もレジストリ内の NIC スイッチの構成情報を更新します。 ただし、OID セット要求を発行した上にあるドライバーは、変更を反映するために、ネットワーク アダプターを再初期化する必要があります。

    **注**  静的の NIC の作成と構成をサポートする PF ミニポート ドライバーは、NDIS を返すことができます\_状態\_REINIT\_新しいアダプターが再初期化するかどうかを確認するには、必要な作業有効にするパラメーターです。

     

-   OID で要求された変更を適用できないのは、PF ミニポート ドライバー、OID が失敗して、適切な NDIS を返すにする必要があります\_状態\_*Xxx*コード。

    この場合は、NDIS は、レジストリ内の NIC スイッチの構成情報を更新できません。

 

 





