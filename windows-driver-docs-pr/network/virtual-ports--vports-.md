---
title: 仮想ポート (VPort)
description: 仮想ポート (VPort)
ms.assetid: FCE0B5F5-5E2E-493A-BE25-57FB2C8B0389
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f1875343a6de5ef827f13f3b2b699618deda236
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571618"
---
# <a name="virtual-ports-vports"></a>仮想ポート (VPort)


仮想ポート (VPort) には、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの NIC のスイッチを内部ポートを表すデータ オブジェクトです。 各 NIC スイッチでは、ネットワーク接続のため、次のポートがあります。

-   1 つ外部の物理ポートの外部の物理ネットワークに接続します。

-   1 つまたは複数の内部拡張 PCI Express 物理機能 (PF) または仮想機能 (Vf) に接続しています。

    PF は、HYPER-V 親パーティションに接続され、そのパーティションで実行されている管理オペレーティング システム内の仮想ネットワーク アダプターとして公開されます。

    VF は、HYPER-V 子パーティションに接続され、そのパーティションで実行されるゲスト オペレーティング システム内の仮想ネットワーク アダプターとして公開されます。

NIC は、1 つまたは複数の拡張に物理ポートからのブリッジ ネットワーク トラフィックを切り替えます。 これは、基になる物理ネットワーク インターフェイスを仮想化のアクセスを提供します。

各 VPort に一意の識別子 (*VPortId*) ネットワーク アダプターで NIC スイッチに一意です。 VPort の既定値は常に既定の NIC スイッチに存在し、削除できません。 既定 VPort が VPortId の NDIS\_既定\_VPORT\_id。

PF のミニポート ドライバーでのオブジェクト識別子 (OID) メソッド要求を処理するときに[OID\_NIC\_スイッチ\_作成\_切り替える](https://msdn.microsoft.com/library/windows/hardware/hh451815)NIC のスイッチと、既定値を作成 VPort のそのスイッチ。 既定値 VPort は PF に常にアタッチされてし、動作の状態は常にします。

既定以外の拡張の OID メソッド要求が作成された[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。 1 つだけの既定以外 VPort、VF にアタッチできます。 アタッチされると、既定では動作の状態です。 1 つまたは複数の既定以外拡張も作成され、PF. にアタッチされています。 これらの拡張が作成されたときに操作不可状態との OID セット要求を稼動[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825)します。

**注**後、VPort が動作可能になります、のみになる操作不可状態の OID 要求をで削除されるとき[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818).



各 VPort が、それを受信し、パケットを送信するために関連付けられている 1 つまたは複数のハードウェア キュー ペア。 ネットワーク アダプターの既定のキュー ペアは、既定 VPort で使用するために予約されています。 キューの拡張が割り当てられ、VPort がで作成したときに割り当てられている既定以外のペア、 [OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)要求。

既定以外の拡張が作成されの OID メソッド要求を使用して構成[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。 OID のセット要求を通じた既定 VPort と既定以外の拡張を再構成[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451825)します。 各 OID 要求に含まれる、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)次の構成を指定する構造体パラメーター:

-   PCIe 関数は、VPort がアタッチされています。

    各 VPort かアタッチできます PF したり、VF いつでも。 VPort が作成され、PCIe 関数に接続されている場合は後、別の PCIe 関数に、添付ファイルを動的に変更できません。

    **注**VPort が常にネットワーク アダプターの PF に接続されている既定値。




Windows Server 2012 の 1 つだけの既定以外の NDIS 6.30 以降 VPort は、VF にアタッチすることができます。 ただし、既定 VPort と共に既定以外の拡張は複数をアタッチして、PF. する


-   VPort に割り当てられているハードウェア キュー ペアの数。

    各 VPort には、使用することのあるハードウェア キュー ペアのセットがあります。 キューの各ペアは、個別の送信で構成され、受信ネットワーク アダプターのキュー。

    キュー ペアは、ネットワーク アダプターの限られたリソースです。 NIC スイッチの作成時に、既定と既定以外の拡張で使用するために予約されているキュー ペアの合計数が指定します。 これにより、既定以外の拡張とは異なるに VPort の既定値に割り当てられているキュー ペアの数。

    各既定以外の VPort を構成して、キュー ペアの数が異なるすることができます。 これと呼ばれます*非対称割り当て*キュー ペアの。 NIC がこのような非対称割り当てを許可しない場合は、各既定以外の VPort を構成するキューのペアの数が等しい。 これと呼ばれます*対称割り当て*キュー ペアの。 詳細については、次を参照してください。[対称と非対称の割り当てのキュー ペア](symmetric-and-asymmetric-assignment-of-queue-pairs.md)します。

    **注**、PF ミニポート ドライバーの中にキュー ペアの非対称の割り当てをサポートするかどうかを報告[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)します。 詳細については、次を参照してください。 [PF ミニポート ドライバーの初期化](initializing-a-pf-miniport-driver.md)します。




各 VPort に割り当てられているキュー ペアの数は動的に変更されません。 VPort が作成された後、VPort に割り当てられているキュー ペアの数を変更できません。

**注**拡張を使用できる既定以外に割り当てられているキュー ペアが 1 つまたは複数の受信側 scaling (RSS) を使用してゲスト オペレーティング システムで実行されている VF ミニポート ドライバー。




-   VPort のモデレート パラメーターを中断します。

    複数の割り込みのモデレート型は、さまざまな拡張に対して指定できます。 これにより、特定の VPort によって生成される割り込みの数を制御する仮想化スタックができます。

表示されるフィルターを各 VPort の OID メソッド要求を発行してでドライバーを後続のパラメーターを構成できる構成に加えて[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795). NIC のスイッチを指定した実行 VPort ごとにフィルター処理を受信します。

拡張には、パケットのフィルター条件は、メディア アクセス制御 (MAC) アドレスと仮想 LAN (VLAN) id の一覧などが含まれているフィルター パラメーターを受信します。 MAC アドレスと VLAN 識別子フィルターでは同時に指定常には、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181) に関連付けられています。[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)要求。 NIC スイッチ スイッチへの受信パケット フィルターする必要がありますが接続先 MAC アドレスと VLAN 識別子、VPort に設定された受信フィルター条件に一致します。 NIC のスイッチは、いずれかの別の VPort や外部の物理ポートから受信したパケットをフィルター処理します。 パケットがフィルターに一致する場合、NIC スイッチする必要がありますに転送する、VPort します。

VPort の複数の MAC アドレスと VLAN 識別子のペアを設定することがあります。 MAC アドレスを設定すると、専用の場合、VPort が次の条件に一致するパケットを受信する受信フィルターを指定します。

-   パケットの宛先 MAC アドレスでは、フィルターの MAC アドレスと一致します。

-   パケットが VLAN タグを持っているか (VLAN タグがあるかどうか)、0 の VLAN 識別子です。

既定以外の拡張が削除の OID のセット要求を通じた[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)します。 既定の OID セットの要求を通じて NIC スイッチが削除された場合にのみ、VPort が削除[OID\_NIC\_切り替える\_削除\_切り替える](https://msdn.microsoft.com/library/windows/hardware/hh451817)します。









