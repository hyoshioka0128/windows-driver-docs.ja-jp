---
title: INF DDInstall.Software セクション
description: DDInstall.Software セクションには、ソフトウェア コンポーネントの INF ファイルに追加の INF ライター定義セクションを参照する 1 つまたは複数の INF AddSoftware ディレクティブが含まれています。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 834120ca5ae4fc2c96f1e0f7ea0d30ffafe36340
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559118"
---
# <a name="inf-ddinstallsoftware-section"></a>INF DDInstall.Software セクション

各ごとのモデル*DDInstall*.**ソフトウェア**セクションは、1 つ以上含まれています。 [ **INF AddSoftware ディレクティブ**](inf-addsoftware-directive.md) INF ライター定義の追加のセクションでは、ソフトウェア コンポーネントの INF ファイルを参照します。  このセクションには、Windows 10 バージョン 1703 以降はサポートされています。

```ini
[install-section-name.Software] |
[install-section-name.nt.Software] |
[install-section-name.ntx86.Software] |
[install-section-name.ntia64.Software] |
[install-section-name.ntamd64.Software] |
[install-section-name.ntarm.Software] |
[install-section-name.ntarm64.Software]
 
AddSoftware=SoftwareName,[flags],software-install-section
```

行うことができます、 *DDInstall*.**ソフトウェア**に少なくとも 1 つのセクション[AddSoftware ディレクティブ](inf-addsoftware-directive.md)ソフトウェア コンポーネントからソフトウェアをインストールします。

ソフトウェアのインストールは、非対話型である必要があります。

## <a name="entries"></a>エントリ

**AddSoftware**=*SoftwareName,[flags],software-install-section*

このディレクティブは、INF ライターの定義を参照*ソフトウェアのインストール-セクション*ソフトウェア コンポーネントの INF ファイルに別の場所。  詳細については、次を参照してください。 [ **INF AddSoftware ディレクティブ**](inf-addsoftware-directive.md)します。

## <a name="remarks"></a>注釈

*DDInstall*.**ソフトウェア**のセクションでは、それに関連として同じプラットフォームとオペレーティング システムの装飾が必要*DDInstall*セクション。  たとえば、*インストール セクション名*.**ntx86**セクションが、対応する、*インストール セクション名*.**ntx86 します。ソフトウェア**セクション。
    
指定した*DDInstall* - 製造元でデバイス/モデルに固有のエントリでは、セクションを参照する必要があります*モデル*INF ファイルのセクション。 大文字の拡張機能を*インストール セクション名*に示すように正式な構文でステートメントを挿入できる、 <em>DDInstall</em>**します。ソフトウェア**クロスプラット フォーム対応の INF ファイルでセクション名。

詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

## <a name="examples"></a>例

```ini
[ContosoCtrlPnl.NT.Software]
AddSoftware = ContosoGrfx1CtrlPnl,, Software_Inst

[Software_Inst]
SoftwareType = 1
SoftwareBinary =  %13%\ContosoCtrlPnl.exe
SoftwareArguments = <<DeviceInstanceID>>
SoftwareVersion = 1.0.0.0
```

## <a name="see-also"></a>関連項目

[コンポーネントの INF ファイルを使用して](using-a-component-inf-file.md)します。

[INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)
