---
title: NetAdapterCx クライアント ドライバーの電源切断シーケンス
description: NetAdapterCx クライアント ドライバーの電源切断シーケンス
ms.assetid: 9E16172C-9E45-4ED7-B6D2-7539DF4718B5
keywords:
- NetAdapterCx クライアント ドライバーの電源切断シーケンス
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5aa3117c75c03162bb715a0538f164600412434e
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209012"
---
# <a name="power-down-sequence-for-a-netadaptercx-client-driver"></a>NetAdapterCx クライアント ドライバーの電源切断シーケンス

次の図は、デバイスの電源をオンにして削除するときに、NetAdapterCx がクライアントドライバーのイベントコールバック関数を呼び出す順序を示しています。 シーケンスは、動作中の電源状態 (D0) にある操作デバイスを使用して、図の上部から開始します。

<img src="images/netadaptercx-powerdown.png" alt="Device enumeration and power-down sequence for NetAdapterCx client driver" title="NetAdapterCx クライアントドライバーのデバイス列挙と電源ダウンシーケンス" style="width: 600px;"/>

大まかな横線は、デバイスの電源を切るために必要な手順を示しています。 図の左側の列には手順が記述されており、右側の列には、それを実現するイベントコールバックが一覧表示されます。 青いテキストでマークされた手順は NetAdapterCx に固有であり、他の手順はすべての WDF ベースのドライバーに共通です。

図に示すように、電源ダウンと削除のシーケンスでは、対応する "元に戻す" コールバックを、デバイスを操作するために使用する関数をフレームワークが呼び出した逆の順序で呼び出す必要があります。 デバイスオブジェクトのコンテキスト領域を削除すると、そのオブジェクトが削除されます。
