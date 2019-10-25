---
title: ソフトウェア専用ドライバーでの PnP と電源管理のサポート
description: ソフトウェア専用ドライバーでの PnP と電源管理のサポート
ms.assetid: bcfca8b2-68d6-4875-8687-27351becd6f4
keywords:
- PnP WDK KMDF、ソフトウェアのみのドライバー
- WDK KMDF、ソフトウェアのみのドライバープラグアンドプレイ
- 電源管理 WDK KMDF、ソフトウェアのみのドライバー
- ソフトウェア専用ドライバー WDK KMDF
- ドライバーのフィルター WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 699ae5c70a48db5a94fb8017501a050a88d045c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831717"
---
# <a name="supporting-pnp-and-power-management-in-software-only-drivers"></a>ソフトウェア専用ドライバーでの PnP と電源管理のサポート


*ソフトウェアのみのドライバー*は、どのハードウェアにもアクセスしないドライバーです。 一部のソフトウェアのみのドライバーは、ハードウェアにアクセスしないドライバースタックに存在します。 これらのドライバーはハードウェアにアクセスしないため、通常、PnP や電源管理操作を実行する必要はありません。

その他のソフトウェア専用ドライバーはフィルタードライバーであり、ハードウェアにアクセスするドライバーのスタックに存在しますが、フィルタードライバーはハードウェアにアクセスしません。 PnP または電源管理操作を指定する i/o 要求をフィルタードライバーが受け取った場合、ドライバーは通常、要求を次のドライバーに渡すだけです。 フレームワークは、これらの要求をインターセプトして渡します。そのため、フレームワークベースのドライバーは要求を認識しません。

ソフトウェアのみのドライバーを作成する場合、ドライバーは[デバイスオブジェクトを作成し](creating-a-framework-device-object.md)ますが、通常は、PnP または電源管理イベントを処理するためのイベントコールバック関数を提供する必要はありません。 ドライバーが[フレームワークキューオブジェクト](framework-queue-objects.md)を使用する場合は、キューの[**WDF\_IO\_queue\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)構造体の**powermanaged**メンバーを**WdfFalse**または**wdfusedefault**に設定する必要があります。

一部のソフトウェアのみのドライバーは、[関数ドライバー](supporting-pnp-and-power-management-in-function-drivers.md)でもあります。 つまり、ハードウェアにアクセスしない仮想デバイスと、ハードウェアデバイスをサポートする関数ドライバーとして、単一のドライバーがソフトウェア専用のドライバーとして機能する場合があります。

 

 





