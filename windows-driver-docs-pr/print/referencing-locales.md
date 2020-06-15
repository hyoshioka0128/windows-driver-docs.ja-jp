---
title: ロケールを参照する
description: ロケールを参照する
ms.assetid: 63ea5534-b2e1-43aa-b45b-e4fe8bb69f49
keywords:
- Unidrv、参照元ロケール
- GPD ファイル WDK Unidrv、参照ロケール
- 参照 (ロケールを)
- WDK Unidrv を参照するロケール
- Unidrv WDK 印刷
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: d995b24d21a53624bfb94344384ad5e1146cfdff
ms.sourcegitcommit: 8a3cb2a87ce9751059bca8145a55b8cc39c34de9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2020
ms.locfileid: "84756170"
---
# <a name="referencing-locales"></a>参照 (ロケールを)

## <a name="using-gpd-files"></a>GPD ファイルの使用

GPD ファイルは、システムのロケールを参照できます。 通常、ロケール識別子は Switch ステートメント内で使用され \* ます。この場合、既定の用紙サイズやリソース dll などのパラメーターをロケール固有の方法で指定できます。

ロケール情報を参照するには、GPD ファイルに、 \* 次のように Windows Driver Kit (WDK) を使用してに含まれる GPD ファイルを含む Include ステートメントが含まれている必要があります。

```cpp
*Include: locale.gpd
```

この GPD ファイルは、"Locale" という名前の機能を定義し、多くのロケールのオプションを定義します。 (定義されているロケールを確認するには、ファイルを参照してください)。これらのロケールオプションの使用例を次に示します。 この例では、ロケールの既定の用紙サイズを基にしています。

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

実行時に、Unidrv は**GetSystemDefaultLCID** (Microsoft Windows SDK のドキュメントで説明されています) を呼び出して、システムの既定のロケールを決定します。 プリンターがインストールされると、GPD パーサーはプリンターの GPD ファイルを読み取り、 \* 既定のロケールに関連付けられている Case ステートメント内の情報を使用します。 (プリンターのインストール後にシステムのロケールが変更された場合、ロケールベースのオプションは変更されないことに注意してください)。

ロケールに基づいてリソース DLL を選択するもう1つの例を次に示します。 リソース DLL には、表示文字列など、ロケール固有のリソースを含めることができます。

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

## <a name="setting-default-paper-size-by-locale"></a>ロケールによる既定の用紙サイズの設定

ユーザーの地理的な場所に基づいて、既定の用紙サイズ (メトリックまたは非メトリック) をドライバーで割り当てることができます。

次のアルゴリズムでは、既定のシステムロケールを取得し、国/地域コードを使用して、システムロケールが、通常はメトリックまたは非メトリックの用紙サイズを使用する国を表しているかどうかを判断します。 この情報を使用すると、ドライバーは既定の用紙サイズを適切に設定できます。たとえば、メートル法システムを使用する国の場合は A4、そうでない場合はレターサイズなどです。

1. 既定のシステムロケールを取得するには、 [GetLocaleInfo](https://docs.microsoft.com/previous-versions//ms776270(v=vs.85))関数を使用します。 \_ \_ 2 番目のパラメーターの lctype に対して、最初のパラメーター、*ロケール*、およびロケールの icountry にロケールシステムの既定値を使用し \_ ます。 *LCType*

1. **GetLocaleInfo**から取得した既定のシステムロケールを使用して、メトリックまたは非メトリック用紙サイズを決定します。
    - 既定のシステムロケールがの場合、非メトリック:

        - CTRY \_ 米国 \_ 、または

        - CTRY \_ カナダ、または

        - 50以上で、CTRY ブラジルではなく60未満。 \_ または

        - 500以上、600より小さい値

    - それ以外の場合はメトリック。
