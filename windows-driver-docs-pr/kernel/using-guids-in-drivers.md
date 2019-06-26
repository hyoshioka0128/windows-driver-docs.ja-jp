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
ms.openlocfilehash: e0e1fd0ee1470f8d5711473a3e8af6bcace5433c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381640"
---
# <a name="using-guids-in-drivers"></a>ドライバーでの GUID の使用





ドライバーと他のシステム コンポーネントを使用して、*グローバルに一意の識別子*さまざまなアイテムを識別するためには、(Guid)。 システム コンポーネントの Guid からの項目のなど定義[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)、PnP、WMI イベント、イベントおよびイベントを静止画像します。 ドライバー開発者はアイテムの Guid をなど、作成できる[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)イベント、およびカスタムの WMI イベントは、カスタム PnP します。 ドライバーとアプリケーションには、使用する Guid を定義するヘッダー ファイルが含まれます。

ここでは、次のトピックについて説明します。

[定義と新しい Guid をエクスポートします。](defining-and-exporting-new-guids.md)

[ドライバー コードに Guid を含む](including-guids-in-driver-code.md)

ユーザー モード アプリケーションで Guid を使用する方法の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




