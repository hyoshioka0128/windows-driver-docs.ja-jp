---
title: 自動検出、プリンターのハード ドライブ GPD
description: 自動検出、プリンターのハード ドライブ GPD
ms.assetid: c3bc415e-fa4d-42d0-9686-3105a588a7ea
keywords:
- 自動検出プリンター ハード ドライブ WDK プリンターの自動構成
- GPD ファイル WDK GDL 拡張機能、ハード ドライブの自動検出しています
- ボックスの自動構成サポートの WDK プリンター、ハード ドライブの自動検出しています
- プリンターのハード ドライブを検出します。
- ハード ドライブの自動検出の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54409b51cd6d1ea1a1aee0a8faf3db8e47d91587
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550030"
---
# <a name="autodetecting-the-printers-hard-drive-for-gpd"></a>自動検出、プリンターのハード ドライブ GPD


GPD ファイルのハード ドライブに関連する機能の GDL ファイルにエントリを追加します。 たとえば、ハード ドライブがインストールされているかどうかに依存する Collate 機能がある場合は、自動的にプリンターが部単位印刷できるかどうかを決定するのに自動構成を使用できます。 GPD ファイルから次のコード例を検討してください。

```GPD
*% Printer supports collation only if PrinterHardDisk is installed
*Feature: Collate
{
  *rcNameID: 392 

  *DefaultOption: OFF
  *Option: ON
  {
    *rcNameID: =ON_DISPLAY
    *switch: PrinterHardDisk
    {
      *case: FALSE
      {
        *Command: CmdSelect
        {
           *Order: JOB_SETUP.5
           *% Collate requested but no disk =>
           *%   printer collate disabled
           *% Print Processor will take care
           *%   of collated copies

           *Cmd: ""
         }
      }
      *case: TRUE
      {
        *Command: CmdSelect
        {
           *Order: JOB_SETUP.5
           *% Collate requested with disk => 
            *%   printer collate enabled
           *% Printer will take care of collated copies

           *Cmd: "@PJL SET QTY=" %d{NumOfCopies}"<0A>"
        }
      }
    }
  }
  *Option: OFF
  {
    *rcNameID: =OFF_DISPLAY
    *Command: CmdSelect
    {
      *Order: JOB_SETUP.5
      *Cmd: ""
    }
  }
}

*% Feature to explicitly constrain the Collate feature
*Feature: PrinterHardDisk
{
  *rcNameID: 430 *% Printer Hard Disk
  *HelpIndex: 12002
  *FeatureType: PRINTER_PROPERTY
  *DefaultOption: FALSE
  *Option: FALSE
  {
    *rcNameID: 444
    *DisabledFeatures: Collate.ON
  }
  *Option: TRUE
  {
    *rcNameID: 443
  }
}
```

自動的に検出するかどうか、ハード_ディスクがインストールされている、を有効または無効にする照合状況に応じて、単に追加 GDL ファイルに次のコード例。

```GDL
*%The GDL parser merges this code with the corresponding feature construct in the GPD file
*Feature: PrinterHardDisk
{
  *% *BidiQuery and *BidiResponse constructs must have the same names
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








