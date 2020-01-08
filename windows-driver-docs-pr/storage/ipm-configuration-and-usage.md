---
title: アイドル状態の電源管理の構成と使用状況
description: アイドル状態の電源管理の構成と使用状況
ms.assetid: 95057785-e5b5-40ae-86e4-50bbf0014cef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15eaff4268d8cb30dfe8d827bbce7dfe75092785
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606520"
---
# <a name="idle-power-management-configuration-and-usage"></a>アイドル状態の電源管理の構成と使用状況

既定では、Storport アイドル電源管理 (IPM) は有効になっていません。 これは、デバイスのハードウェアキーの "StorPort" サブキーの "EnableIdlePowerManagement" 値を0以外の値に設定することによって、レジストリで有効にすることができます。 これは、デバイスの INF ファイルを使用するか、レジストリエディターを使用して手動で行うことができます。

次のサンプルテキストは、Storport の IPM 機能を有効にするためにデバイスの INF ファイルに追加する必要があるものを示しています。

```cpp
          [DDInstall.HW]
          ; Enables Storport IPM for this adapter
          HKR, "StorPort", "EnableIdlePowerManagement", 0x00010001, 0x01
```

これは、HKR がサービスキーではなくハードウェアキーを指している INF ファイルの DDInstall. HW セクション内からのみ実行できます。 INF ファイルを変更する方法の詳細については、「[ドライバーのレジストリキーの概要](https://go.microsoft.com/fwlink/p/?linkid=144533)」を参照してください。

次のスクリーンショットに示されている [電源オプション] コントロールパネルアプレットを使用して、システムの電源ポリシーとディスクのアイドル状態のタイムアウト値を構成します。 [**スタート**&gt;**コントロールパネル]** &gt; **[電源オプション]** からアクセスできます。

![ipm 電源オプションを示すスクリーンショット](images/ipm-power-options.png)

コマンドラインツール (*Powercfg*) を使用することもできます。 「 **Powercfg/?」と入力します。** 使用方法については、「」を参照してください。
