---
title: エラー ソース管理
description: エラー ソース管理
ms.assetid: f73d9006-a7e7-4a0d-9654-004f53286743
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、エラーソース管理
- WHEA WDK、エラーソース管理
- ハードウェアエラー WDK WHEA、エラーソース管理
- エラー WDK WHEA、エラーソース管理
- プラットフォーム固有のハードウェアエラードライバープラグイン WDK WHEA、エラーソース管理
- PSHED プラグイン WDK WHEA、エラーソース管理
- エラーソース管理 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d54ea2a58150d827086f50df2e9fafabcf15cd64
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844409"
---
# <a name="error-source-control"></a>エラー ソース管理


Windows カーネルがハードウェアプラットフォームによって実装されている各エラーソースを制御できるようにする、オペレーティングシステムへのインターフェイスが公開されています。 エラーソース管理操作には、次のものがあります。

-   エラーソースを有効または無効にする。

-   エラーソースに関連付けられているマスクビットを設定またはクリアします。 これらのマスクビットは、エラーソースの特定の動作を有効または無効にします。

-   エラーソースに関連付けられている重大度ビットを設定します。 これらの重要度のビットは、特定のハードウェアエラーがオペレーティングシステムに報告される重大度レベルを制御します。

-   エラーソースに関連付けられているしきい値パラメーターを設定します。

Windows カーネルは、WHEA 管理アプリケーションからのエラーソース制御要求に応答して、エラーソースを構成するために、を呼び出します。 PSHED 検出された標準エラーソースに対するエラーソース管理操作をサポートします。 [エラーソース検出](error-source-discovery.md)に参加し、pshed サポートされていない追加のエラーソースをオペレーティングシステムに報告する、pshed プラグインが実装されている場合は、エラーをサポートするために、pshed プラグインもエラーソース管理に参加する必要があります。これらの追加のエラーソースに対するソース管理操作。 また、必要に応じて、標準のエラーソースを1つ以上制御する方法をオーバーライドするために、必要に応じてエラーソースコントロールに参加することもできます。

エラーソース管理に参加する PSHED プラグインを実装する方法の詳細については、「[エラーソース管理への参加](participating-in-error-source-control.md)」を参照してください。

ユーザーモード管理アプリケーションは、 [WHEA 管理 API](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)を呼び出すことによって、エラーソースを制御します。 WHEA 管理アプリケーションを実装する方法の詳細については、「 [Whea 管理アプリケーション](whea-management-applications.md)」を参照してください。

 

 




