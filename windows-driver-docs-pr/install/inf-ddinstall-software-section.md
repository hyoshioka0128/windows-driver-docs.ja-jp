---
title: INF DDInstall.Software セクション
description: DDInstall. Software セクションには、ソフトウェアコンポーネントの INF ファイルで追加の INF ライター定義セクションを参照する1つ以上の INF AddSoftware ディレクティブが含まれています。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a942b1f394261f106a63363c8bb3da61b1046610
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223222"
---
# <a name="inf-ddinstallsoftware-section"></a>INF DDInstall.Software セクション

各モデルの*Ddinstall がインストール*します。**Software**セクションには、ソフトウェアコンポーネントの inf ファイルで追加の inf ライター定義セクションを参照する1つ以上の[**inf addsoftware ディレクティブ**](inf-addsoftware-directive.md)が含まれています。  このセクションは、Windows 10 バージョン1703以降でサポートされています。

```inf
[install-section-name.Software] |
[install-section-name.nt.Software] |
[install-section-name.ntx86.Software] |
[install-section-name.ntia64.Software] |
[install-section-name.ntamd64.Software] |
[install-section-name.ntarm.Software] |
[install-section-name.ntarm64.Software]
 
AddSoftware=SoftwareName,[flags],software-install-section
```

*Ddinstall*を提供できます。ソフトウェアコンポーネントからソフトウェアをインストールするための、 [Addsoftware ディレクティブ](inf-addsoftware-directive.md)が1つ以上含まれている**ソフトウェア**セクション。

ソフトウェアのインストールは非対話型である必要があります。

## <a name="entries"></a>エントリ

**Addsoftware**=*SoftwareName、[flags]、software-install-section*

このディレクティブは、ソフトウェアコンポーネントの INF ファイルの別の場所にある INF ライターで定義された*ソフトウェアのインストールセクション*を参照します。  詳細については、「 [**INF AddSoftware ディレクティブ**](inf-addsoftware-directive.md)」を参照してください。

## <a name="remarks"></a>解説

*Ddinstall*。**ソフトウェア**セクションには、関連する*ddinstall*セクションと同じプラットフォームとオペレーティングシステムの装飾が必要です。  たとえば、 *「」* と指定します。**ntx86**セクションには、対応する*インストールセクション名*があります。**ntx86。ソフトウェア**セクション。
    
指定された*Ddinstall*セクションは、INF ファイルの "製造元別*モデル*" セクションのデバイス/モデル固有のエントリで参照されている必要があります。 正式な構文のステートメントに示されている*インストールセクション名*の大文字と小文字を区別しない拡張機能は、このような<em>ddinstall</em>に挿入でき**ます。** クロスプラットフォームの INF ファイルのソフトウェアセクション名。

システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

## <a name="examples"></a>例

```inf
[ContosoCtrlPnl.NT.Software]
AddSoftware = ContosoGrfx1CtrlPnl,, Software_Inst

[Software_Inst]
SoftwareType = 1
SoftwareBinary =  %13%\ContosoCtrlPnl.exe
SoftwareArguments = <<DeviceInstanceID>>
SoftwareVersion = 1.0.0.0
```

## <a name="see-also"></a>関連項目

[コンポーネントの INF ファイルを使用](using-a-component-inf-file.md)します。

[INF AddSoftware ディレクティブ](inf-addsoftware-directive.md)
