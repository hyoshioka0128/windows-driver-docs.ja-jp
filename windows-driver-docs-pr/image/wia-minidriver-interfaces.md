---
title: WIA ミニドライバー インターフェイス
description: WIA ミニドライバー インターフェイス
ms.assetid: 6d069584-f9e1-4312-b8f2-1ef3d518faeb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb3139e10bab9a6c3cabeb1c911e47aa51d26877
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840677"
---
# <a name="wia-minidriver-interfaces"></a>WIA ミニドライバー インターフェイス





WIA ミニドライバーは、標準の**IUnknown** com インターフェイス (Microsoft Windows SDK のドキュメントで説明されています) と、その他の2つの wia 固有のインターフェイス ( [i usd](istiusd-com-interface.md)と[IWIAMINIDRV](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)) を実装する COM オブジェクトです。

### <a name="istiusd-interface"></a>I(米国) インターフェイス

*米国ドル*で定義されている**it usd**インターフェイスは、次のアクションを実行します。

-   WIA サービスが最初に読み込むときにドライバーを初期化します。

-   デバイスが非同期デバイス通知をサポートしているかどうかを報告するために、ドライバーの機能を WIA サービスに返します。

-   デバイスのロックとロック解除を排他的に使用します。

### <a name="iwiaminidrv-interface"></a>IWiaMiniDrv インターフェイス

*Wiamindr*で定義されているインターフェイスでは、ほとんどの WIA ミニドライバーの機能が公開されています。 このインターフェイスは、次のアクションを実行します。

-   静止イメージデバイスの既定値と現在の設定を定義します。

-   静止イメージデバイスでサポートされているコマンドとイベントを定義します。

-   デバイスから WIA サービスにデータを転送します (最終的には、呼び出し元のアプリケーションに渡されます)。

これらのインターフェイスの詳細については、「 [WIA ドライバーの開発: 基本的な概念](developing-a-wia-driver--basic-concepts.md)」を参照してください。

 

 




