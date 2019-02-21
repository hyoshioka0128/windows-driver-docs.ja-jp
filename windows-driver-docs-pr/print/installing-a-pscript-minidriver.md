---
title: Pscript ミニドライバーをインストールします。
description: Pscript ミニドライバーをインストールします。
ms.assetid: 9c48b2b0-c293-4606-bbaa-3fcaca01c300
keywords:
- WDK Pscript、ミニドライバーをインストールします。
- WDK の INF ファイルを印刷する Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccc32feb728606af4095aa4c6908c9249f5508bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558561"
---
# <a name="installing-a-pscript-minidriver"></a>Pscript ミニドライバーをインストールします。





Pscript ミニドライバーのインストールが必要です、[プリンター INF ファイル](printer-inf-files.md)ミニドライバーのファイルを識別します。 プリンターのモデルが Microsoft のプリンター INF ファイルでサポートされていない場合は、ntprint.inf、ベンダーから提供された INF ファイルが必要です。 INF ファイルを参照する必要があります[プリンター INF ファイルのデータ セクション](printer-inf-file-data-sections.md)と[プリンター INF ファイルのインストール セクション](printer-inf-file-install-sections.md)ntprint.inf で定義されています。 ミニドライバー abc100 という名前では、次の INF ファイルのエントリが通常必要です。

```cpp
[Manufacturer]
"ABC Printers"
 
[ABC Printers]
"ABC Printer 100 PS" = ABC100.PPD, ABC_Printer_100_PS
 
[ABC100.PPD]
CopyFiles=@ABC100.ppd       ; PPD file.
DataSection=PSCRIPT_DATA    ; PSCRIPT Data Section
DataFile=ABC100.ppd
Include=NTPRINT.INF         ; Include NTPRINT.INF.
Needs=PSCRIPT.OEM           ; Install PSCRIPT.
```

指定する場合、[プラグインのユーザー インターフェイス](user-interface-plug-ins.md)または[プラグインでレンダリング](rendering-plug-ins.md)、INF ファイル内でこれらのコンポーネントの名前を含める必要があります。 カスタマイズされたコードをインストールする方法の詳細については、次を参照してください。[カスタマイズされたドライバー コンポーネントをインストール](installing-customized-driver-components.md)します。

 

 




