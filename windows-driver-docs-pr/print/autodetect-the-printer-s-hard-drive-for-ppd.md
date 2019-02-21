---
title: Autodetect、プリンターのハード ドライブ PPD
description: Autodetect、プリンターのハード ドライブ PPD
ms.assetid: 0f2eba5c-1a05-4aaf-8780-266d2339570e
keywords:
- 自動検出プリンター ハード ドライブ WDK プリンターの自動構成
- PPD ファイル WDK 自動構成、ハード ドライブの自動検出しています
- ボックスの自動構成サポートの WDK プリンター、ハード ドライブの自動検出しています
- プリンターのハード ドライブを検出します。
- ハード ドライブの自動検出の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50ddc8db58ea8a5db956970fe4435b8ce4a078c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553301"
---
# <a name="autodetect-the-printers-hard-drive-for-ppd"></a>Autodetect、プリンターのハード ドライブ PPD


PPD ファイルのハード ドライブに関連する機能の GDL ファイルにエントリを追加します。 前の例に示すように、同じ手法を使用して GDL ファイルに対応する機能の構造体を作成して、これを行うことができます。 GDL の次の構成体は、ハード ディスクがインストールされているかどうかを自動的に検出します。

```GDL
*% The GDL parser merges this feature definition with the 
*% corresponding feature construct in the GPD file
*Feature: PrinterHardDisk
{
  *FeatureType: PRINTER_PROPERTY

  *BidiQuery: PrinterHardDisk
  {
     *QueryString: "\Printer.Configuration.HardDisk:Installed"
  }
  *BidiResponse: PrinterHardDisk
  {
     *ResponseType: BIDI_BOOL
     *ResponseData: ENUM_OPTION (PrinterHardDisk)
  }
  *Option: FALSE
  {
     *BidiValue: BOOL(FALSE)
  }
  *Option: TRUE
  {
     *BidiValue: BOOL(TRUE)
  }
}
```

 

 




