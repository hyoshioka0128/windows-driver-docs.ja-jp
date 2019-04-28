---
title: GDL 演習ノート
description: GDL 演習ノート
ms.assetid: 39013410-ad8e-4b1a-9db7-2ec541f08989
keywords:
- GDL WDK、例
- WDK GDL の例
- WDK GDL のチュートリアル
- GDL WDK、チュートリアル
- GDL WDK、インデックスのツリー
- パーサー WDK GDL、インデックスのツリー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf8ee1ab3103d736f5b0939db3f9b032ea1f91e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372090"
---
# <a name="gdl-exercise-notes"></a>GDL 演習ノート


次のコード例では、GDL 演習のすべてのパーサーを生成するインデックス ツリーが表示されます。

```cpp
      <:ROOT2>
    *PFeature : InputTray    <:INPUTTRAY_FEATURE>
        *POption : Lower    <:INPUTTRAY_OPTION2>
            *Capacity    <:TRAY_CAPACITY>
            *Command    <:ACOMMAND>
            *Name    <:INPUTTRAY_OPT_NAME>
        *POption : Upper    <:INPUTTRAY_OPTION2>
            *Capacity    <:TRAY_CAPACITY>
            *Command    <:ACOMMAND>
            *Name    <:INPUTTRAY_OPT_NAME>
        *DefaultOption    <:DEFAULT_OPT>
        *Name    <:NAME>
    *PFeature : PaperSize    <:PAPERSIZE_FEATURE>
        *POption : Custom    <:CUST_PAPERSIZE_OPTION>
            *MinSize    <:MIN_SIZE>
            *MaxSize    <:MAX_SIZE>
            *Command    <:ACOMMAND>
            *Name    <:PAPER_SIZE_OPT_NAME>
        *POption : OEMName_Special_size    <:OEM_PAPERSIZE_OPTION>
            *OEM_Info    <:OEM_INFO>
            *PaperSize    <:PAPERDIMENSIONS>
            *Command    <:ACOMMAND>
            *Name    <:PAPER_SIZE_OPT_NAME>
        *POption : A4    <:PREDEFINED_PAPERSIZE_OPTION>
            *PaperSize    <:PAPERDIMENSIONS>
            *Command    <:ACOMMAND>
            *Name    <:PAPER_SIZE_OPT_NAME>
        *POption : Legal    <:PREDEFINED_PAPERSIZE_OPTION>
            *PaperSize    <:PAPERDIMENSIONS>
            *Command    <:ACOMMAND>
            *Name    <:PAPER_SIZE_OPT_NAME>
        *POption : Letter    <:PREDEFINED_PAPERSIZE_OPTION>
            *PaperSize    <:PAPERDIMENSIONS>
            *Command    <:ACOMMAND>
            *Name    <:PAPER_SIZE_OPT_NAME>
        *DefaultOption    <:DEFAULT_OPT>
        *Name    <:NAME>
    *PFeature : random    <:PFEATURE >
        *POption : First    <:GENERIC_OPTION>
            *Command    <:ACOMMAND>
            *Name    <:NAME>
        *DefaultOption    <:DEFAULT_OPT>
        *Name    <:NAME>
```

\*名と\*POption エントリがそれぞれ異なるセマンティクスを持つ複数のテンプレートをマップします。 たとえば、\*名名、INPUTTRAY にマップ\_OPT\_名、または用紙\_サイズ\_OPT\_名。 \*汎用マップ POption\_オプション、定義済み\_PAPERSIZE\_オプション、CUST\_PAPERSIZE\_オプション、OEM\_PAPERSIZE\_オプション、または INPUTTRAY\_OPTION2 します。 テンプレートの構造が正しく定義されている場合、その templatization 規則に従って、パーサーは、最も適切なテンプレートを紹介します。

**注**  スキーマがより詳細ないくつかの基本的なテンプレートと以降の派生バリアントをこれらの演習が確立します。 このプロセスは、現実でのスキーマを進化方法を模倣します。 継承には、以前に定義されたテンプレートを変更することがなく拡張する演習のスキーマが有効になります。 この機能にはマスターのスキーマを拡張するサード パーティができ、また、任意のサードパーティ スキーマの拡張機能を元のマスター スキーマのユーザーとの互換性を維持します。

 

表示される手順の回答は一意ではありません。 たとえば、でした派生したテンプレートの最小\_サイズと最大\_次のように PAPERDIMENSIONS からサイズ。

```cpp
*Template:  MIN_SIZE
{
    *Name: "*MinSize"
    *Inherits: PAPERDIMENSIONS
}
*Template:  MAX_SIZE
{
    *Name: "*MaxSize"
    *Inherits: PAPERDIMENSIONS
}
```

なお、ホワイト ペーパー\_サイズ\_OPT\_名と INPUTTRAY\_OPT\_名テンプレートは、テンプレート名から継承し、再定義も、\*エントリの名前します。

再定義の影響、\*名エントリがこれらの派生テンプレート基本テンプレートを確立する継承ツリーからを非表示にします。

名前を宣言と通常、テンプレート、\*メンバー、この宣言の意味を名前から派生したすべてのテンプレートがも\*メンバー。 ただし、派生テンプレートが再定義\*名前エントリを除外から暗黙\*派生テンプレートのメンバーの一覧。 この除外では、テンプレートの名前になりますがマップされていたデータ エントリなし (たとえば、\*内で名前が表示される、 \*Pfeature) は INPUTTRAY にマップを取得\_OPT\_名 (これが正しくありません)。

ホワイト ペーパーに名前の特殊化が予想される場合\_サイズ\_OPT\_名と INPUTTRAY\_OPT\_スキーマ、スキーマの異なる実装の元のデザイン時に名前になります名前を削除するだけで、\*ジェネリックのメンバー リスト\_オプション。 この変更としても、再定義する必要がない\*名。 設計の調整をさらには名前、ホワイト ペーパーが\_サイズ\_OPT\_名、および INPUTTRAY\_OPT\_名前、そのような状況をより正確に反映されるため、一般的な仮想テンプレートからの継承これらのキーワードの間のリレーションシップです。

 

 




