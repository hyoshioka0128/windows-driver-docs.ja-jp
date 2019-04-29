---
title: PPD の Windows Vista の自動構成フロー
description: PPD の Windows Vista の自動構成フロー
ms.assetid: 60675cd3-fe98-4772-aa1b-a73529480d8a
keywords:
- PPD ファイル WDK 自動構成、一連の手順
- ボックスの自動構成サポートの WDK プリンター、一連の手順
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e1cf59884967bd56de4f0af8c3040a26a55eeda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331182"
---
# <a name="autoconfig-flow-in-windows-vista-for-ppd"></a>PPD の Windows Vista の自動構成フロー


自動構成は、次のシーケンスを次に示します。

1.  ポート モニターは、スプーラーに以前ではなく、キャッシュまたは変更されたすべての値を含む通知を送信します。

2.  スプーラは、DrvPrinterEvent を呼び出すことによってポート モニターからの通知に応答します。

3.  プリンター\_イベント\_構成がすべての新しい値を含むドライバーに渡されます。 ドライバーは、属性の値が変更されたことが通知されます。 レジストリが更新されます。

4.  通知が大きすぎる場合は、制限のスキーマ イベントが呼び出されます。

5.  すべての GDL ファイルの拡張機能と、PPD. 内 GDL コンテンツを含む PPD ファイルを解析します。 いずれかの GDL ファイル拡張機能または PPD ファイル全体ですべての GDL コンテンツで囲む必要があります`*Ifdef: GDL_Enabled`と`*Endif: GDL_Enabled`します。

6.  プラグインの IHV が値を取得 **\*MSBidiValue**の現在の文字列値に基づいてこのは **\*QueryString**します。 たとえば、  **\*QueryString**の値\\Printer.Configuration.DuplexUnit:Installed を表す、  **\*BidiValue** BOOL(TRUE) の値。

7.  プラグインの IHV、最新の構成に従って、ドライバーの UI が更新されます。

 

 




