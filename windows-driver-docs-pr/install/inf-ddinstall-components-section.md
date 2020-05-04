---
title: INF DDInstall.Components セクション
description: DDInstall. Components セクションには、ドライバーパッケージの INF ファイルで追加の INF ライター定義セクションを参照する1つ以上の INF AddComponent ディレクティブが含まれています。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26b6169180d49a7d1a43d0eedacbe79a54758c1d
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223258"
---
# <a name="inf-ddinstallcomponents-section"></a>INF DDInstall.Components セクション

この省略可能なセクションには、ドライバーパッケージ INF ファイルで追加の INF ライター定義セクションを参照する1つ以上の[**Inf AddComponent ディレクティブ**](inf-addcomponent-directive.md)が含まれています。  このセクションは、Windows 10 バージョン1703以降でサポートされています。

```inf
[install-section-name.Components] |
[install-section-name.nt.Components] |
[install-section-name.ntx86.Components] |
[install-section-name.ntia64.Components] |
[install-section-name.ntamd64.Components] |
[install-section-name.ntarm.Components] |
[install-section-name.ntarm64.Components] |
 
AddComponent=ComponentName,[flags],component-install-section
```

*Ddinstall*を提供できます。ドライバーパッケージと任意の数のソフトウェアコンポーネントの間にシンボリックリレーションシップを作成するための1つ以上の**Addcomponent**ディレクティブを含む**Components**セクション。

## <a name="entries"></a>エントリ

**Addcomponent**=*ComponentName、[flags]、component-install-section*

このディレクティブは、この*Ddinstall*セクションで取り上げられているデバイスのドライバーについて、inf ファイル内の他の場所にある inf ライターで定義されたコンポーネントを参照します。  詳細については、「 [**INF AddComponent ディレクティブ**](inf-addcomponent-directive.md)」を参照してください。

## <a name="remarks"></a>解説

*Ddinstall*。**コンポーネント**のセクションには、関連する*ddinstall*セクションと同じプラットフォームとオペレーティングシステムの装飾が必要です。  たとえば、 *「」* と指定します。**ntx86**セクションには、対応する*インストールセクション名*があります。**ntx86**セクション。

指定された*Ddinstall*セクションは、INF ファイルの "製造元別*モデル*" セクションのデバイス/モデル固有のエントリで参照されている必要があります。  正式な構文のステートメントに示されている*インストールセクション名*の大文字と小文字を区別しない拡張機能は、このような*ddinstall*に挿入できます。クロスプラットフォームの INF ファイルの**コンポーネント**セクション名。

システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

## <a name="examples"></a>例

```inf
[ContosoGrfx.NT.Components]
AddComponent = ContosoControlPanel,,Component_Inst

[Component_Inst]
ComponentIDs = VID0001&PID0001&SID0001
DisplayName = %ContosoControlPanelDisplayName%
```

## <a name="see-also"></a>関連項目

[コンポーネント INF ファイルの使用](using-a-component-inf-file.md)

[INF AddComponent ディレクティブ](inf-addcomponent-directive.md)
