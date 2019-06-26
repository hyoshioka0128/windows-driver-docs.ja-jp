---
title: PortCls D3 終了遅延の要件
description: このトピックでは、Windows ポート クラス ドライバー (PortCls) が Windows 8 の新しいインターフェイスを使用して、D3 のスリープ状態の終了の待機時間の要件を操作する方法について説明します。
ms.assetid: 3CEFF85B-5A2E-4F85-BCAC-00F1773A8F4D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6806439ae169eedb85983a071f8346a1c54f53b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362561"
---
# <a name="portcls-d3-exit-latency-requirement"></a>PortCls D3 終了遅延の要件


このトピックでは、Windows ポート クラス ドライバー (PortCls) が Windows 8 の新しいインターフェイスを使用して、D3 のスリープ状態の終了の待機時間の要件を操作する方法について説明します。

システムが完全に (たとえば、スリープ状態またはコネクト スタンバイ) の操作、(完全に動作) D0 に返されるオーディオのアダプターの必要な終了の待機時間以外のプラットフォームの電源状態に入ったときが緩和されます。 これにより、D3 よりも深くのスリープ状態を使用するオーディオのアダプターの場合でも、これらの詳細な状態が (終了時間) 待機時間が長い終了になる可能性があります。

PortCls は今すぐ新しい電源管理インターフェイスを使用して、新しい D3 終了の待機時間の許容範囲を生成して、オーディオのミニポート ドライバーを動的に通信します。 これらの許容範囲を表したもの[ **PC\_終了\_待機時間**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ne-portcls-_pc_exit_latency)列挙値。

新しい電源管理のインターフェイスの詳細については、次を参照してください[ **IAdapterPowerManagement3。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement3)

 

 




