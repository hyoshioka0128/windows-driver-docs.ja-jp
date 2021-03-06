---
title: エラー ソース管理
description: エラー ソース管理
ms.assetid: f73d9006-a7e7-4a0d-9654-004f53286743
keywords:
- Windows ハードウェア アーキテクチャ WDK のエラー、エラーのソース管理
- WHEA WDK、エラーのソース管理
- ハードウェア エラー WDK WHEA、エラーのソース管理
- WDK WHEA、エラーのソース管理のエラー
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、エラーのソース管理
- PSHED プラグイン WDK WHEA、エラーのソース管理
- エラー ソース制御 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18f73c9824a9ace3ae1e395cfb87a80615f64010
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386482"
---
# <a name="error-source-control"></a>エラー ソース管理


PSHED では、各ハードウェア プラットフォームで実装されているエラーのソースを制御する Windows カーネルは、オペレーティング システムへのインターフェイスを公開します。 エラーのソース管理操作を以下に示します。

-   有効にするか、エラーのソースを無効にします。

-   設定またはオフにすると、エラーのソースに関連付けられたマスク ビット。 このマスクのビットは、有効またはエラーの発生元の特定の動作を無効にします。

-   エラーのソースと関連付けられている重要度ビットを設定します。 これらの重要度のビットは、オペレーティング システムに特定のハードウェア エラーが報告される重大度レベルを制御します。

-   エラーのソースと関連付けられているしきい値パラメーターを設定します。

Windows カーネルへの呼び出し、PSHED に WHEA 管理アプリケーションによってエラー ソース制御要求に応答、エラーの発生元を構成します。 PSHED、PSHED を検出すると、標準エラー ソースのエラーのソース管理操作をサポートしています。 参加しているプラグイン PSHED が実装されている場合[エラー ソースの検出](error-source-discovery.md)とレポートのプラグインの PSHED、PSHED をサポートしていないオペレーティング システムに追加のエラーのソースは、エラーの発生元にも参加する必要がありますこれらの追加のエラーのソースのエラーのソース管理操作をサポートするコントロール。 プラグイン PSHED は、標準エラー ソースの 1 つ以上の PSHED を制御する方法をオーバーライドするエラーのソース管理にも参加できます。

エラーのソース管理に参加している PSHED プラグインを実装する方法の詳細については、次を参照してください。[エラーのソース管理に参加している](participating-in-error-source-control.md)します。

ユーザー モードの管理アプリケーションを呼び出してエラーのソースを制御する、 [WHEA 管理 API](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)します。 WHEA 管理アプリケーションを実装する方法の詳細については、次を参照してください。 [WHEA 管理アプリケーション](whea-management-applications.md)します。

 

 




