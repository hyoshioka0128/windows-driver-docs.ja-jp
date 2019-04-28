---
title: プリンター INF ファイル インストール セクション
description: プリンター INF ファイル インストール セクション
ms.assetid: fb544271-1f0f-4bbd-b0a7-88dc89cc8186
keywords:
- WDK の INF ファイルを印刷するインストール セクション
- セクションでは WDK プリンターをインストールします。
- セクションでは WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d7da8881e8ab5afe26ecb3bd5fc1a2416f5b41b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362300"
---
# <a name="printer-inf-file-install-sections"></a>プリンター INF ファイル インストール セクション





Windows NT 4.0 と以前は、ミニドライバーを顧客に提供するベンダーは Microsoft から取得した、適切な Microsoft プリンター ドライバーのコピーを持つ顧客も指定します。

通常、Windows 2000 以降、ベンダーは、ミニドライバーと Microsoft のプリンター ドライバーを配布しないでください。 代わりに、各仕入先は、仕入先のファイルをインストールし、Microsoft のプリンターの INF ファイル、Ntprint.inf で、適切なプリンター ドライバーのコンポーネントがインストールされますが呼び出され、INF ファイルを提供します。

**注**  マイクロソフトは、そのプリンター ドライバーの更新バージョンを定期的にリリースします。更新されたバージョンでのみ使用可能な機能を必要とするミニドライバーは、追加の手順を必要があります。 詳細については、次を参照してください。[更新コア印刷ドライバーを使用して](using-updated-core-print-drivers.md)します。

 

Ntprint.inf、Microsoft のプリンター INF ファイルに含まれる[ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)ベンダー INF ファイルを参照できます。

-   \[PSCRIPT します。OEM\]

    Microsoft Postscript プリンター ドライバー (Pscript) をインストールします。

-   \[UNIDRV します。OEM\]

    Microsoft Universal プリンター ドライバー (Unidrv) をインストールします。

-   \[UNIDRV\_BIDI.OEM\]

    Microsoft ユニバーサル プリンター ドライバーと Pjlmon.dll、インストール、*言語モニター*をプリンター ジョブ言語 (PJL) をサポートし、PJL プリンターの双方向通信を提供します。

-   \[TTFSUB します。OEM\]

    インストール、Windows Driver Kit (WDK) に含まれるされのセットを含む Ttfsub.gpd \*Unidrv でサポートされているプリンターで使用できる共通の TrueType フォント置換の TTFS エントリ。

-   \[sRGBPROFILE.OEM\]

    システムの sRGB カラー プロファイルをインストールします。

-   \[ロケール。OEM\]

    ロケール識別子を含む、Locale.gpd をインストールします。 (を参照してください[ロケールを参照する](referencing-locales.md))。

INF ファイルからこれらのインストール セクションを参照するには、ファイルは、インクルードを使用する必要があり、次の例に示すように、ディレクティブを必要があります。

```cpp
[Manufacturer]
"ABC Printers"
 
[ABC Printers]
"ABC Printer 100ex" = ABC100EX.GPD, ABC_Printer_100ex
 
[ABC100EX.GPD]
CopyFiles=@ABCres.dll,@ABC100EX.gpd
DataSection=UNIDRV_BIDI_DATA      ; Unidrv Bidirectional Data Section
DataFile=ABC100EX.gpd
Include=NTPRINT.INF               ; Include NTPRINT.INF.
Needs=TTFSUB.OEM,UNIDRV_BIDI.OEM  ; Install Unidrv, TrueType subs,
 ;    and PJL language monitor.
```

 

 




