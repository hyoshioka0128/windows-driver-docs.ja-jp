---
title: INF ドライバー バージョンのエントリ
description: INF ドライバー バージョンのエントリ
ms.assetid: 092cd9ed-8988-4ffd-9958-1267f3c52819
keywords:
- バージョン番号の WDK オーディオ
- INF ファイル WDK オーディオ
- オーディオのミニポート ドライバー WDK、バージョン番号
- ミニポート ドライバー WDK オーディオ、バージョン番号
- オーディオ ドライバー WDK、バージョン番号
- ドライバー バージョン番号の WDK オーディオ
- INF DriverVer ディレクティブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 120261d0e57c1ef5bafea0a641367081e8b43589
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359901"
---
# <a name="inf-driver-version-entry"></a>INF ドライバー バージョンのエントリ


## <span id="inf_driver_version_entry"></span><span id="INF_DRIVER_VERSION_ENTRY"></span>


ドライバー パッケージ内の INF ファイルには、INF によってインストールされているドライバーのドライバー バージョン情報を指定します。 ファイルにバージョン情報とは異なり、全体としてドライバー パッケージを識別する、[内部および外部のバージョン番号](internal-and-external-version-numbers.md)パッケージ内の個々 のドライバー ファイル。

ファイル内の各ドライバーの日付とバージョン番号を指定します、 [ **INF DriverVer ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)次の形式。

**DriverVer**= *mm* / *dd* / *yyyy*\[、*x*.*y*.*v*.*z*\]

日付パラメーター *mm*/*dd*/*yyyy* 2 桁の月のコードから成る*mm*2 桁の日コード*dd*、および 4 桁の年コード*yyyy*します。 このパラメーターは、ドライバー パッケージの日付を指定し、INF ファイルを含むのすべてのドライバー ファイルに適用されます。 ハイフン (-) は、スラッシュ (/) の代わりに日付フィールドの区切り記号として使用できます。 オペレーティング システムの使用、 **DriverVer**ドライバーの 2 つのバージョンを選択するときに、ドライバーのバージョンの比較を実行する日付。 この日付にも表示されます、**ドライバーの日付**デバイス マネージャーによって表示される値。

省略可能なバージョン番号*x*.*y*.*v*.*z* 、表示目的でのみ使用が角かっこ、上に表示される (たとえば、**ドライバーのバージョン**デバイス マネージャーによって表示される番号)。 オペレーティング システムでは、ドライバーの選択のこの値を使用しません。 ドライバー ファイルをコンパイルするときに確認で指定されている場合は、内部バージョン番号、 *FILEVERSION*ドライバーのリソース ファイルと一致するパラメーター、 **DriverVer** INF でバージョン番号ファイルです。

オペレーティング システムは、ドライバーを検索する場合よりも新しいと、ドライバーが選択**DriverVer**ドライバーより前の日付の日付。 INF ファイルを持たない場合**DriverVer**エントリ、または署名なし、オペレーティング システムは 0000/00/00 の既定の日付は適用されます。

Windows 2000、Windows XP でし、後でドライバー パッケージの INF ファイルを指定する必要があります、 **DriverVer**ディレクティブ。

 

 




