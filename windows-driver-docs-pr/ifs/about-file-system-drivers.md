---
title: ファイルシステムドライバーについて
description: ファイルシステムドライバーについて
ms.assetid: a64d83c6-d4cd-432d-bc1a-a3ff4656527c
keywords:
- ドライバー WDK ファイルシステム
- ファイルシステムドライバー WDK
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 46e5ab1dec5eb2a29edfa69a21438d24f8e19b2f
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2019
ms.locfileid: "74135168"
---
# <a name="about-file-system-drivers"></a>ファイルシステムドライバーについて

ほとんどの場合、完全なファイルシステムドライバーを開発する必要はありません。 新しいファイルシステムドライバーを開発する場合は、次の手順を実行します。

- [ *Fastfat*サンプル](https://docs.microsoft.com/windows-hardware/drivers/samples/file-system-driver-samples)は、モデルとして使用するために使用できます。

- ファイルシステムドライバーを作成してインストールする方法については、「[ファイルシステムドライバー用の INF ファイルの作成](creating-an0inf-file-for-a-file-system-driver.md)」を参照してください。

WDK には、ファイルシステムの開発に関する概念ドキュメントは用意されていません。

Windows でのほとんどのファイルシステム関連の開発には、[ファイルシステムミニフィルタードライバー](file-system-minifilter-drivers.md)の作成が含まれます。
