---
title: 仮想ポートの作成
description: 仮想ポートの作成
ms.assetid: 6102576D-3236-4FDD-8963-83A9E90FF7F0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1b27a68a95763d43226600c5fb42d2ebd9291fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357352"
---
# <a name="creating-a-virtual-port"></a>仮想ポートの作成


仮想ポート (VPort) は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの NIC のスイッチを内部ポートを表すデータ オブジェクトです。 各 NIC スイッチでは、ネットワーク接続のため、次のポートがあります。

-   1 つ外部の物理ポートの外部の物理ネットワークに接続します。

-   1 つまたは複数の内部拡張 PCI Express (PCIe) 物理機能 (PF) または仮想機能 (Vf) に接続しています。

    PF は、HYPER-V 親パーティションに接続され、そのパーティションで実行されている管理オペレーティング システム内の仮想ネットワーク アダプターとして公開されます。

    VF は、HYPER-V 子パーティションに接続され、そのパーティションで実行されるゲスト オペレーティング システム内の仮想ネットワーク アダプターとして公開されます。

拡張の 2 種類あります。

<a href="" id="default-vport"></a>既定の VPort  
既定の VPort は、管理オペレーティング システムで実行されているネットワーク コンポーネントへのネットワーク接続を提供します。 既定 VPort NDIS の識別子を持つ\_既定\_VPORT\_id。

ドライバーは、PF ミニポート ドライバーでは、作成し、既定の NIC スイッチを構成します、ときに、暗黙的に VPort の既定を作成し、PF. にアタッチします。 既定の VPort、VF にアタッチできません。

既定の VPort は常にアクティブ化の状態と、明示的に削除することはできません。 PF ミニポート ドライバーでは、既定の NIC のスイッチを削除するときにのみ既定 VPort 暗黙的に削除します。

NIC のスイッチと既定 VPort スイッチを作成する方法の詳細については、次を参照してください。 [NIC スイッチの作成](creating-a-nic-switch.md)です。

