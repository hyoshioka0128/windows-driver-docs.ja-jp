---
title: カメラ ドライバー UI 拡張機能のサンプル
description: カメラ ドライバー UI 拡張機能のサンプル
ms.assetid: 21ddf804-fff5-4cdc-adb5-f85d769ccc1f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e005b5647dafda46e3a782571f1f6c912a514f89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559437"
---
# <a name="camera-driver-ui-extension-sample"></a>カメラ ドライバー UI 拡張機能のサンプル





*拡張*WDK のディレクトリには、WIA デジタル カメラのドライバーのサンプル ユーザー インターフェイス拡張機能が含まれています。

このサンプルでは、WIA ユーザー インターフェイス (UI) の拡張機能を記述する方法を示します。 デバイス プロパティ ダイアログ ボックス (Windows エクスプ ローラーからアクセス可能) にタブを追加し、サンプル カメラ デバイスのアイコンのコンテキスト メニューにコマンドを追加します。 実装を提供することで、WDK からこれらの拡張機能を WIA サンプル カメラに適用されます、 **IShellPropSheetExt**と**IContextMenu** (Microsoft Windows SDK で説明されている COM インターフェイスドキュメント)。

 

 




