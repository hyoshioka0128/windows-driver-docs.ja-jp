---
title: ドライバーのコード分析
description: コード Analysis for Drivers は、C および C++ プログラムで基本的なコーディング エラーを検出するコンパイル時の静的検証ツールです。
ms.assetid: 2F3549EF-B50F-455A-BDC7-1F67782B8DCA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37d0b2a0df11e04523564c0e633d83482e424fb5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560587"
---
# <a name="code-analysis-for-drivers"></a>ドライバーのコード分析


ドライバーのコード分析は、C/C++ プログラムの基本的なコーディング エラーをコンパイル時に検出する静的検証ツールです。(主に) カーネル モード ドライバーのコードからエラーを検出することを目的に特化されたモジュールが備わっています。

**注**コード分析用のドライバー固有のモジュールでは、以前のバージョンの WDK では、PREfast for Drivers (PFD) と呼ばれるスタンドアロン ツールの一部であった。 また、PREfast for Drivers は、Microsoft Automated Code Review (OACR) の一部として、WDK ビルド環境に統合されていました。 以降では、Windows Driver Kit (WDK) 8 は、ドライバー固有の機能と統合されている、 [Visual Studio でコード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)します。

 

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションでは


-   [ドライバーの概要のコード分析](code-analysis-for-drivers-overview.md)
-   [ドライバーのコード分析を実行する方法](how-to-run-code-analysis-for-drivers.md)
-   [SAL 2 Windows ドライバーの注釈](sal-2-annotations-for-windows-drivers.md)
-   [Code Analysis for Drivers の警告](prefast-for-drivers-warnings.md)

 

 





