---
title: USB リモート NDIS の概要
description: USB リモート NDIS の概要
ms.assetid: 05714f49-38bc-4a36-83db-2eeb16c6add6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd33595210dd61bb4c83a6ca784f70b836887e1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340006"
---
# <a name="usb-remote-ndis-overview"></a>USB リモート NDIS の概要




リモートの NDIS の USB デバイスは、2 つのインターフェイスを使用した USB 通信デバイス クラス (CDC) デバイスとして実装されます。 抽象のコントロールの種類の通信クラス インターフェイスとデータ クラス インターフェイスを組み合わせて、リモート NDIS の USB デバイスを表す 1 つの機能単位を形成します。 クラスの通信インターフェイスは、イベント通知の 1 つのエンドポイントが含まれていて、コントロール メッセージの共有の双方向のコントロール エンドポイントを使用します。 データ クラス インターフェイスには、2 つの一括エンドポイント データ トラフィックが含まれています。

>[!NOTE]
> ユニバーサル シリアル バス (USB) 仕様のバージョン 1.1 および 2.0 の理解が必要です。 USB 通信デバイス クラス (CDC) 仕様は参照としてお勧めします。 これらのドキュメントをご覧 http://www.usb.orgします。

 

 

 





