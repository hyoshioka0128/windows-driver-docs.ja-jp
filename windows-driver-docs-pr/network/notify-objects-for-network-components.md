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
ms.openlocfilehash: 1de7f990d6c7e3a445931d8f8848d9a3f25b2df9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571609"
---
# <a name="notify-objects-for-network-components"></a>ネットワーク コンポーネントの通知オブジェクト





A*通知オブジェクト*に代わって特定のネットワーク コンポーネントのオブジェクトへのネットワーク構成サブシステムによって送信される通知を処理します。 通知オブジェクト ダイナミック リンク ライブラリ (DLL) によって提供されます。 通知オブジェクトは、ネットワーク コンポーネントのプロパティ ページを表示して、ネットワーク構成をそのコンポーネントのプログラムで制御するために使用されます。

**注**  ネットワーク コンポーネントは通常不要通知オブジェクトの両方の次の条件に該当する場合。

 

-   ネットワーク コンポーネントをインストールしてその情報 (INF) ファイルを使用して削除できます。

-   ネットワーク構成の変更に反応は必須ではありません。

次のセクションで説明オブジェクトに通知し、それらを開発する方法について説明します。

[約オブジェクトに通知します。](about-notify-objects.md)

[通知オブジェクトを作成します。](creating-a-notify-object.md)

リファレンス情報については、インターフェイス メソッドのサポート オブジェクトに通知する、次を参照してください。[通知オブジェクト](https://msdn.microsoft.com/library/windows/hardware/ff559161)します。

 

 





