---
title: ドライバーのコード分析
description: ドライバーのコード分析は、C および C++ プログラムで基本的なコーディングエラーを検出するコンパイル時の静的検証ツールです。
ms.assetid: 2F3549EF-B50F-455A-BDC7-1F67782B8DCA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1fcebf33888957cd2926b506bd0449b2c702d82
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769318"
---
# <a name="code-analysis-for-drivers"></a>ドライバーのコード分析


ドライバーのコード分析は、C/C++ プログラムの基本的なコーディング エラーをコンパイル時に検出する静的検証ツールです。(主に) カーネル モード ドライバーのコードからエラーを検出することを目的に特化されたモジュールが備わっています。

**メモ** 以前のバージョンの WDK では、コード分析用のドライバー固有のモジュールは、PREfast for Drivers (PFD) と呼ばれるスタンドアロンツールに含まれていました。 また、PREfast for Drivers は、Microsoft Automated Code Review (OACR) の一部として、WDK ビルド環境に統合されていました。 Windows Driver Kit (WDK) 8 以降では、ドライバー固有の機能は、[コード分析ツールを使用したアプリケーション品質の分析](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/dd264897(v=vs.120))と統合されています。

 

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [ドライバーのコード分析の概要](code-analysis-for-drivers-overview.md)
-   [ドライバーのコード分析を実行する方法](how-to-run-code-analysis-for-drivers.md)
-   [Windows ドライバーの SAL 2 注釈](sal-2-annotations-for-windows-drivers.md)
-   [ドライバーのコード分析の警告](prefast-for-drivers-warnings.md)

 

 





