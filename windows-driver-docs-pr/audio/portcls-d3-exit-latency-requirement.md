---
title: PortCls D3 終了遅延の要件
description: このトピックでは、Windows ポートクラスドライバー (PortCls) が新しい Windows 8 インターフェイスを使用して、D3 スリープ状態の終了待機時間の要件を操作する方法について説明します。
ms.assetid: 3CEFF85B-5A2E-4F85-BCAC-00F1773A8F4D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e0f77ecf7f929fb6056254756b60439d8897f42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832468"
---
# <a name="portcls-d3-exit-latency-requirement"></a>PortCls D3 終了遅延の要件


このトピックでは、Windows ポートクラスドライバー (PortCls) が新しい Windows 8 インターフェイスを使用して、D3 スリープ状態の終了待機時間の要件を操作する方法について説明します。

システムが完全に動作している (たとえば、スリープまたはコネクトスタンバイ) 以外のプラットフォームの電源状態になると、オーディオアダプターが D0 (完全に動作) に戻るために必要な終了待機時間が緩やかになる可能性があります。 これにより、このようなより深い状態が終了待機時間 (終了時間) を超える可能性がある場合でも、オーディオアダプターが D3 より深いスリープ状態を使用できるようになります。

PortCls は新しい電源管理インターフェイスを使用して、新しい D3 終了待機時間の許容範囲を生成し、オーディオミニポートドライバーに動的に伝達できるようになりました。 これらの許容範囲は、 [**PC\_終了\_待機時間**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ne-portcls-_pc_exit_latency)列挙値として表されます。

新しい電源管理インターフェイスの詳細については、IAdapterPowerManagement3 を参照してください。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement3)

 

 




