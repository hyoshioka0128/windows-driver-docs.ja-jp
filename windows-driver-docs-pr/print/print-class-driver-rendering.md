---
title: V4 印刷クラス ドライバー レンダリング
description: レンダリングのために、v4 プリンタードライバーは、印刷クラスドライバーの既存の表示機能を利用できます。
ms.assetid: F8178988-1C11-4B21-B250-6626528E0AE5
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 457defe22d76824b729e6003657380420af9a2f8
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652942"
---
# <a name="v4-print-class-driver-rendering"></a>V4 印刷クラス ドライバー レンダリング


レンダリングのために、v4 プリンタードライバーは、印刷クラスドライバーの既存の表示機能を利用できます。

印刷クラスドライバーの既存の表示機能を利用するために、v4 プリンタードライバーは**Requiredclass** v4 manifest ディレクティブを使用できます。 **Requiredclass**ディレクティブを使用すると、ドライバーは、デバイスのドライバー/フレンドリ名と GUID をキーとして使用して、指定されたクラスドライバーのすべてのファイルをインクルードします。 これは、印刷クラスドライバーをモデル固有のプリンタードライバーにリンクするためのメカニズムです。

たとえば、 *PCL5e*という名前の印刷クラスのドライバーを持つ Fabrikam という会社は、次のサンプルの印刷ドライバーマニフェストを使用して、印刷クラスドライバーをプリンタードライバーにリンクできます。

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
PrinterExtensionUrl="https://www.fabrikam.com/download.asp?uiapp=120"

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
> **Requiredclass**ディレクティブは、クラスドライバーでは使用できません。 **Requiredclass**を使用する場合は、リンク先のプリンタードライバーと印刷クラスドライバーの間でファイル名の競合を回避する必要があります。 類似した名前のファイルは相互に上書きされませんが、トラブルシューティング中に、クラスドライバーパッケージファイルと v4 プリンタードライバーのファイルを区別することが困難な場合があります。

 
V4 プリンタードライバーのマニフェストディレクティブの詳細については、「 [V4 ドライバーマニフェスト](v4-driver-manifest.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

[V4 ドライバーマニフェスト](v4-driver-manifest.md)  



