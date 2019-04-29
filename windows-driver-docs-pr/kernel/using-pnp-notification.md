---
title: PnP 通知の使用
description: PnP 通知の使用
ms.assetid: cc6c9106-37b3-473c-bbd2-89701d698fdf
keywords:
- WDK PnP 通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93a866b086294e479ca227688f5ca751119950aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391068"
---
# <a name="using-pnp-notification"></a>PnP 通知の使用





PnP 環境でドライバーとアプリケーションは、コンピューターのデバイスの構成の変更に対応する必要があります。 たとえば、アプリケーションは、マシンに関心のあるデバイスが追加され、ドライバーは、特定のデバイス上の変更が発生した場合を知る必要があることを認識する必要があります。

PnP マネージャーでは、ドライバーとアプリケーションを特定の PnP イベントが発生したときに通知するためのメカニズムを提供します。 このセクションでは、カーネル モード コードでの PnP 通知を使用する方法について説明します。 ユーザー モード アプリケーションの作成者がに関するについては、Microsoft Windows SDK ドキュメントを参照してください、 **RegisterDeviceNotification**関数および関連する関数。

 

 




