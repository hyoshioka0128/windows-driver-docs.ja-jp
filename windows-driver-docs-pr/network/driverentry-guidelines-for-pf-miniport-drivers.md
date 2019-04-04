---
title: PF ミニポート ドライバー DriverEntry ガイドライン
description: PF ミニポート ドライバー DriverEntry ガイドライン
ms.assetid: 6F885379-41EC-411E-8909-4DF48042849A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fed229f0560c68aa6052116c210254e4323cfc86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537350"
---
# <a name="driverentry-guidelines-for-pf-miniport-drivers"></a>PF ミニポート ドライバー DriverEntry ガイドライン


このトピックでは、書き込みのためのガイドラインを説明します、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff548818)ミニポート ドライバーの PCI Express (PCIe) 物理機能 (PF) の関数。 PF は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターのコンポーネントです。

**注**  次のガイドラインは、PF ミニポート ドライバーにのみ適用されます。 PCIe 仮想機能 (VF) アダプターのミニポート ドライバーの初期化ガイドラインについては、[VF のミニポート ドライバーの初期化](initializing-a-vf-miniport-driver.md)を参照してください。

 

SR-IOV ネットワーク アダプターには、アダプターの物理ポートと内部仮想ポート (拡張) 経由でネットワーク トラフィックを転送するハードウェア ブリッジを実装する必要があります。 このブリッジと呼ばれる、 *NIC スイッチ*します。 詳細については、[NIC スイッチ](nic-switches.md)を参照してください。

PF のミニポート ドライバーでは、SR-IOV ネットワーク アダプターの静的 NIC スイッチの作成をサポートする場合は、デバイス スタック内のネットワーク アダプターの機能のデバイス オブジェクト (FDO) が作成されるときに、スイッチのリソースを割り当てる必要があります。 この場合、ドライバーが NDIS 呼び出される前にこれらのリソースを割り当てる必要があります[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)します。 これを行うには、アダプターの FDO を追加またはデバイス スタックから削除されたときに、プロセスに参加するように、ドライバーは省略可能なプラグ アンド プレイ (PnP) ハンドラーを登録する必要があります。

ミニポート ドライバーを提供する必要があります、 [ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)これら PnP ハンドラー関数を登録する関数。 これを行うには、ドライバーはへの呼び出しのコンテキストからこれらの手順を次の[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff548818)関数。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)のエントリ ポイントを含む構造体、 *MiniportXxx*関数。 具体的には、ドライバーの設定、 **SetOptionsHandler**のドライバーのエントリ ポイントをメンバー [ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数。

2.  ミニポート ドライバーの呼び出し、 [ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)そのエントリ ポイントを登録する関数。 NDIS ドライバーの呼び出し、この呼び出しのコンテキストから[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数

3.  NDIS を呼び出すと[ *MiniportSetOptions*](https://msdn.microsoft.com/library/windows/hardware/ff559443)、ミニポート ドライバーの呼び出し、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数を指定します。[ **NDIS\_ミニポート\_PNP\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566475)構造体。 この構造体のエントリ ポイントを定義する、 [ *MiniportAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559332)、 [ *MiniportRemoveDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559427)、 [ *MiniportStartDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559452)、および[ *MiniportFilterResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff559384)関数。 NDIS は、PCI バス ドライバーによって発行された PnP I/O 要求パケット (Irp) を処理するときに、これらのハンドラー関数を呼び出します。

    NDIS ドライバーを呼び出す前に、PF ミニポート ドライバーする必要があります NIC スイッチに追加のソフトウェアのリソースを割り当てるかどうか[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数の場合、ドライバーを登録する必要があります、 [*MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)関数。 NDIS を呼び出すと、 *MiniportAddDevice* PF ミニポート ドライバーが呼び出すことができます関数、 [**エミュレーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564511) NIC スイッチ構成キーワードの設定を読み取るレジストリから。 これらのキーワードの詳細については、[SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)を参照してください。

    に関するガイドラインの詳細については、 [ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)関数を参照してください[ *MiniportAddDevice* PF ミニポート ドライバーに関するガイドライン](miniportadddevice-guidelines-for-pf-miniport-drivers.md).

NIC のスイッチを作成する方法の詳細については、[NIC スイッチの作成](creating-a-nic-switch.md)を参照してください。

 

 





