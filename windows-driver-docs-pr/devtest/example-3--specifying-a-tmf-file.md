---
title: 例 3 TMF ファイルを指定します。
description: 例 3 TMF ファイルを指定します。
ms.assetid: 202304f0-7f8e-4ad1-b10c-185c33db1498
keywords:
- Tracefmt WDK、TMF ファイル
- TMF ファイル WDK、例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d83a2a1899393f503f6efddd514de426823471f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531513"
---
# <a name="example-3-specifying-a-tmf-file"></a>例 3: TMF ファイルを指定します。

この例では、トレース メッセージを書式設定に使用される TMF ファイルを指定する方法を示します。

-   使用して、 **- tmf**パラメーター。

    次のコマンドを使用して、 **- tmf** TMF ファイルのパスとファイル名を指定するパラメーター。 パスは、他の TMF パスの指定をオーバーライドします。

    ```
    tracefmt mytrace.etl -tmf c:\tracing\37753236-c81f-505e-d40a-128d3bb2b5ff.tmf
    ```

    Tracefmt では、指定した TMF ファイルを使用して、mytrace.etl ファイルにトレース メッセージの書式を設定します。

-   使用して、 **-p**パラメーター。

    次のコマンドを使用して、 **-p** TMF ファイルが配置されているディレクトリを指定するパラメーター。 Tracefmt では、コントロールの正しい TMF ファイルを検索する TMF ファイル名を持つトレース プロバイダーの GUID と一致します。 これにより、コピーまたは煩雑 GUID ファイル名を入力することから、ユーザーが保存されます。

    ```
    tracefmt mytrace.etl -p c:\tracing
    ```

    Tracefmt では、指定した TMF ファイルを使用して、mytrace.etl ファイルにトレース メッセージの書式を設定します。

-   % のトレースを使用して\_形式\_検索\_パス % です。

    このシリーズの最初のコマンドは、トレース % の値を設定する\_形式\_検索\_%path% 環境変数をここでは、ディレクトリ場所に c:\\トレースします。

    それに続く Tracefmt コマンドで、 **- tmf**と **-p**パラメーターは省略されています。

    ```
    set TRACE_FORMAT_SEARCH_PATH=c:\tracing
    tracefmt mytrace.etl
    ```

    Tracefmt が c: ドライブを検索 Tracefmt コマンドでは、パスでも、ディレクトリが指定されたが\\TMF ファイル、および、使用 mytrace.etl ファイルにメッセージがトレースを書式設定するコンテンツのディレクトリをトレースします。

これらのメソッドのいずれかで指定された TMF ファイルが行う手順については、トレース メッセージの書式設定に含めない場合[traceview で](traceview.md)「の書式情報が見つかりません」エラー メッセージと出力ファイルにメッセージを書き込みます。 次に、例を示します。

```text
Unknown( 10): GUID=37753236-c81f-505e-d40a-128d3bb2b5ff (No Format Information found).
Unknown( 11): GUID=37753236-c81f-505e-d40a-128d3bb2b5ff (No Format Information found).
Unknown( 11): GUID=37753236-c81f-505e-d40a-128d3bb2b5ff (No Format Information found).
...
```
