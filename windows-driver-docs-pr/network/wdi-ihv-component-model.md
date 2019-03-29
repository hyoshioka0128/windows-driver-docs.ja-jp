---
title: WDI IHV コンポーネント モデル
description: このセクションでは、WDI ミニポート ドライバーとそれらのインターフェイスの期待値の NDIS インターフェイスの概要を示します。IHV コンポーネント WDI モデルでは、NDIS ミニポートです。
ms.assetid: FF670015-BB70-4703-BBA9-69130213D7D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d7a7f698be54a2cfcc85a03cf1bea92ab34d01a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578756"
---
# <a name="wdi-ihv-component-model"></a>WDI IHV コンポーネント モデル


このセクションでは、WDI ミニポート ドライバーとそれらのインターフェイスの期待値の NDIS インターフェイスの概要を示します。

IHV コンポーネント WDI モデルでは、NDIS ミニポートです。 オペレーティング システムおよび既存および新規の NDIS Api を使用して、ネットワーク スタックとのインターフェイスします。 Microsoft の WLAN のコンポーネントは、WDI IHV ミニポート ドライバーとオペレーティング システムの残りの部分間に配置します。 WDI インターフェイスと既存の NDIS/ネイティブ WLAN インターフェイス間のマッピングを提供します。 WDI コマンドは新しい NDIS Oid としてパッケージ化し、WDI インジケーターは新しい NDIS 兆候としてパッケージ化します。 使用して、データ パスが対話する[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体の新しいハンドラーを使用します。

次の図は、全体的なアーキテクチャのレイアウトと、サンプル メッセージのフロー (PNP アクション、Oid、および送信) オペレーティング システムから以前のネイティブ WLAN モデルと新しい WDI WLAN モデルの両方を IHV ミニポート ドライバーに示します。

![ネイティブ wi-fi および wdi ドライバーの比較](images/wdi-model-comparison.png)

だけでなく、ネイティブ Wi-fi インターフェイス要件を支援する、Microsoft の WLAN のコンポーネントは、共通の NDIS 要件のほとんども処理します。 たとえば、処理、 [ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418) NDIS 要件が満たされていることを確認するメッセージ WDI データとコントロールのパスに変換し、NDIS から要件。 ただし、IHV ミニポート ドライバー追加を実行する機能もあります。 通知を受けることができます、ドライバー *MiniportPause*中に実行したいその他のクリーンアップを実行する呼び出し*MiniportPause*します。

 

 





