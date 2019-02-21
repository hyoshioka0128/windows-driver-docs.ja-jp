---
title: INF ドライバーのバージョンのエントリ
description: INF ドライバーのバージョンのエントリ
ms.assetid: 092cd9ed-8988-4ffd-9958-1267f3c52819
keywords:
- バージョン番号の WDK オーディオ
- INF ファイル WDK オーディオ
- オーディオのミニポート ドライバー WDK、バージョン番号
- ミニポート ドライバー WDK オーディオ、バージョン番号
- オーディオ ドライバー WDK、バージョン番号
- ドライバー バージョン番号の WDK オーディオ
- INF DriverVer Directive
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545ce33436a4870432329a2c2394cc2197bab446
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553144"
---
# <a name="inf-driver-version-entry"></a>INF ドライバーのバージョンのエントリ


## <span id="inf_driver_version_entry"></span><span id="INF_DRIVER_VERSION_ENTRY"></span>


ドライバー パッケージ内の INF ファイルには、INF によってインストールされているドライバーのドライバー バージョン情報を指定します。 ファイルにバージョン情報とは異なり、全体としてドライバー パッケージを識別する、[内部および外部のバージョン番号](internal-and-external-version-numbers.md)パッケージ内の個々 のドライバー ファイル。

ファイル内の各ドライバーの日付とバージョン番号を指定します、 [ **INF DriverVer ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547394)次の形式。

**DriverVer**= *mm* / *dd* / *yyyy*\[、*x*.*y*.*v*.*z*\]

日付パラメーター *mm*/*dd*/*yyyy* 2 桁の月のコードから成る*mm*2 桁の日コード*dd*、および 4 桁の年コード*yyyy*します。 このパラメーターは、ドライバー パッケージの日付を指定し、INF ファイルを含むのすべてのドライバー ファイルに適用されます。 ハイフン (-) は、スラッシュ (/) の代わりに日付フィールドの区切り記号として使用できます。 オペレーティング システムの使用、 **DriverVer**ドライバーの 2 つのバージョンを選択するときに、ドライバーのバージョンの比較を実行する日付。 この日付にも表示されます、**ドライバーの日付**デバイス マネージャーによって表示される値。

省略可能なバージョン番号*x*.*y*.*v*.*z* 、表示目的でのみ使用が角かっこ、上に表示される (たとえば、**ドライバーのバージョン**デバイス マネージャーによって表示される番号)。 オペレーティング システムでは、ドライバーの選択のこの値を使用しません。 ドライバー ファイルをコンパイルするときに確認で指定されている場合は、内部バージョン番号、 *FILEVERSION*ドライバーのリソース ファイルと一致するパラメーター、 **DriverVer** INF でバージョン番号ファイルです。

オペレーティング システムは、ドライバーを検索する場合よりも新しいと、ドライバーが選択**DriverVer**ドライバーより前の日付の日付。 INF ファイルを持たない場合**DriverVer**エントリ、または署名なし、オペレーティング システムは 0000/00/00 の既定の日付は適用されます。

Windows 2000、Windows XP でし、後でドライバー パッケージの INF ファイルを指定する必要があります、 **DriverVer**ディレクティブ。

 

 




