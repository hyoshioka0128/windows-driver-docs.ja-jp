---
title: UI プラグインからドライバー設定にアクセスする
description: UI プラグインからドライバー設定にアクセスする
ms.assetid: 898e1cfb-851b-403e-a88b-d38c505c1390
keywords:
- ユーザーインターフェイスプラグイン WDK 印刷、ドライバー設定へのアクセス
- UI プラグイン WDK 印刷、ドライバー設定へのアクセス
- 状態情報 WDK 印刷プラグイン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b422d1d6773616c2f07e765eb9496628fca0f3b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844615"
---
# <a name="accessing-driver-settings-from-ui-plug-ins"></a>UI プラグインからドライバー設定にアクセスする





UI プラグインは、プリンターの機能とその他の内部情報の現在の状態を取得できます。 [**Iprintoemdriverui::D rvgetdriversetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvgetdriversetting) COM インターフェイスメソッドは、Microsoft のプリンタードライバーのプリンターインターフェイス DLL 内に実装されており、UI プラグインによって呼び出すことができます。

さらに、次のメソッドを使用すると、UI プラグインでドライバー情報を変更できます。

[**Iprintoemdriverui::D rvupdateuisetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting)を使用すると、ユーザーがドライバーの設定を変更したときに、UI プラグインからドライバーに通知できます。

[**Iprintoemdriverui::D rvupgraderegistrysetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupgraderegistrysetting)を使用すると、以前のバージョンのドライバーで使用されているレジストリ設定を更新できるように、ui プラグインでレジストリのデバイス設定を変更できます。

 

 




