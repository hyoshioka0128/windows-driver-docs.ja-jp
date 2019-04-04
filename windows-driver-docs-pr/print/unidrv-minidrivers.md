---
title: Unidrv ミニドライバー
description: Unidrv ミニドライバー
ms.assetid: ebf12f61-6194-4033-92a2-2bbccc40a6fd
keywords:
- Unidrv、ミニドライバー
- ミニドライバー WDK Unidrv
- テキスト ベースのプリンター説明 WDK Unidrv
- WDK Unidrv プリンタの説明
- GPD は、WDK Unidrv、Unidrv 機能をファイルします。
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e2b8963ff529bd5e2e6eff2035db22a9ec36232
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552876"
---
# <a name="unidrv-minidrivers"></a>Unidrv ミニドライバー





Unidrv ミニドライバーは、プリンターの説明が含まれているテキスト ファイルです。 各ミニドライバーは、1 つの製造元から 1 つのプリンターの種類について説明します。 このテキストの説明は汎用的なプリンターの説明 (GPD) と呼ばれ、各ファイルは GPD ファイルと呼ばれます。 各ミニドライバーは、1 つまたは複数の GPD ファイルで構成されます。

GPD ファイルを使用してプリンターを記述する、Unidrv には、次の機能がサポートされています。

-   ジェネリック、standard[プリンターの機能](printer-features.md)ほとんどのプリンターに存在します。

-   Unique、プリンターのプリンターのみを提供する機能をカスタマイズします。

-   インストール可能な[プリンター オプション](printer-options.md)、これのみ選択できるオプションがインストールされている場合。

-   [制約オプション](option-constraints.md)、互換性のないオプションを指定できます。

-   [条件付きステートメント](conditional-statements.md)プリンターのいくつかの特性が他のユーザーに依存していることを指定できます。

-   仕様の[プリンター コマンド](printer-commands.md)の大規模な選択範囲の現在の値を含めることができる[標準的な変数](standard-variables.md)します。 これらの変数に対する算術演算を実行することもできます。

-   標準のヘルプ ファイルを記述するために、Unidrv で提供されるだけでなく、カスタマイズされたヘルプ ファイルは、機能をカスタマイズします。

GPD ファイルを作成する方法の詳細については、[GPD Files の概要](introduction-to-gpd-files.md)を参照してください。

Unidrv ミニドライバーは、1 つ以上の GPD ファイルで構成できます。 詳細については、[複数 GPD ファイルで、ミニドライバーを使用して](using-multiple-gpd-files-in-a-minidriver.md)を参照してください。

プリンターがインストールされている場合、Unidrv の GPD パーサーは、すべてのプリンターの GPD ファイルを読み取ります。 プリンターの一時的なバイナリ ファイルを作成する GPD ファイル内の情報が使用されます。 両方の[Unidrv ユーザー インターフェイス](unidrv-user-interface.md)と[Unidrv レンダラー](unidrv-renderer.md)このバイナリ ファイルを参照します。

通常、ミニドライバーは、フォント、ビットマップ、およびローカライズ可能なテキスト文字列などのリソースを提供する必要があります。 これらのリソースは、リソース DLL に配置されます。 詳細については、[、ミニドライバーのリソース Dll を使用して](using-resource-dlls-in-a-minidriver.md)を参照してください。

 

 




