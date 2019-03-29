---
title: ドライバーでの GUID の使用
description: ドライバーでの GUID の使用
ms.assetid: b70a2f64-dd7b-4d76-a4cf-dcb60ce0585c
keywords:
- WDK のカーネルをグローバルに一意の識別子
- Guid の WDK カーネル
- WDK の Guid 識別子
- ヘッダー ファイルの WDK Guid
- カーネル モード ドライバー WDK、Guid
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20a1d8436168de8e8de29c676a43a5bd6e6b9f9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574362"
---
# <a name="using-guids-in-drivers"></a>ドライバーでの GUID の使用





ドライバーと他のシステム コンポーネントを使用して、*グローバルに一意の識別子*さまざまなアイテムを識別するためには、(Guid)。 システム コンポーネントの Guid からの項目のなど定義[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)、PnP、WMI イベント、イベントおよびイベントを静止画像します。 ドライバー開発者はアイテムの Guid をなど、作成できる[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)イベント、およびカスタムの WMI イベントは、カスタム PnP します。 ドライバーとアプリケーションには、使用する Guid を定義するヘッダー ファイルが含まれます。

ここでは、次のトピックについて説明します。

[定義と新しい Guid をエクスポートします。](defining-and-exporting-new-guids.md)

[ドライバー コードに Guid を含む](including-guids-in-driver-code.md)

ユーザー モード アプリケーションで Guid を使用する方法の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




