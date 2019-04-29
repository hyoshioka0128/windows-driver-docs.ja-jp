---
title: 仮想ポートのパラメーターの設定
description: 仮想ポートのパラメーターの設定
ms.assetid: 92CBE5B2-897D-4B34-9AB9-8207C42A72BF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 322132216739466da54c1fb790f9d5ee208373dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382895"
---
# <a name="setting-the-parameters-of-a-virtual-port"></a>仮想ポートのパラメーターの設定


上にある、ドライバーは、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターで NIC スイッチの仮想ポート (VPort) のパラメーターを変更できます。 オブジェクト識別子 (OID) を設定するドライバーの問題の要求の[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825)これらのパラメーターを変更します。

上にあるドライバーは、この OID セット要求を発行、前に初期化する必要があります、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体で、VPort 上で変更するパラメーター。 ドライバーを初期化し、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710) OID 要求、およびセットの構造、 **InformationBuffer**メンバーをポインター、 **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター**構造体。

VPort の構成パラメーターの一部のサブセットのみを変更することができます。 上にあるドライバーの次のメンバーを設定して変更するパラメーターを指定します、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。

-   **SwitchId**メンバーは、パラメーターが返されるには、NIC のスイッチの識別子を設定する必要があります。

    **注**  以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、*既定 NIC スイッチ*します。 **SwitchId** NDIS にメンバーを設定する必要があります\_既定\_スイッチ\_id。

     

-   **VPortId** VPort に関連付けられている識別子にメンバーを設定する必要があります。 上にあるドライバーは、次の方法のいずれかで VPort 識別子を取得します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。

    -   前の OID メソッド要求から[OID\_NIC\_スイッチ\_ENUM\_拡張](https://msdn.microsoft.com/library/windows/hardware/hh451821)します。

-   適切な NDIS\_NIC\_スイッチ\_VPORT\_PARAMS\_*Xxx*\_CHANGED フラグを設定する必要があります、**フラグ**メンバー。 メンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体は、対応する NDIS 場合にのみ変更できます\_NIC\_スイッチ\_VPORT\_PARAMS\_*Xxx*\_Ntddndis.h で変更されたフラグが定義されています。

-   メンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597) NDIS に対応する構造体\_NIC\_スイッチ\_VPORT\_PARAMS\_*Xxx*\_CHANGED フラグ設定、**フラグ**メンバー、VPort 構成で設定されます変更するパラメーターです。

以降では、Windows Server 2012 での次のメンバーのみ、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体を指定できますOID セット要求を使用して変更[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825):

<a href="" id="portname"></a>**portName**  
このメンバーには、VPort のわかりやすい説明が含まれています。

<a href="" id="interruptmoderation"></a>**InterruptModeration**  
このメンバーには、VPort の割り込み節度設定を指定します。

<a href="" id="processoraffinity"></a>**ProcessorAffinity**  
このメンバーは、グループの数とこの VPort を関連付けられている Cpu のビットマップを指定します。

上にあるドライバーがこれらを変更するためのガイドラインに従う必要があります、 **ProcessorAffinity**を VPort のメンバー。

-   このメンバーは、PF. にアタッチされている拡張でのみ有効です。 このフィールドは、拡張、VF に関連付けられている既定以外に対して有効ではありません。

-   拡張、PF にアタッチされている、既定以外の VPort の作成時に少なくとも 1 つのプロセッサを指定してください。 VPort の作成後は、既定以外の VPort に関連付けられているプロセッサのアフィニティを変更できます。

    **注**  OID メソッドの要求の既定以外の拡張が作成された[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。

     

<a href="" id="vportstate"></a>**VPortState**  
このメンバーには、VPort の現在の状態を指定します。

上にあるドライバーがこれらを変更するためのガイドラインに従う必要があります、 **VPortState**を VPort のメンバー。

-   既定以外の、VF に関連付けられている VPort の**VPortState**メンバーは常に設定する必要があります**NdisNicSwitchVPortStateActivated**します。

-   既定以外の PF に関連付けられている VPort の**VPortState**にメンバーを設定する必要があります**NdisNicSwitchVPortStateDeactivated** VPort が作成されます。 OID の要求の設定後にのみ、PF VPort がアクティブ化[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825) VPortState に、アクティブな変更を上にあるドライバーによって発行されます。状態。

    PF のミニポート ドライバーが経由で割り当てられた共有メモリなど、VPort のリソースを割り当てることが既定以外の VPort がアクティブになる[ **NdisAllocateSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff561616)します。 PF のミニポート ドライバーがリソースを割り当てること VPort ドライバーの OID セットの要求を通じて VPort の削除されるまでアクティブ化後にいつ[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818).

-   既定値 VPort がアクティブ化された状態では常にします。 値、 **VPortState**メンバーは常に設定する必要があります**NdisNicSwitchVPortStateActivated** VPort の既定の。

-   VPort がアクティブの状態のときは、無効化できません。 PF のミニポート ドライバーでは、受信でき、アクティブ化された状態では、VPort に対応する MAC フィルターが設定されて場合にのみ、VPort からのパケットを送信することができます。 ただしの OID セットの要求を通じて、VPort の削除後[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)ドライバーは、VPort に割り当てられたリソースを解放する必要があります。 ドライバーは保留中のすべての送信を取り消すか受信パケットの場合、VPort での操作もする必要があります。

PF ミニポート後は、ドライバーの OID のセット要求を受け取ります[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825)、ドライバーの構成パラメーターを使用してハードウェアを構成する. ドライバーでは、NDIS で識別されるこれらの構成パラメーターを変更できるだけ\_NIC\_スイッチ\_VPORT\_パラメーター\_*Xxx*\_CHANGEDフラグ、**フラグ**のメンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。

 

 





