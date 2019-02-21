---
title: PF のミニポート ドライバーからのバック チャネル通信
description: PF のミニポート ドライバーからのバック チャネル通信
ms.assetid: 819FC32C-D50C-480F-AE6E-078E4ECD3400
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41a5b398954508f6b86cd0aab2bdbbac9b8feb47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538086"
---
# <a name="backchannel-communication-from-the-pf-miniport-driver"></a>PF のミニポート ドライバーからのバック チャネル通信


ミニポート ドライバーの PCI Express (PCIe) 物理機能 (PF) は、VF 構成ブロックのデータの変更に関する問題の通知を PCIe 仮想機能 (VF) のミニポート ドライバーと通信します。 PF のミニポート ドライバーの問題をこれらの通知*が無効になる*VF 構成ブロック内のデータ。 この通知に応答して、VF のミニポート ドライバーは、無効化された、VF 構成ブロックから、データを読み取る PF ミニポート ドライバーに backchannel 要求を発行できます。

VF 構成ブロックは、PF と VF のミニポート ドライバーの間のバック チャネル通信に使用されます。 IHV は、デバイスの 1 つ以上の VF 構成ブロックを定義できます。 各 VF 構成ブロックは、IHV で定義された形式、長さ、およびブロック id。

**注**  各 VF 構成ブロックからのデータは、PF と VF のミニポート ドライバーでのみ使用します。 形式とデータの内容は、Windows オペレーティング システムのコンポーネントに対して非透過的です。

 

次の手順は、発行し、無効な VF 構成データの通知を処理するときに発生します。

1.  NDIS、ゲスト オペレーティング システムの I/O 制御要求を発行[ **IOCTL\_VPCI\_INVALIDATE\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/hh439301)します。 この IOCTL が完了したら、NDIS は VF 構成データが変更されたことが通知されます。

2.  HYPER-V 親パーティションで実行されている、管理オペレーティング システムでは、次の手順が発生します。

    1.  PF のミニポート ドライバー呼び出し、 [ **NdisMInvalidateConfigBlock** ](https://msdn.microsoft.com/library/windows/hardware/hh451517) VF 構成データが変更され、無効になっている NDIS に通知します。 ドライバーのセット、 *BlockMask* VF 構成ブロックを指定する ULONGLONG ビットマスクにパラメーターが変更されました。 ビットマスクの各ビットは、VF 構成ブロックに対応します。 ビットが 1 つに設定されている場合、対応する VF 構成ブロック内のデータが変更されました。
    2.  NDIS は、VF 構成ブロックのデータへの変更について、管理オペレーティング システムで実行される仮想化スタックを通知します。 仮想化スタックは、キャッシュ、 *BlockMask*パラメーターのデータ。

        **注**  PF ミニポート ドライバーを呼び出すたびに[ **NdisMInvalidateConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451517)、仮想化スタックの Or、 *BlockMask*キャッシュに現在の値を持つパラメーターのデータ。

         

    3.  仮想化スタックでは、VF 構成データの無効化について、ゲスト オペレーティング システムで実行される仮想の PCI (VPCI) ドライバーに通知します。 仮想化スタックは、キャッシュされた送信*BlockMask* VPCI ドライバーにパラメーターのデータ。

3.  HYPER-V 子パーティションで実行されている、ゲスト オペレーティング システムでは、次の手順が発生します。

    1.  VPCI ドライバーは、キャッシュされた保存*BlockMask*でパラメーターのデータ、 **BlockMask**のメンバー、 [ **VPCI\_INVALIDATE\_ブロック\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh451586)構造に関連付けられている、 [ **IOCTL\_VPCI\_INVALIDATE\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/hh439301)要求。

    2.  VPCI ドライバーが正常に完了、 [ **IOCTL\_VPCI\_INVALIDATE\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/hh439301)要求。 このような場合は、NDIS の問題のオブジェクト識別子 (OID) メソッド要求[OID\_SRIOV\_VF\_INVALIDATE\_CONFIG\_ブロック](https://msdn.microsoft.com/library/windows/hardware/hh451903)VF ミニポート ドライバーにします。 [ **NDIS\_SRIOV\_VF\_INVALIDATE\_CONFIG\_ブロック\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451684) OID 要求で渡されますが。 この構造体が含まれていますが、キャッシュされた*BlockMask*パラメーターのデータ。

        NDIS 別問題も[ **IOCTL\_VPCI\_INVALIDATE\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/hh439301) VF 構成データの変更の連続する通知を処理するために要求します。

    3.  VF ドライバーが処理するときに、 [OID\_SRIOV\_VF\_INVALIDATE\_CONFIG\_ブロック](https://msdn.microsoft.com/library/windows/hardware/hh451903)要求によって指定された、VF 構成要素からデータを読み取ることできます呼び出す[ **NdisMReadConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)します。 このプロセスの詳細については、次を参照してください。 [VF のミニポート ドライバーからのバック チャネル通信](backchannel-communication-from-a-vf-miniport-driver.md)します。

 

 





