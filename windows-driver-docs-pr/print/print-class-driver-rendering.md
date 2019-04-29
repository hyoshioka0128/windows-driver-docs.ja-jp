---
title: V4 印刷クラス ドライバー レンダリング
description: レンダリングには、v4 プリンター ドライバーは、印刷クラス ドライバーの既存の表示機能を利用できます。
ms.assetid: F8178988-1C11-4B21-B250-6626528E0AE5
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: b9dd9fa0b4ca6576794281e6e6460b8c0ee9d2f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389479"
---
# <a name="v4-print-class-driver-rendering"></a>V4 印刷クラス ドライバー レンダリング


レンダリングには、v4 プリンター ドライバーは、印刷クラス ドライバーの既存の表示機能を利用できます。

既存のレンダリングの印刷クラス ドライバーの機能を活用する v4 プリンター ドライバーを使用できます、 **RequiredClass** v4 マニフェスト ディレクティブ。 使用して、 **RequiredClass**ディレクティブによりドライバーでキーとして、デバイスとその GUID のドライバー/フレンドリ名を使用して、指定したクラス ドライバーからのすべてのファイルが含まれます。 モデルに固有のプリンター ドライバーの印刷クラス ドライバーをリンクするためのメカニズムです。

たとえば、fabrikam という名前の印刷クラス ドライバーを使用した会社*PCL5e*、自分のプリンター ドライバーの印刷クラス ドライバーをリンクする、次のサンプルの印刷ドライバー マニフェストを使用して。

```Text
[DriverConfig]
DataFile=FAPDL.gpd
RequiredFiles=UNIRES.DLL,STDNAMES.GPD,STDDTYPE.GDL,STDSCHEM.GDL,STDSCHMX.GDL,MSXPSINC.GPD
RequiredClass="Fabrikam PCL5e Class Driver",{9343720D-B67E-4451-B93F-6F721C439771} ; This links the print class driver to this printer driver
ResourceFile=FARC.dll
PropertyBag=FAProperty.dpb
PrinterDriverID={GUID}
DriverCategory=PrintFax.Printer
ConstraintScript=faconst.js
EventFile=faevents.xml
PrinterExtensionUrl="http://www.fabrikam.com/download.asp?uiapp=120"

[BidiFiles]
BidiSPMFile=FABidiSPM.xml
BidiWSDFile=FABidiWSD.xml
BidiUSBFile=FaBidiUSB.xml
BidiUSBJSFile=FABidiUSBJS.js 

[DriverRender]
PageOutputQuality.Draft=MxdcImageType.JPEGHigh
PageOutputQuality.Normal= MxdcImageType.JPEGMedium
PageOutputQuality.High=MxdcImageType.PNG

[PrinterExtensions]
DriverEvent=FAapp.exe,{GUID}
PrintPreferences=FAapp.exe,{GUID2}
```

> [!NOTE]
> **RequiredClass**クラス ドライバーは、ディレクティブを使用できません。 使用すると**RequiredClass**、プリンター ドライバーとリンクしている印刷クラス ドライバーのファイル名の競合を避ける必要があります。 類似した名前のファイルは、相互に上書きされません、クラスのドライバー パッケージ ファイルと、v4 プリンター ドライバーからファイルを区別する、トラブルシューティングの際に難しいあります。

 
V4 プリンター ドライバー マニフェスト ディレクティブの詳細については、次を参照してください。 [V4 ドライバー マニフェスト](v4-driver-manifest.md)します。

## <a name="related-topics"></a>関連トピック

[V4 ドライバー マニフェスト](v4-driver-manifest.md)  



