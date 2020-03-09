---
title: ファイルシステムのサンプルコード
description: ファイルシステムのサンプルコード
ms.assetid: a64d83c6-d4cd-432d-bc1a-a3ff4656527c
keywords:
- ドライバー WDK ファイルシステム
- ファイルシステムドライバー WDK
ms.date: 02/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: f87a87824ae52df1099286ecad430feed482ce81
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910531"
---
# <a name="file-system-sample-code"></a>ファイルシステムのサンプルコード

ほとんどの場合、Windows 用の完全なファイルシステムドライバーを開発する必要はありません。 新しいファイルシステムドライバーを開発する場合は、 [ *fastfat*サンプル](https://docs.microsoft.com/windows-hardware/drivers/samples/file-system-driver-samples)をモデルとして使用できます。 ファイルシステムドライバーをインストールする方法については、「[ファイルシステムドライバー用の INF ファイルの作成](creating-an-inf-file-for-a-file-system-driver.md)」を参照してください。

WDK には、ファイルシステムの開発に関する概念ドキュメントは用意されていません。

Windows でのほとんどのファイルシステム関連の開発では、システムによって提供される[フィルターマネージャー](filter-manager-concepts.md)と対話するファイルシステムフィルター ("ミニフィルター") ドライバーを作成する必要があります。
