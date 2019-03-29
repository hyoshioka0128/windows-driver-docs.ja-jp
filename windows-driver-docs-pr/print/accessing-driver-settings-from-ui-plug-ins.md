---
title: UI プラグインからドライバー設定にアクセスする
description: UI プラグインからドライバー設定にアクセスする
ms.assetid: 898e1cfb-851b-403e-a88b-d38c505c1390
keywords:
- ドライバーの設定へのアクセス、ユーザー インターフェイスにプラグイン WDK 印刷
- UI プラグイン WDK、印刷ドライバーの設定にアクセスします。
- WDK 印刷プラグインのステータス情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb898333baf1d788ba21a0a60a16bd38b6c6a8eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570549"
---
# <a name="accessing-driver-settings-from-ui-plug-ins"></a>UI プラグインからドライバー設定にアクセスする





プラグインの UI には、プリンターの機能とその他の内部情報の現在の状態を取得できます。 [ **IPrintOemDriverUI::DrvGetDriverSetting** ](https://msdn.microsoft.com/library/windows/hardware/ff553114) COM インターフェイス メソッドは Microsoft のプリンター ドライバーのプリンター インターフェイス DLL 内に実装し、UI プラグインを使用して呼び出すことができます。

さらに、次のメソッドは、ドライバーの情報を変更する UI プラグインを許可します。

[**IPrintOemDriverUI::DrvUpdateUISetting** ](https://msdn.microsoft.com/library/windows/hardware/ff553115) UI をユーザーがドライバーの設定を変更したときに、ドライバーに通知をプラグインできます。

[**IPrintOemDriverUI::DrvUpgradeRegistrySetting** ](https://msdn.microsoft.com/library/windows/hardware/ff553118)古いバージョンのドライバーによって使用されるレジストリ設定を更新できるように、UI のレジストリで、デバイスの設定を変更するプラグインを使用します。

 

 




