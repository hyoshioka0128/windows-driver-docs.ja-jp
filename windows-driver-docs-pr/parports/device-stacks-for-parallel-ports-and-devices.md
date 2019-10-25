---
title: パラレル ポートとデバイスのデバイス スタック
description: パラレル ポートとデバイスのデバイス スタック
ms.assetid: 80222ed9-f900-4d97-b459-2d8ca780e1d1
keywords:
- システム提供のパラレルドライバー WDK、デバイススタック
- デバイススタック WDK パラレルドライバー
- パラレルデバイス WDK、デバイススタック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c07e3f97d17a71bce511c9fbcc2fb890d7deef4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831485"
---
# <a name="device-stacks-for-parallel-ports-and-devices"></a>パラレル ポートとデバイスのデバイス スタック





このセクションでは、並列ポートとパラレルポートに接続されているデバイスに対して、システムによって提供されるパラレルドライバーによって作成されるデバイススタックについて説明します。

次の図は、並列ポートとパラレルポートに接続されているデバイスに対して、システム提供のパラレルドライバーによって作成されるデバイススタックの種類を示しています。

![パラレルポートとデバイスの windows デバイスとドライバースタックを示す図](images/parport4.png)

パラレルポートに接続されている並列デバイス用のベンダー提供の関数ドライバーはオプションです。 システムによって提供されるパラレルドライバーは、並列デバイスを生のデバイスとして直接制御し、デバイスの親パラレルポートを制御するための広範なサポートを提供します。

パラレルポートおよびパラレルポートに接続されているデバイスを操作する方法の詳細については、以下を参照してください。

[パラレルデバイスインターフェイス、内部名、およびシンボリックリンク](parallel-device-interfaces--internal-names--and-symbolic-links.md)

[パラレルポートとデバイスの IOCTL およびコールバックのサポート](ioctl-and-callback-support-for-parallel-ports-and-devices.md)

[パラレルポートの操作](operating-a-parallel-port.md)

[パラレルポートに接続されているパラレルデバイスの操作](operating-a-parallel-device-attached-to-a-parallel-port.md)

[システム提供のパラレルドライバーへのクライアントインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 




