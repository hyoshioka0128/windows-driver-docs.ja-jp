---
title: 電源メーター インターフェイス
description: 電源メーター インターフェイス
ms.assetid: be3ffb33-f1da-403d-b888-378ffd5cac8a
keywords:
- 使用状況の測定と予算の WDK の電源をインターフェイス
- 電力メーター インターフェイス WDK
- PMI WDK 電源メーター
ms.date: 10/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: d419a271efd49519779a60d9db1501835bcad6f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331802"
---
# <a name="power-meter-interface"></a>電源メーター インターフェイス


電源メーター インターフェイス (PMI) は I/O 要求パケット (Irp) サービスを提供する WDM ドライバーを通じて提供されます、[電源マネージャー](https://msdn.microsoft.com/library/windows/hardware/ff559829)の電源の WMI プロバイダー コンポーネントと、[ユーザー モードの Power サービス](user-mode-power-service.md)(UMPS)。

PMI では、ユーザー モード サービスまたはアプリケーションによって発行される I/O 制御 (IOCTL) 要求パケットのさまざまなサポートを提供します。 この IOCTL インターフェイスは、次の項目に関する情報を提供します。

-   電源の使用状況測定機能、電源メーターの構成。 これには、サンプリング間隔と電源のしきい値が含まれます。

-   電力メーターの電力予算構成。

-   ベンダーの名前と、測定のシリアル番号などの電力メーターの資産情報。

-   現在の電力レベルと予算の情報。

PMI には、電力のしきい値または予算に達したか超えましたなどのイベントの使用状況測定の電源の通知のサポートも提供します。

使用状況測定情報 PMI からアクセスされる電源は通常読み取り専用です。 ただし、電力メーターの機能、によってその予算構成でしたが読み取り専用または読み取り/書き込みアクセス許可。

PMI IOCTL インターフェイスの詳細については、次を参照してください。 [PMI Ioctl](https://msdn.microsoft.com/library/windows/hardware/ff543884)します。

 
**注**   PMB インフラストラクチャは、Windows 7、Windows Server 2008 R2、および以降のバージョンの Windows オペレーティング システムでサポートされています。


 




