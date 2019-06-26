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
ms.openlocfilehash: 8446945e110e8093bd3e790f2278049237f44979
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386523"
---
# <a name="nfp-power-management"></a>NFP 電源管理


NFP デバイスは、次の 3 つの電源モードのいずれかで動作します。 これらのモードは*active*、*アイドル*、*スタンバイ*、および*power 削除*します。 NFP デバイスは、パブリケーション、またはデバイスへのサブスクリプションが無効になっている低電力モードを入力できます。 NFP ドライバーを応答を有効にする電源モードのいずれかにデバイスを移行または Windows からの通知を無効にします。

NFP ドライバーが表示されます、 [ **IOCTL\_NFP\_を有効にする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_enable)または[ **IOCTL\_NFP\_無効**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_disable)有効またはサブスクリプション、パブリケーション、およびプレゼンスのイベントを無効にするコードを制御します。 これらの制御コードは、デバイスの電源モードの変更にもトリガーします。 [近距離近接 (NFP) の電源管理のコネクテッド スタンバイ プラットフォーム](https://docs.microsoft.com/windows-hardware/design/device-experiences/near-field-promiximity--nfp--power-management-for-modern-standby-platforms)トピック NFP デバイスの電源モードの変更の詳細な説明を提供します。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

