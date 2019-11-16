---
title: ファイルシステムレガシフィルタードライバーについて
description: ファイルシステムレガシフィルタードライバーについて
ms.assetid: 8de28cd6-40be-48db-a839-335a85e48fc4
keywords:
- レガシフィルタードライバー WDK ファイルシステム、レガシファイルシステムフィルタードライバーについて
- ファイルシステムレガシフィルタードライバー WDK、ファイルシステムレガシフィルタードライバーについて
- ファイルシステムレガシフィルタードライバーとは
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5976bdda755453345adfb7fe02855b2d5ccf198e
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2019
ms.locfileid: "74135166"
---
# <a name="about-file-system-legacy-filter-drivers"></a>ファイルシステムレガシフィルタードライバーについて

このセクションの情報は、既存のレガシフィルタードライバーを管理する開発者を対象としています。 レガシファイルシステムフィルターモデルは、[フィルターマネージャーとミニフィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-and-minifilter-driver-architecture)に置き換えられました。

> [!NOTE]
> 最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、フィルターマネージャーをサポートする[ファイルシステムミニフィルタードライバー](filter-manager-and-minifilter-driver-architecture.md)を使用します。 レガシドライバーをミニフィルタードライバーに移植する方法については、「[レガシフィルタードライバーを移植するためのガイドライン](guidelines-for-porting-legacy-filter-drivers.md)」を参照してください。
