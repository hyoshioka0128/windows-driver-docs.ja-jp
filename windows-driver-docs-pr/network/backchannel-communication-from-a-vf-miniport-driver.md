---
title: VF のミニポート ドライバーからのバック チャネル通信
description: VF のミニポート ドライバーからのバック チャネル通信
ms.assetid: B7208199-1308-4EF1-A03B-237A283563C4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f44ff7d450ea1cfb64c6727c1afc0cc63486b0b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557237"
---
# <a name="backchannel-communication-from-a-vf-miniport-driver"></a>VF のミニポート ドライバーからのバック チャネル通信


ミニポート ドライバーの PCI Express (PCIe) 仮想機能 (VF) は、VF 構成ブロックからデータを読み書き PCIe 物理機能 (PF) のミニポート ドライバーと通信します。

VF 構成ブロックは、PF と VF のミニポート ドライバーの間のバック チャネル通信に使用されます。 独立系ハードウェア ベンダー (IHV) は、デバイスの 1 つ以上の VF 構成ブロックを定義できます。 各 VF 構成ブロックは、IHV で定義された形式、長さ、およびブロック id。 たとえば、IHV は VF のミニポート ドライバーのメディア アクセス制御 (MAC) アドレスを使用できる、VF 構成ブロックを定義できます。 別の VF 構成ブロックは、現在 VF と仮想ポート (VPort) の構成に使用できます。

**注**  各 VF 構成ブロックからのデータは、PF と VF のミニポート ドライバーでのみ使用します。 形式とデータの内容は、Windows オペレーティング システムのコンポーネントに対して非透過的です。

 

各 VF 構成ブロックは、IHV によって一意の識別子を割り当てられます。 これにより、クエリまたは特定の VF 構成ブロックに関する情報を設定する VF ミニポート ドライバーができます。

VF ミニポート ドライバーでは、読み取りを開始または、次の関数を使用して、指定した VF 構成ブロックに対する書き込み操作。

-   [**NdisMReadConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)VF の指定された構成ブロックからデータを読み取ります。 VF のミニポート ドライバーは、この関数を呼び出すと、ブロックの識別子と読み取られるデータの長さを指定します。 ドライバーはまた、要求されたデータが格納されるバッファーへのポインターを渡します。

-   [**NdisMWriteConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)、VF 構成の指定されたブロックに書き込むデータ。 VF のミニポート ドライバーは、この関数を呼び出すと、ブロックの識別子と書き込まれるデータの長さを指定します。 ドライバーは、元のデータが書き込まれるバッファーへのポインターも渡します。

PF のミニポート ドライバーでは、次の方法で指定された VF 構成ブロックへのアクセスを管理します。

-   VF のミニポート ドライバーを呼び出すと[ **NdisMReadConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)、NDIS のオブジェクト識別子 (OID) メソッド要求の発行[OID\_SRIOV\_読み取り\_VF\_CONFIG\_ブロック](https://msdn.microsoft.com/library/windows/hardware/hh451874)PF ミニポート ドライバーにします。 この OID 要求には、関数呼び出しで VF ミニポート ドライバーによって渡されたパラメーターのデータが含まれています。

    PF ミニポート ドライバーでは、読み取り操作を実行し、ドライバー OID 要求が完了すると、要求されたデータを返します。 NDIS がへの呼び出しから戻る OID 要求が完了すると、 [ **NdisMReadConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)します。

-   VF のミニポート ドライバーを呼び出すと[ **NdisMWriteConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)、NDIS の OID メソッド要求を発行する[OID\_SRIOV\_書き込み\_VF\_CONFIG\_ブロック](https://msdn.microsoft.com/library/windows/hardware/hh451918)PF ミニポート ドライバーにします。 この OID 要求には、関数呼び出しで VF ミニポート ドライバーによって渡されたパラメーターのデータが含まれています。

    PF のミニポート ドライバーでは、書き込み操作を実行し、OID 要求を完了します。 NDIS がへの呼び出しから戻る OID 要求が完了すると、 [ **NdisMWriteConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)します。

次の図では、SR-IOV backchannel インターフェイスを介して VF 構成ブロックを読み書きするプロセスを示します。

![イメージは、さまざまな構成ブロックが vf ミニポート ドライバー、ndis、および pf ミニポート ドライバーの間で移動を示しています。](images/sriov-vf-backchannel.png)

 

 





