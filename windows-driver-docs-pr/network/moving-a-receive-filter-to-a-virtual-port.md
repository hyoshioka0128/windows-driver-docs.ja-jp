---
title: 仮想ポートへの受信フィルターの移動
description: 仮想ポートへの受信フィルターの移動
ms.assetid: 6315FB18-3F57-43C2-B864-3759058092BB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79fa01624e4c06e40bc051106e1ea3382894634b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580548"
---
# <a name="moving-a-receive-filter-to-a-virtual-port"></a>仮想ポートへの受信フィルターの移動


オブジェクト識別子 (OID) のセット上にあるドライバーの問題の要求の[OID\_受信\_フィルター\_移動\_フィルター](https://msdn.microsoft.com/library/windows/hardware/hh451845)受信フィルターを別の仮想ポート (VPort) に移動するにはNIC のスイッチで VPort します。 通常など、仮想化スタックの上にある、ドライバーは、次の条件のいずれかに該当する場合、この OID 要求を発行します。

-   仮想化スタックでは、既定 VPort の受信フィルターを設定します。 このフィルターには、メディア アクセス コントロール (MAC) アドレスと、HYPER-V 子パーティションで公開されている仮想マシン (VM) ネットワーク アダプターの仮想 LAN (VLAN) のパラメーターが含まれています。 これにより、ソフトウェア ベースの合成データ パス経由で VM ネットワーク アダプターと基になるネットワーク アダプター間で転送されるパケット。

    リソースの PCI Express (PCIe) 仮想機能 (VF) が割り当てられているし、VF が子パーティションに接続されている、仮想化スタックは VF に既定以外の VPort を作成します。 仮想化スタックはし、VF に VPort がアタッチされている既定以外に、既定 VPort から VM のネットワーク アダプターの受信フィルターを移動します。 これにより、VF、ハードウェア ベースのデータ パス経由で VM ネットワーク アダプターと基になるネットワーク アダプター間で転送されるパケット。

    これらのデータ パスの詳細については、[SR-IOV データ パス](sr-iov-data-paths.md)を参照してください。

-   ゲスト オペレーティング システムがまだ実行されている HYPER-V 子パーティションから、VF がデタッチされました。 上にあるドライバーが、PF. に VPort がアタッチされている既定値に VPort 既定以外からの VM ネットワーク アダプターの受信フィルターを移動する OID セット要求を発行するこの例では、 この場合、合成データ パスにパケット トラフィックが戻されます。

OID セット要求を発行している上位のドライバー 1 つ VPort から別 VPort に受信フィルターを移動するに[OID\_受信\_フィルター\_移動\_フィルター](https://msdn.microsoft.com/library/windows/hardware/hh451845)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_移動\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567166)構造体。

ドライバーの問題を遮断する前に、 [OID\_受信\_フィルター\_移動\_フィルター](https://msdn.microsoft.com/library/windows/hardware/hh451845)要求と、それを初期化する必要があります、 [ **NDIS\_受信\_フィルター\_移動\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451651)次のように構造体。

-   ドライバーのセット、 **FilterId**メンバーの以前に割り当てられた識別子の識別子には、フィルターを受信します。

    **注**  上にあるドライバーから以前の OID メソッド要求のフィルターの識別子を取得した[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)または[OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)します。

     

-   ドライバーのセット、 **SourceQueueId** NDIS メンバー\_既定\_受信\_キュー\_id。

-   ドライバーのセット、 **SourceVPortId**メンバーにこのフィルターを設定すると以前 VPort の識別子。

-   ドライバーのセット、 **DestQueueId** NDIS メンバー\_既定\_受信\_キュー\_id。

-   ドライバーのセット、 **DestVPortId**メンバーがこのフィルターは、移動する VPort の識別子。

NDIS のメンバーの検証、 [ **NDIS\_受信\_フィルター\_移動\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451651) OID を転送する前にPF のミニポート ドライバーに要求を設定します。

PF のミニポート ドライバーでは、この OID セット要求を処理する場合は、分割不可能な操作で受信フィルターに移動する必要があります。 ドライバーは、同時に受信キューと VPort からフィルターを削除し、別の受信キューと VPort に設定するには、ネットワーク アダプターを構成できる必要があります。

 

 





