---
title: 仮想関数の PCI 構成データの設定
description: 仮想関数の PCI 構成データの設定
ms.assetid: 74CAAD8B-7009-4C79-A496-93B4A3DA0B43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7fcadadbc051005d0ae467cf986bb93731da5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362024"
---
# <a name="setting-the-pci-configuration-data-of-a-virtual-function"></a>仮想関数の PCI 構成データの設定


ミニポート ドライバーを PCI Express (PCIe) 仮想機能 (VF) は、HYPER-V 子パーティションのゲスト オペレーティング システムで実行されます。 このため、VF のミニポート ドライバーは VF の PCI 構成領域などのハードウェア リソースを直接アクセスすることはできません。 ミニポート ドライバー PCIe 物理機能 (PF) にのみを VF の PCI 構成領域にアクセスできます。 PF のミニポート ドライバーでは、HYPER-V 親パーティションの管理オペレーティング システムで実行され、VF リソースへのアクセスには特権します。

など、仮想化スタックの上にある、ドライバーの OID セット要求を発行する[OID\_SRIOV\_書き込み\_VF\_CONFIG\_領域](https://msdn.microsoft.com/library/windows/hardware/hh451925)ときに、VF ミニポート ドライバー呼び出し[ **NdisMSetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563670) PCI 構成領域に書き込めません。

この OID セット要求を発行する前に、上にあるドライバーがのメンバーを設定する必要があります、[**NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_領域\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451688)次のように構造体。

-   設定、 **VFId**メンバー情報が書き込まれるの VF の識別子。

-   設定、**オフセット**データが書き込まれる VF の PCI 構成領域内のオフセットにメンバー。

-   設定、**長さ**VF の PCI 構成領域に書き込むバイト数のメンバー。

-   設定、 **BufferOffset** 、バッファー内のオフセットにメンバー (によって参照される、**InformationBuffer**メンバー) 指定した VF の PCI 構成領域に書き込まれたデータにが含まれます。 このオフセットがの先頭からバイト単位で指定された、 [ **NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_領域\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451688)構造体。

OID メソッド要求を処理するときに[OID\_SRIOV\_書き込み\_VF\_CONFIG\_領域](https://msdn.microsoft.com/library/windows/hardware/hh451925)、PF ミニポート ドライバーが次のガイドラインに従う必要があります。

-   PF のミニポート ドライバーは、VF がで指定されたを確認する必要があります、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_領域\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451688)構造体を以前に割り当てられているリソースします。 PF のミニポート ドライバーの OID メソッドの要求からの VF 用のリソースの割り当て[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。

    指定した VF 用のリソースが割り当てられていない場合、ドライバーは OID 要求に失敗する必要があります。

-   PF のミニポート ドライバー呼び出し[ **NdisMSetVirtualFunctionBusData** ](https://msdn.microsoft.com/library/windows/hardware/hh451526)要求 PCI 構成領域に書き込めません。 ただし、VF ドライバーが前のキャッシュの PCI 構成領域のデータの読み取りや書き込み PCI 構成領域の操作、PF ミニポート ドライバーも返します。

    **注**  独立系ハードウェア ベンダー (IHV) が SR-IOV 対応の一部としてバーチャル バス ドライバー (VBD) を提供する場合[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)、PF ミニポート ドライバーを呼び出してはならない[ **NdisMSetVirtualFunctionBusData**](https://msdn.microsoft.com/library/windows/hardware/hh451526)します。 代わりに、ドライバーをプライベートな通信チャネルを介して VBD とのインターフェイスし、VBD を呼び出すことを要求する必要があります[ *SetVirtualFunctionData*](https://msdn.microsoft.com/library/windows/hardware/hh451552)します。 この関数がから公開されている、 [GUID\_VPCI\_インターフェイス\_標準](https://msdn.microsoft.com/library/windows/hardware/hh451146)基になる仮想 PCI (VPCI) バス ドライバーによってサポートされているインターフェイス。

     

PF のミニポート ドライバーでは、OID 要求を正常に完了する場合、ドライバーは要求された PCI 構成の領域データをによって参照されるバッファーにコピーする必要があります、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 ドライバーで指定されたオフセットからバッファーへのデータのコピー、**BufferOffset**のメンバー、 [ **NDIS\_SRIOV\_読み取り\_VF\_構成\_領域\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451681)構造体。

 

 





