---
title: GPD ファイルの概要
description: GPD ファイルの概要
ms.assetid: f29415cf-d8ca-42a2-bbae-2be53e3621a6
keywords:
- 一般的なプリンター説明 WDK Unidrv
- GPD ファイル WDK Unidrv
- Unidrv、GPD ファイル
- GPD GPD ファイルについての WDK Unidrv のファイルします。
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7a0bc4fab91134ad6181dcec2bfca1c9d93a02d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577886"
---
# <a name="introduction-to-gpd-files"></a>GPD ファイルの概要





GPD ファイルの作成に使用[Unidrv ミニドライバー](unidrv-minidrivers.md)します。 Unidrv ミニドライバーは、1 つまたは複数の GPD ファイルに格納できるテキスト ベースの汎用的なプリンター説明 (GPD) で構成されます。

GPD ファイルは、プリンターを記述するのに GPD 言語を使用します。 ファイルが含まれて[GPD ファイル エントリ](gpd-file-entries.md)GPD 言語を使用する、次の種類の情報を提供します。

-   [プリンター属性](printer-attributes.md)プリンター特性を記述します。

-   [プリンター コマンド](printer-commands.md)プリンター操作を制御します。

-   [プリンターの機能](printer-features.md)Unidrv で制御できるプリンターの機能を説明します。

-   [プリンター オプション](printer-options.md)プリンターの機能に割り当てることができる状態を表します。

-   [プリンターのフォントの記述](printer-font-descriptions.md)に関連付けられたハードウェアに常駐し、カートリッジのフォント特性を指定します。

-   [条件付きステートメント](conditional-statements.md)プリンター属性とプリンターの構成間の依存関係を記述します。

GPD 言語では、次の操作を制御する GPD ファイル エントリも定義します。

[ラスターのデータを圧縮します。](compressing-raster-data.md)

[色の形式の処理](handling-color-formats.md)

[ハーフトーン Unidrv で](halftoning-with-unidrv.md)

[インストール可能な機能とオプションの処理](handling-installable-features-and-options.md)

[プリンター メモリの構成を記述します。](describing-printer-memory-configurations.md)

この概要のセクションでは、のディスカッションも含まれています。[ユニットをマスター](master-units.md)、 [、ミニドライバーにファイルを複数 GPD を使用して](using-multiple-gpd-files-in-a-minidriver.md)、および[、ミニドライバーのリソース Dll を使用して](using-resource-dlls-in-a-minidriver.md)します。

 

 




