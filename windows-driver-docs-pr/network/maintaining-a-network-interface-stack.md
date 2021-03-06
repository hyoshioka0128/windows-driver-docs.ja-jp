---
title: ネットワーク インターフェイス スタックの保守
description: ネットワーク インターフェイス スタックの保守
ms.assetid: c51a2e5b-28ad-4e86-8b37-1491f85a17bb
keywords:
- NDIS ネットワーク インターフェイス、WDK スタック メンテナンス
- ネットワーク インターフェイスの WDK、スタックのメンテナンス
- スタックの WDK ネットワーク
- stack テーブル WDK のネットワークをインターフェイスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d06baba22acf836f0dc3fc0bdaaa3b4759f20c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356190"
---
# <a name="maintaining-a-network-interface-stack"></a>ネットワーク インターフェイス スタックの保守





NDIS インターフェイスの履歴テーブルを維持するためにサービスを提供します (*ifStackTable*で RFC 2863)。 NDIS は、NDIS ミニポート アダプター、NDIS 5 スタックのテーブルを保持します。*x*中間のドライバーおよび NDIS フィルター モジュールをフィルター処理します。 NDIS には、NDIS ドライバーを追加し、このテーブル内のエントリの削除を有効にするサービスも提供します。 MUX 中間ドライバーでは、NDIS に仮想ミニポート インターフェイスとプロトコルの低いインターフェイス間のリレーションシップへのアクセスはありません。 そのため、NDIS 6.0 MUX 中間ドライバーでは、これらの内部インターフェイス リレーションシップを指定する必要があります。

2 つのインターフェイスに関係するスタックを定義する NDIS ドライバーを渡すことができます*HigherLayerIfIndex*と*LowerLayerIfIndex*パラメーターを[ **NdisIfAddIfStackEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifaddifstackentry)関数。 これらのパラメーターは、ネットワーク インターフェイスのスタックとの下位のスタックにする必要がある 1 つのネットワーク インターフェイスの上位にする必要がある 1 つのネットワーク インターフェイスを指定します。

別のインターフェイス (たとえば、内部バインド MUX 中間ドライバーで NDIS に表示されていない) に関連するインターフェイスのスタック順序情報を持つドライバーは呼び出し**NdisIfAddIfStackEntry**を設定する、インターフェイスの履歴テーブルです。 この関数は、NDIS を返します\_状態\_スタック エントリが正常に行われた場合は成功します。 所有または上位のレイヤー インターフェイスのインターフェイスのプロバイダーは、コンポーネントでは通常、(この*HigherLayerIfIndex*識別) 呼び出し**NdisIfAddIfStackEntry**します。

履歴テーブルのエントリを削除するドライバーに渡します*HigherLayerIfIndex*と*LowerLayerIfIndex*パラメーターを[ **NdisIfDeleteIfStackEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifdeleteifstackentry)関数。

インターフェイスのスタックを維持するための例では、MUX 6.0 のドライバーのサンプルを参照してください。

 

 





