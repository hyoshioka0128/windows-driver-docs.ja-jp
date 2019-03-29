---
title: ロケールを参照する
description: ロケールを参照する
ms.assetid: 63ea5534-b2e1-43aa-b45b-e4fe8bb69f49
keywords:
- Unidrv、ロケールを参照します。
- GPD ファイル WDK Unidrv、ロケールを参照します。
- ロケールを参照します。
- ロケールの WDK Unidrv を参照します。
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a47fe10eb8df01764acd99b04967442bc3ee7e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578181"
---
# <a name="referencing-locales"></a>ロケールを参照する





### <a name="using-gpd-files"></a>GPD ファイルを使用します。

GPD ファイルには、システムのロケールを参照できます。 内でロケール識別子を使用する通常、 \*Switch ステートメント、ロケール固有の方法で既定の用紙サイズとリソース Dll などのパラメーターを指定できます。

ロケール情報を参照する GPD ファイルを含める必要があります、\*ファイル locale.gpd を含むステートメントを含める (Windows ドライバー キットに付属する\[WDK\]) 次のように。

```cpp
*Include: locale.gpd
```

この GPD ファイルは、「ロケール」と呼ばれる機能を定義し、ロケールの多くのオプションを定義します。 (定義されているロケールを表示するファイルを参照してください)。これらのロケール オプションの使用例を次に示します。 例では、ロケールに既定の用紙サイズを行います。

```cpp
*Feature: PaperSize
{
...
    Option: A4
    {
    }
    ...
*switch: Locale
{
    *case: English_United_States
    {
        *DefaultOption: Letter
    }
    *case: English_United_Kingdom
    {
        *DefaultOption: A4
    }
    *default:
    {
        *DefaultOption: Letter
    }
} *% End of switch
} *% End of Feature: PaperSize
```

Unidrv、実行時に呼び出すことによって、システムの既定のロケールを決定します**GetSystemDefaultLCID** (Microsoft Windows SDK のドキュメントで説明)。 GPD パーサーがプリンターの GPD ファイルを読み取るし、内の情報を使用してプリンターがインストールされている場合、 \*Case ステートメントに関連付けられた既定のロケール。 (プリンターをインストールした後に、システムのロケールが変更された場合は、ロケール ベースのオプションを変更しないことに注意してください)。

次のロケールに基づいて、DLL のリソースを選択します。 別の例に示します。 リソース DLL は、文字列の表示など、ロケールに固有のリソースを含めることができます。

```cpp
*switch: Locale
{
    *case: English_United_States
    {
        *ResourceDLL: english.dll
    }
    *case: German_Standard
    {
        *ResourceDLL: german.dll
    }
    *default:
    {
        *ResourceDLL: english.dll
    }
}
```

### <a name="setting-default-paper-size-by-locale"></a>ロケールによって既定の用紙サイズを設定します。

ユーザーの地理的な場所を基に、ドライバーの割り当て、既定の用紙サイズ、メトリックまたはメトリック以外の場合のいずれかにすることがあります。

次のアルゴリズムでは、既定のシステム ロケールを取得し、国/地域コードを使用して、システムのロケールが通常はメートル法またはメートル単位以外の用紙サイズを使用する国を表すかどうかを判断します。 この情報により、ドライバー、既定の用紙サイズを適切に設定、メトリック システムを使用する国の A4 やレター サイズのない国など。

1.  使用して、 [GetLocaleInfo](https://go.microsoft.com/fwlink/p/?linkid=52069) (Microsoft Windows SDK のドキュメントで定義された) 関数を既定のシステム ロケールを取得します。 ロケールを使用して、\_システム\_最初のパラメーターの既定の*ロケール*、およびロケール\_ICOUNTRY 2 番目のパラメーターの*LCType*します。

2.  取得した既定のシステム ロケールを使用して、 **GetLocaleInfo**メトリックまたはメトリック以外の用紙サイズを決定します。
    -   非メトリックの既定のシステム ロケールの場合:
        -   か\_UNITED\_状態、または
        -   か\_カナダ、または
        -   50 が 60 未満に以上ないかと\_ブラジル、または
        -   500 が 600 未満に以上
    -   メトリックがそれ以外の場合。

 

 




