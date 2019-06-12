---
title: IPM の構成と使用方法
description: IPM の構成と使用方法
ms.assetid: 95057785-e5b5-40ae-86e4-50bbf0014cef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3ffeb42fb0ff4439e984281f1d3cb90bb475f59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368753"
---
# <a name="ipm-configuration-and-usage"></a>IPM の構成と使用方法


Storport アイドル状態の電源管理 (IPM) は、既定では無効です。 デバイスのハードウェア キーを 0 以外の値からの"StorPort"サブキーに"EnableIdlePowerManagement"値を設定して、レジストリで有効にできます。 これは、デバイスの INF ファイルを使用して、または手動でレジストリ エディターを使用して実行できます。

次のサンプル テキストは、Storport アイドル状態の電源管理機能を有効にするデバイスの INF ファイルに追加する必要がありますを示しています。

```cpp
          [DDInstall.HW]
          ; Enables Storport IPM for this adapter
          HKR, "StorPort", "EnableIdlePowerManagement", 0x00010001, 0x01
```

これは、ハードウェア キーをサービス キーではなく HKR が指す場所、INF ファイルの DDInstall.HW セクション内からのみ実行できます。 INF ファイルを変更する方法の詳細については、次を参照してください。[ドライバーのレジストリ キーの概要](https://go.microsoft.com/fwlink/p/?linkid=144533)します。

次のスクリーン ショットに示すように、電源オプション コントロール パネル アプレットを使用して、システムの電源ポリシーとディスクのアイドル タイムアウト値を構成します。 アクセス**開始** &gt; **コントロール パネルの**  &gt; **電源オプション**します。

![スクリーン ショット: ipm 電源オプション](images/ipm-power-options.png)

コマンド ライン ツール (*Powercfg.exe*) こともできます。 型**powercfg/でしょうか。** コマンド プロンプトでの使用状況情報。

 

 




