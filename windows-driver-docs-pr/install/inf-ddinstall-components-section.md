---
title: INF DDInstall.Components セクション
description: DDInstall.Components セクションには、ドライバー パッケージ INF ファイルに追加の INF ライター定義セクションを参照する 1 つまたは複数の INF AddComponent ディレクティブが含まれています。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7aadabb3e1d97e76e18196290a20eb37a87278f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535582"
---
# <a name="inf-ddinstallcomponents-section"></a>INF DDInstall.Components セクション

このオプションのセクションには、1 つまたは複数が含まれています[ **INF AddComponent ディレクティブ**](inf-addcomponent-directive.md) INF ライター定義の追加のセクションでは、ドライバー パッケージ INF ファイルを参照します。  このセクションには、Windows 10 バージョン 1703 以降はサポートされています。

```ini
[install-section-name.Components] |
[install-section-name.nt.Components] |
[install-section-name.ntx86.Components] |
[install-section-name.ntia64.Components] |
[install-section-name.ntamd64.Components] |
[install-section-name.ntarm.Components] |
[install-section-name.ntarm64.Components] |
 
AddComponent=ComponentName,[flags],component-install-section
```

行うことができます、 *DDInstall*.**コンポーネント**1 つまたは複数のセクション**AddComponent**シンボリック ドライバー パッケージおよびソフトウェア コンポーネントの任意の数の間でリレーションシップを作成するディレクティブ。

## <a name="entries"></a>エントリ

**AddComponent**=*ComponentName を [flags] コンポーネントのインストール-セクション*

このディレクティブは、INF ライター定義コンポーネントのインストール-セクションこの対象となるデバイスのドライバーの INF ファイルで別の場所を参照*DDInstall*セクション。  詳細については、[ **INF AddComponent ディレクティブ**](inf-addcomponent-directive.md)を参照してください。

## <a name="remarks"></a>注釈

*DDInstall*.**コンポーネント**のセクションでは、それに関連として同じプラットフォームとオペレーティング システムの装飾が必要*DDInstall*セクション。  たとえば、*インストール セクション名*.**ntx86**セクションが、対応する、*インストール セクション名*.**ntx86.Components**セクション。

指定した*DDInstall* - 製造元でデバイス/モデルに固有のエントリでは、セクションを参照する必要があります*モデル*INF ファイルのセクション。  大文字の拡張機能を*インストール セクション名*に示すように正式な構文でステートメントを挿入できる、 *DDInstall*.**コンポーネント**クロスプラット フォーム対応の INF ファイルでセクション名。

詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

## <a name="examples"></a>例

```ini
[ContosoGrfx.NT.Components]
AddComponent = ContosoControlPanel,,Component_Inst

[Component_Inst]
ComponentIDs = VID0001&PID0001&SID0001
DisplayName = %ContosoControlPanelDisplayName%
```

## <a name="see-also"></a>関連項目

[コンポーネント INF ファイルの使用](using-a-component-inf-file.md)

[INF AddComponent ディレクティブ](inf-addcomponent-directive.md)
