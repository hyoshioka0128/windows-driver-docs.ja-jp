---
title: NFP 電源管理
description: NFP 電源管理
ms.assetid: A47F4B01-A912-410A-8CF8-656D2C125148
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f420cb0b1d259a46e4181b0c853caad1170dd5ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834041"
---
# <a name="nfp-power-management"></a>NFP 電源管理


NFP デバイスは、3つの電源モードのいずれかで動作します。 これらのモードは、*アクティブ*、*アイドル*、*スタンバイ*、および*電源が削除*されています。 デバイスに対するパブリケーションまたはサブスクリプションが無効になっている場合は、NFP デバイスを低電力モードにすることができます。 NFP ドライバーは、Windows からの通知の有効化または無効化に応じて、デバイスをいずれかの電源モードに切り替えます。

NFP ドライバーは、 [ **\_nfp\_enable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_enable)または[**IOCTL\_\_nfp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable)を受信して、サブスクリプション、パブリケーション、およびプレゼンスイベントを有効または無効にする制御コードを無効にします。 これらの制御コードは、デバイスの電源モードの変更もトリガーします。 [接続されているスタンバイプラットフォームの近距離通信 (NFP) 電源管理](https://docs.microsoft.com/windows-hardware/design/device-experiences/near-field-promiximity--nfp--power-management-for-modern-standby-platforms)に関するトピックでは、NFP デバイスの電源モードの変更について詳しく説明しています。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

