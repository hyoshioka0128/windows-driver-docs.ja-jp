---
title: OID_NIC_SWITCH_ALLOCATE_VF 要求の発行
description: OID_NIC_SWITCH_ALLOCATE_VF 要求の発行
ms.assetid: 72285E72-DEC7-4578-9B6C-E616FECD6F41
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48395ca61ef3e2cc48ae1bee5394d19173829140
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353751"
---
# <a name="issuing-oidnicswitchallocatevf-requests"></a>OID の発行\_NIC\_スイッチ\_ALLOCATE\_VF 要求


オブジェクト識別子 (OID) メソッドの要求を発行する前に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)ミニポート ドライバーを PCI Express (PCIe) 物理機能 (PF)、ドライバーの上にあるフォーマット、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。 この構造体には、PCIe 仮想機能 (VF)、ネットワーク アダプターに割り当てられるリソースの構成パラメーターが含まれています。 上にあるドライバーは、次のようにこの構造体のメンバーを設定する必要があります。

-   **SwitchId**メンバーは、ネットワーク アダプターで既に作成されている NIC スイッチの識別子を設定する必要があります。 NIC のスイッチがの OID メソッド要求を使って作成された[OID\_NIC\_スイッチ\_作成\_切り替える](https://msdn.microsoft.com/library/windows/hardware/hh451815)します。

    OID メソッド要求を処理するときに[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)、PCIe 物理機能 (PF) のミニポート ドライバーは VF のリソースを割り当てます。 リソースが正常に割り当てられている場合 PF ミニポート ドライバーは VF を指定した NIC スイッチに割り当てます。

    **注**Windows Server 2012 で NDIS 6.30 以降、SR-IOV インターフェイスに対してのみサポートして既定の NIC のスイッチ、ネットワーク アダプター。 値、 **SwitchId** NDIS にメンバーを設定する必要があります\_既定\_スイッチ\_id。

    NIC のスイッチの詳細については、次を参照してください。 [NIC スイッチ](nic-switches.md)します。

-   **VFId** NDIS にメンバーを設定する必要があります\_無効な\_VF\_関数\_id。

-   **RequestorId** NDIS にメンバーを設定する必要があります\_無効な\_RID。

-   **VMFriendlyName**と**VMName**メンバーは、HYPER-V 子パーティションのパラメーターに設定する必要があります。 PF のミニポート ドライバーでは、情報提供を目的にのみこれらのメンバーを使用します。

    **注**HYPER-V 子パーティションとも呼ばれますが、*仮想マシン (VM)* します。

    VF の上にあるドライバーの問題の前に、指定された VM に関連付けられて、 [OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)要求。

-   **NicName**メンバーは、仮想マシン (VM) ネットワーク アダプターの識別子を設定する必要があります。 この仮想アダプターは、VM で実行されているゲスト オペレーティング システムで公開されます。 PF ミニポート ドライバーは、情報提供を目的にのみ、このメンバーを使用します。

    VF のリソースが割り当てられているし、子パーティションにアタッチされている、VF のネットワーク アダプターがゲスト オペレーティング システムに公開されます。 VM のネットワーク アダプターのチームは、パケットの転送、VF のネットワーク アダプターと VF、ハードウェア ベースのデータ パス経由でします。

    ただし、VF は、ライブ マイグレーション中のプロセスなど、子パーティションからデタッチでした。 この場合、ソフトウェア ベースの合成データ パスを介してパケットの転送が行われます。 これらのデータ パスの詳細については、次を参照してください。 [SR-IOV データ パス](sr-iov-data-paths.md)します。

-   **PermanentMacAddress**と**CurrentMacAddress**メンバーに設定してください、メディア、VF の仮想ネットワーク アダプターのアクセス制御 (MAC) アドレス。 これらのアドレスは、HYPER-V 子パーティションのゲスト オペレーティング システムで実行されているネットワーク スタックに公開されます。

上にあるドライバーの OID メソッド要求を発行する[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)次の手順。

1.  上にあるドライバーを初期化します、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710) OID メソッド要求の構造体。 ドライバーのセット、 **InformationBuffer**メンバーが初期化されたへのポインターに[ **NDIS\_NIC\_スイッチ\_VF\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。

2.  上にあるドライバー呼び出し[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)基になる PF ミニポート ドライバーに OID 要求を発行します。

    **注**上にあるドライバーを呼び出すと[ **NdisOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff563710)、NDIS OID 要求をインターセプトし、VF パラメーターで指定されたことを確認、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。 パラメーターの検証が正常には、NDIS は PF ミニポート ドライバーに OID を転送します。 それ以外の場合、NDIS が NDIS に OID 要求が失敗した\_状態\_無効な\_パラメーター。

上にある、ドライバーは VF のリソースの割り当てを要求した後、そのドライバーは、同じ VF のリソースの解放が要求できる唯一のコンポーネントになります。 上にあるドライバーの OID セット要求を発行する必要があります[OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822) VF リソースを解放します。 ドライバーのによって割り当てられた各 VF のリソースを解放する必要があります上にあるドライバーを停止できますが、前に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)要求。