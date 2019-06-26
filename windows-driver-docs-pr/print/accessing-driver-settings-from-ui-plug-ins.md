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
ms.openlocfilehash: d996039f271d8acf312cc2532b3d0aa4f2bd8688
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385701"
---
# <a name="accessing-driver-settings-from-ui-plug-ins"></a>UI プラグインからドライバー設定にアクセスする





プラグインの UI には、プリンターの機能とその他の内部情報の現在の状態を取得できます。 [ **IPrintOemDriverUI::DrvGetDriverSetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriverui-drvgetdriversetting) COM インターフェイス メソッドは Microsoft のプリンター ドライバーのプリンター インターフェイス DLL 内に実装し、UI プラグインを使用して呼び出すことができます。

さらに、次のメソッドは、ドライバーの情報を変更する UI プラグインを許可します。

[**IPrintOemDriverUI::DrvUpdateUISetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting) UI をユーザーがドライバーの設定を変更したときに、ドライバーに通知をプラグインできます。

[**IPrintOemDriverUI::DrvUpgradeRegistrySetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriverui-drvupgraderegistrysetting)古いバージョンのドライバーによって使用されるレジストリ設定を更新できるように、UI のレジストリで、デバイスの設定を変更するプラグインを使用します。

 

 




