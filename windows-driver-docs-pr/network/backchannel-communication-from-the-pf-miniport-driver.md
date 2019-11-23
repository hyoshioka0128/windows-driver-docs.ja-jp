---
title: PF ミニポート ドライバーからのバックチャネル通信
description: PF ミニポート ドライバーからのバックチャネル通信
ms.assetid: 819FC32C-D50C-480F-AE6E-078E4ECD3400
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db02eddd756e45c0c1fd0e68ab23aeb58a175702
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838227"
---
# <a name="backchannel-communication-from-the-pf-miniport-driver"></a>PF ミニポート ドライバーからのバックチャネル通信


PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーは、PCIe 仮想機能 (VF) のミニポートドライバーと通信して、VF 構成ブロックのデータの変更に関する通知を発行します。 PF ミニポートドライバーは、これらの通知を発行して、VF 構成ブロック内のデータを*無効*にします。 この通知に応答して、VF ミニポートドライバーは、PF ミニポートドライバーに backchannel 要求を発行して、無効になっている VF 構成ブロックからデータを読み取ることができます。

VF 構成ブロックは、PF および VF ミニポートドライバー間のバックチャネル通信に使用されます。 IHV は、デバイスに対して1つまたは複数の VF 構成ブロックを定義できます。 各 VF 構成ブロックには、IHV によって定義された形式、長さ、およびブロック ID があります。

  **注**各 VF 構成ブロックのデータは、PF および vf ミニポートドライバーによってのみ使用されます。 このデータの形式と内容は、Windows オペレーティングシステムのコンポーネントに対して非透過的です。

 

無効な VF 構成データの通知を発行および処理するときは、次の手順が実行されます。

1.  ゲストオペレーティングシステムでは、NDIS は IOCTL\_VPCI の i/o 制御要求を発行し、 [ **\_ブロック\_無効**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)にします。 この IOCTL が完了すると、NDIS には、VF 構成データが変更されたことが通知されます。

2.  Hyper-v の親パーティションで実行されている管理オペレーティングシステムでは、次の手順が実行されます。

    1.  PF ミニポートドライバーは、 [**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)関数を呼び出して、VF 構成データが変更され、無効になったことを NDIS に通知します。 ドライバーは、どの VF 構成ブロックが変更されたかを指定する ULONGLONG ビットマスクに*Blockmask*パラメーターを設定します。 ビットマスクの各ビットは、VF 構成ブロックに対応します。 ビットが1に設定されている場合は、対応する VF 構成ブロック内のデータが変更されます。
    2.  NDIS は、管理オペレーティングシステムで実行される仮想化スタックを、VF 構成ブロックデータの変更について通知します。 仮想化スタックは、 *Blockmask*パラメーターデータをキャッシュします。

        **注**  PF ミニポートドライバーが[**NdisMInvalidateConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisminvalidateconfigblock)を呼び出すたびに、仮想化スタックは、*ブロックマスク*パラメーターデータにキャッシュ内の現在の値を指定します。

         

    3.  仮想化スタックは、ゲストオペレーティングシステムで実行されている仮想 PCI (VPCI) ドライバーに、VF 構成データの無効化について通知します。 仮想化スタックは、キャッシュされた*Blockmask*パラメーターデータを vpci ドライバーに送信します。

3.  Hyper-v の子パーティションで実行されているゲストオペレーティングシステムでは、次の手順が実行されます。

    1.  VPCI ドライバーは、キャッシュされた*blockmask*パラメーターデータを Vpci の**blockmask**メンバーに保存し、 [**IOCTL\_vpci**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)に関連付けられている[ **\_ブロック\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ns-vpci-_vpci_invalidate_block_output)構造体を無効にして、ブロック要求を無効に\_\_します。\_

    2.  VPCI ドライバーは[**IOCTL\_vpci\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)正常に完了し、ブロック要求を\_無効にします。 このような場合、NDIS は Oid\_Oid のオブジェクト識別子 (OID) メソッドの要求を発行し[\_vf\_無効\_構成\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-invalidate-config-block) vf ミニポートドライバーにブロックします。 [**NDIS\_SRIOV\_VF\_無効\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_invalidate_config_block_info)は OID 要求で渡されます。\_ この構造体には、キャッシュされた*Blockmask*パラメーターのデータが含まれます。

        また、NDIS では、別の[**IOCTL\_VPCI\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/vpci/ni-vpci-ioctl_vpci_invalidate_block)も発行されます。これにより、VF 構成データへの変更の継続的な通知を処理するために、ブロック要求\_ブロックが発生

    3.  VF ドライバーが OID\_処理するとき[\_vf\_無効\_構成\_ブロック](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-invalidate-config-block)要求は、 [**NdisMReadConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)を呼び出すことによって、指定された vf 構成ブロックからデータを読み取ることができます。 このプロセスの詳細については、「 [VF ミニポートドライバーからのバックチャネル通信](backchannel-communication-from-a-vf-miniport-driver.md)」を参照してください。

 

 





