---
title: ネットワーク コンポーネントの通知オブジェクト
description: ネットワーク コンポーネントの通知オブジェクト
ms.assetid: 5b5c5da2-7163-44cf-8e8a-c736278f2535
keywords:
- オブジェクトの WDK ネットワークへの通知します。
- ネットワーク オブジェクト WDK に通知します。
- 通知の WDK ネットワーク
- ネットワーク コンポーネント オブジェクト WDK に通知します。
- プロパティ ページを表示します。
- プロパティ ページの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66be6a9120c3ffbc619b84c362691376759b6cdc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354535"
---
# <a name="notify-objects-for-network-components"></a>ネットワーク コンポーネントの通知オブジェクト





A*通知オブジェクト*に代わって特定のネットワーク コンポーネントのオブジェクトへのネットワーク構成サブシステムによって送信される通知を処理します。 通知オブジェクト ダイナミック リンク ライブラリ (DLL) によって提供されます。 通知オブジェクトは、ネットワーク コンポーネントのプロパティ ページを表示して、ネットワーク構成をそのコンポーネントのプログラムで制御するために使用されます。

**注**  ネットワーク コンポーネントは通常不要通知オブジェクトの両方の次の条件に該当する場合。

 

-   ネットワーク コンポーネントをインストールしてその情報 (INF) ファイルを使用して削除できます。

-   ネットワーク構成の変更に反応は必須ではありません。

次のセクションで説明オブジェクトに通知し、それらを開発する方法について説明します。

[約オブジェクトに通知します。](about-notify-objects.md)

[通知オブジェクトを作成します。](creating-a-notify-object.md)

リファレンス情報については、インターフェイス メソッドのサポート オブジェクトに通知する、次を参照してください。[通知オブジェクト](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559161(v=vs.85))します。

 

 





