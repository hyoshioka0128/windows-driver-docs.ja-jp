---
title: WDI IHV コンポーネントモデル
description: このセクションでは、WDI ミニポートドライバーの NDIS インターフェイスの概要と、これらのインターフェイスに対する期待について説明します。WDI モデルの IHV コンポーネントは、NDIS ミニポートです。
ms.assetid: FF670015-BB70-4703-BBA9-69130213D7D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59079d4d9a638b6d49e7fff1eaba3d48c076420a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842927"
---
# <a name="wdi-ihv-component-model"></a>WDI IHV コンポーネントモデル


このセクションでは、WDI ミニポートドライバーの NDIS インターフェイスの概要と、これらのインターフェイスに対する期待について説明します。

WDI モデルの IHV コンポーネントは、NDIS ミニポートです。 既存および新しい NDIS Api を使用して、オペレーティングシステムとそのネットワークスタックとのインターフェイスを作成します。 Microsoft WLAN コンポーネントは、WDI IHV ミニポートドライバーとその他のオペレーティングシステムの間にあります。 これは、WDI インターフェイスと、既存の NDIS/ネイティブ WLAN インターフェイスとの間のマッピングを提供します。 WDI コマンドは新しい NDIS Oid としてパッケージ化され、WDI の兆候は新しい NDIS の兆候としてパッケージ化されています。 データパスは、新しいハンドラーを使用して、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を介してやり取りします。

次の図は、アーキテクチャの全体的なレイアウトと、オペレーティングシステムから、古いネイティブ WLAN モデルと新しい WDI WLAN モデルの両方の IHV ミニポートドライバーへのメッセージのサンプルフロー (PNP アクション、Oid、送信) を示しています。

![ネイティブ wi-fi と wdi ドライバーの比較](images/wdi-model-comparison.png)

Microsoft WLAN コンポーネントは、ネイティブ Wi-fi インターフェイスの要件を支援するだけでなく、多くの一般的な NDIS 要件も処理します。 たとえば、ndis の[*Miniportpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)要件を処理し、それらを WDI データと制御パスメッセージに変換して、ndis 要件が満たされるようにします。 ただし、IHV ミニポートドライバーは、追加の作業を行う機能も提供します。 このドライバーは *、miniportpause 呼び出しで*通知されるように登録できます。これにより、 *miniportpause*中に実行する追加のクリーンアップが実行されます。

 

 





