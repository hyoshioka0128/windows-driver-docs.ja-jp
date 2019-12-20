---
title: USB リモート NDIS の概要
description: USB リモート NDIS の概要
ms.assetid: 05714f49-38bc-4a36-83db-2eeb16c6add6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d87b336dacf5b2412b144897acc0ae4b2a8fdb2f
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210758"
---
# <a name="usb-remote-ndis-overview"></a>USB リモート NDIS の概要




USB リモート NDIS デバイスは、2つのインターフェイスを備えた USB 通信デバイスクラス (CDC) デバイスとして実装されます。 抽象コントロール型の通信クラスインターフェイスと、データクラスインターフェイスを組み合わせて、USB リモート NDIS デバイスを表す単一の機能単位を形成します。 通信クラスインターフェイスには、イベント通知用のエンドポイントが1つ含まれており、コントロールメッセージに共有双方向コントロールエンドポイントを使用します。 データクラスインターフェイスには、データトラフィック用の2つのバルクエンドポイントが含まれています。

>[!NOTE]
>ユニバーサルシリアルバス (USB) 仕様のバージョン1.1 と2.0 について理解している  必要があります。 USB 通信デバイスクラス (CDC) の仕様は、参照として提案されます。 これらのドキュメントをご覧 https://www.usb.org します。

 

 

 