<a href="" id="nondefault-vport"></a>既定以外の VPort  
NIC のスイッチの作成時に既定以外の拡張は暗黙的に作成されません。 OID メソッド要求を発行して、これらのポートを明示的に作成しますなど、仮想化スタックの上にあるドライバー [OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。 既定以外の拡張は、PF または、VF、接続されている可能性があり、NIC のスイッチが作成された後にのみ作成できます。

既定以外の VF に関連付けられている VPort は、ゲスト オペレーティング システムで実行されているネットワーク コンポーネントへのネットワーク接続を提供します。 作成して、VF にアタッチされている、したら、既定以外 VPort は、アクティブ化された状態です。

既定以外の PF に関連付けられている VPort では、管理オペレーティング システムで実行されているネットワーク コンポーネントに追加のネットワーク オフロード機能を提供します。 たとえば、既定以外の PF を拡張が提供される可能性がありますが、仮想マシン キュー (VMQ) インターフェイスに似た機能をオフロードします。

**注**既定以外の拡張は、NIC のスイッチが作成された後にのみ作成できます。



上位のドライバーの問題のオブジェクト識別子 (OID) メソッド要求[OID\_NIC\_切り替える\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816) NIC スイッチを指定した既定以外の VPort を作成します。 この OID 要求には、ネットワーク アダプターの PF または以前に割り当てられた VF に作成された VPort もアタッチします。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、[ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。 正常に戻った後、 [OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)要求、 **VPortId**のメンバー、 **NDIS\_NIC\_切り替える\_VPORT\_パラメーター**構造体が NIC スイッチの拡張の間で一意である VPort 識別子。

上にあるドライバーを初期化します、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構成情報を含む構造体既定を作成する VPort 以外。 構成情報には、先 VPort がアタッチされている既定以外と数、キュー ペア VPort 既定以外の PCIe 関数が含まれています。

初期化時、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造上にあるドライバーは、次を実行する必要があります。

-   **SwitchId**メンバーは、ネットワーク アダプターの OID メソッド要求を既に作成されている NIC スイッチの識別子を設定する必要があります[OID\_NIC\_切り替える\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)します。

    **注**以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、*既定 NIC スイッチ*します。 上にあるドライバーが VPort の既定以外の作成時に設定する必要があります、 **SwitchId** NDIS メンバー\_既定\_スイッチ\_ID です。



-   **VPortId** NDIS にメンバーを設定する必要があります\_既定\_VPORT\_id。

-   **AttachedFunctionId** VF またはアタッチする VPort 既定以外になっている PF の識別子にメンバーを設定する必要があります。

    NDIS @property\_PF\_関数\_ID が、PF. を指定します 以前の OID メソッド要求を通じて割り当てられたリソースを含む VF の識別子に値を設定する必要がありますそれ以外の場合、 [OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。

    **注**VF または PF に既定以外の VPort の添付ファイルは既定以外の VPort が作成された後は変更できません。



上にあるドライバーは、VPort に割り当てられているキュー ペアの数を指定もできます。 キュー ペアは、送信は、送受信、VPort に割り当てられているネットワーク アダプターのキューです。 ネットワーク アダプターでは、既定以外の拡張の非対称キュー ペアをサポートする場合、上にあるドライバーはドライバーを作成する各 VPort のキュー ペアの数が異なるを指定できます。 詳細については、次を参照してください。[対称と非対称の割り当てのキュー ペア](symmetric-and-asymmetric-assignment-of-queue-pairs.md)します。

上にあるドライバー呼び出し[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)問題を[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)基になる PF ミニポート ドライバーに要求します。 NDIS ミニポート ドライバーに OID メソッド要求を転送する前に、次は。

1.  NDIS 内のパラメーターの検証、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。 パラメーターがエラーである場合は、NDIS OID メソッド要求は失敗し、要求は、PF ミニポート ドライバーに渡されません。

2.  NDIS に割り当てる 1 つの範囲内で VPort 既定以外の識別子を (**NumVPorts**– 1) ここで、 **NumVPorts**ミニポート ドライバーが、ネットワーク アダプターで構成されている拡張の数です。 ドライバーでは、この数を指定します、 **NumVPorts**のメンバー、 [ **NDIS\_NIC\_スイッチ\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451582)構造体。 ドライバーの OID クエリ要求をこの構造体を返します[OID\_NIC\_スイッチ\_ENUM\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451819)します。

    **注**NDIS の A VPort 識別子\_既定\_VPORT\_VPort 既定 NIC スイッチの PF に関連付けられている既定の ID は予約されています。




割り当てられた VPort 識別子には、既定以外の VPort ネットワーク アダプターの NIC のスイッチを一意に識別します。


3.  NDIS セット、 **VPortId**の NDIS メンバー\_NIC\_スイッチ\_VPORT\_割り当てられた VPort 識別子を持つパラメーター構造体。

PF のミニポート ドライバーには、OID 要求が発行される、ドライバーは指定した既定以外の VPort に関連付けられているハードウェアおよびソフトウェア リソースを割り当てます。 すべてのリソースが正常に割り当てられた後、PF ミニポート ドライバー、OID が正常に完了 NDIS を返すことによって\_状態\_から成功[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416).

場合、 [OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)要求が正常に完了、PF ミニポート ドライバーおよび上位のドライバーを保持する必要があります、 **VPortId** VPort 一連の操作の既定値以外の値。 **VPortId**値は、これらの操作中に使用されます。

-   NDIS および上にあるドライバーを使用して、 **VPortId**を既定以外の連続する OID で VPort を識別する値を要求などに関連するこの VPort、 [OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825)と[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)します。

-   送信操作では中、NDIS を指定します、 **VPortId** VPort のパケットの送信元を識別する値。 バンドの外 (OOB) 内でこの値が指定されて[ **NDIS\_NET\_バッファー\_一覧\_フィルター\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566567)のデータ、[NET\_バッファー\_一覧](net-buffer-list-structure.md)構造体。

-   中に受信操作、PF ミニポート ドライバーを指定します、 **VPortId**パケットが転送される値。 この値は、OOB 内も指定[ **NDIS\_NET\_バッファー\_一覧\_フィルター\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566567)データ、の[NET\_バッファー\_一覧](net-buffer-list-structure.md)構造体。

次の点は、既定以外の拡張の作成に適用されます。

-   メディア アクセス制御 (MAC) が作成された後は、仮想 LAN (VLAN) の識別子を VPort で構成のフィルターが表示されます。 これらのドライバーを動的に関連する設定の OID メソッド要求を発行してフィルターが表示される[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)します。 受信フィルターは、1 つ VPort OID を別の要求の設定から移動することも[OID\_受信\_フィルター\_移動\_フィルター](https://msdn.microsoft.com/library/windows/hardware/hh451845)します。

-   作成時にその VPort は VF にアタッチされている既定以外はアクティブ化された状態です。 VF にアタッチされている場合、VPort を非アクティブ化できません。

    作成時にその VPort が PF にアタッチされている既定以外は、非アクティブ化の状態です。 HYPER-V 拡張可能スイッチ モジュールなどの上にあるドライバーには、VPort が正常に作成された後、PF に VPort 接続されている既定以外に明示的にアクティブにします。 これには、OID メソッド要求の発行を[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825) PF ミニポート ドライバーにします。

    上にあるドライバーは、この OID 要求を発行の際に渡して、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597) を含む構造体**VPortState**メンバーに設定**NdisNicSwitchVPortStateActivated**します。

    既定以外の VPort がアクティブ化された状態を後、PF ミニポート ドライバーに割り当てることが共有メモリ、VPort 呼び出して[ **NdisAllocateSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff561616)します。 ドライバーを設定する必要があります、 **VPortId**内のメンバー、 [ **NDIS\_SHARED\_メモリ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567303) VPort の構造体識別子の値。

**注**既定以外の VPort がアクティブ化された状態をときにのみ設定されますを非アクティブ化された状態には、削除の OID セット要求を[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818).











