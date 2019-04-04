---
title: Unidrv ミニドライバーをインストールします。
description: Unidrv ミニドライバーをインストールします。
ms.assetid: 0efead8f-c413-4ec1-b940-89b57f95345e
keywords:
- Unidrv、ミニドライバー
- ミニドライバー WDK Unidrv
- WDK の INF ファイルを印刷する Unidrv ミニドライバー
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bc374d3c9082802b31ff698b0afa557aac87c4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529674"
---
# <a name="installing-a-unidrv-minidriver"></a>Unidrv ミニドライバーをインストールします。





Unidrv ミニドライバーのインストールが必要です、[プリンター INF ファイル](printer-inf-files.md)ミニドライバーのファイルを識別します。 プリンターのモデルが Microsoft のプリンター INF ファイルでサポートされていない場合は、ntprint.inf、ベンダーから提供された INF ファイルが必要です。 INF ファイルを参照する必要があります[プリンター INF ファイルのデータ セクション](printer-inf-file-data-sections.md)と[プリンター INF ファイルのインストール セクション](printer-inf-file-install-sections.md)ntprint.inf で定義されています。 ミニドライバー abc100 という名前では、次の INF ファイルのエントリは通常必要となる、プリンターは、双方向は、TrueType フォントの置き換えをサポートし、1 つのリソース DLL を使用する場合。

```cpp
[Manufacturer]
"ABC Printers"
 
[ABC Printers]
"ABC Printer 100" = ABC100.GPD, ABC_Printer_100
 
[ABC100.GPD]
CopyFiles=@ABCres.dll,@ABC100.gpd  ;Resource DLL and GPD file
DataSection=UNIDRV_BIDI_DATA       ;Unidrv Data Section
DataFile=ABC100.gpd
Include=NTPRINT.INF                ;Include NTPRINT.INF.
Needs=TTFSUB.OEM,UNIDRV_BIDI.OEM   ;Install TrueType subs, Unidrv,
  ;    and PJL language monitor.
```

指定する場合、[プラグインのユーザー インターフェイス](user-interface-plug-ins.md)または[プラグインでレンダリング](rendering-plug-ins.md)、INF ファイル内でこれらのコンポーネントの名前を含める必要があります。 カスタマイズされたコードをインストールする方法の詳細については、[カスタマイズされたドライバー コンポーネントをインストール](installing-customized-driver-components.md)を参照してください。

 

 




