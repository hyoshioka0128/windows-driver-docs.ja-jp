---
title: 電源メーター インターフェイス
description: 電源メーター インターフェイス
ms.assetid: be3ffb33-f1da-403d-b888-378ffd5cac8a
keywords:
- 電力使用状況測定と予算 WDK、インターフェイス
- 電源メーターインターフェイス WDK
- PMI WDK 電源メーター
ms.date: 10/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c1cae3c35e2e9ced9a9b588381de94620497328
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829022"
---
# <a name="power-meter-interface"></a>電源メーター インターフェイス


電源メーターインターフェイス (PMI) は、[電源マネージャー](https://docs.microsoft.com/windows-hardware/drivers/kernel/power-manager)からの i/o 要求パケット (irp)、および[ユーザーモードの電源サービス](user-mode-power-service.md)(UMPS) の電源 WMI プロバイダーコンポーネントを処理する WDM ドライバーによって提供されます。

PMI では、ユーザーモードのサービスまたはアプリケーションによって発行されたさまざまな i/o 制御 (IOCTL) 要求パケットがサポートされています。 この IOCTL インターフェイスは、次の項目に関する情報を提供します。

-   電力測定機能と電源メーターの構成。 これには、サンプリング間隔と電力のしきい値が含まれます。

-   電源メーターの電力の割り当ての構成。

-   ベンダーの名前やメーターのシリアル番号など、電力メーターの資産情報。

-   現在の電源レベルと予算の情報。

PMI では、電力のしきい値や予算に達した場合や超過した場合など、電力測定イベントの通知もサポートされます。

PMI からアクセスされる電力使用状況測定情報は、通常、読み取り専用です。 ただし、電力メーターの機能によっては、その予算構成に読み取り専用または読み取り/書き込みのアクセス許可が与えられる場合があります。

PMI IOCTL インターフェイスの詳細については、「 [Pmi ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/pmi/index)」を参照してください。

 
**  ** pmb インフラストラクチャは、windows 7、windows Server 2008 R2、およびそれ以降のバージョンの windows オペレーティングシステムでサポートされています。


 




