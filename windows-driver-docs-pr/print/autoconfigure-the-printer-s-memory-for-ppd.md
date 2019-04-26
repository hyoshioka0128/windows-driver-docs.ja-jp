---
title: PPD のプリンターのメモリを自動構成する
description: PPD のプリンターのメモリを自動構成する
ms.assetid: 75df1026-896f-4840-a69d-975f813ca636
keywords:
- メモリの WDK プリンター autoconfig
- PPD ファイル WDK 自動構成、メモリ
- ボックスの自動構成サポート WDK プリンター、メモリ
- autoconfiguring プリンター メモリ WDK
- プリンター メモリの構成の WDK の自動構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52037f4a9f90823f2d9130110a24ac7e584278a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350754"
---
# <a name="autoconfigure-the-printers-memory-for-ppd"></a>PPD のプリンターのメモリを自動構成する


PPD. で指定されたメモリ オプションの GDL にエントリを追加します。 最初のサンプルでは、インストール可能なメモリのオプションに関係する PPD ファイルからの例の抜粋を示します。

```PPD
*% === Installable Options ===========
*OpenGroup: InstallableOptions/Options Installed
 
*OpenUI *InstalledMemory/Memory Configuration: PickOne
*DefaultInstalledMemory: 24Meg
*InstalledMemory 24Meg/Standard 24 MB RAM: ""
*InstalledMemory 56Meg/56 MB Total RAM: ""
*InstalledMemory 72Meg/72 MB Total RAM: ""
*CloseUI: *InstalledMemory
 
*CloseGroup: InstallableOptions
```

"InstalledMemory"PPD を自動構成を有効にする機能、GDL ファイルに次のコード例を追加します。

```GDL
*% This feature definition merges with the definition in the PPD file
*% because both have the same name
*Feature: InstalledMemory
{
  *FeatureType: PRINTER_PROPERTY

  *% *BidiQuery and *BidiResponse constructs must have the same names
  *BidiQuery: InstalledMemory
  {
    *QueryString: "\Printer.Configuration.Memory:Size"
  }
  *BidiResponse: InstalledMemory
  {
    *ResponseType: BIDI_INT
    *ResponseData: ENUM_OPTION (InstalledMemory)
  }
 
  *Option: 24Meg
  { 
    *BidiValue: INT(24576)
  } 
  *Option: 56Meg
  {
    *BidiValue: INT(57344)
  }
  *Option: 72Meg
  {
    *BidiValue: INT(73728)
  }
}
```

 

 




