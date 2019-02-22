---
title: 新しいデジタルを追加するコントロール パネルに書式設定します。
description: 新しいデジタルを追加するコントロール パネルに書式設定します。
ms.assetid: ce36738c-6471-4b68-82ad-80b8509c052b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f063c2d35dc62e8d9310a0adbfdc8b2b4f58908
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561048"
---
# <a name="adding-new-digital-formats-to-control-panel"></a>新しいデジタルを追加するコントロール パネルに書式設定します。


Windows Vista および以降のバージョンの Windows では、SPDIF 経由でサード パーティ製のデジタル オーディオ形式そのストリームを開発し、コントロール パネルの この形式を利用できます。

デジタル オーディオ形式を開発した後は、形式については、新しい GUID を定義し、関連付けられているオーディオ ドライバーをインストールする INF ファイルを使用します。 INF ファイルから次のコードでは、必要な情報が、新しいデジタル オーディオ形式をレジストリに追加する方法を示します。

```inf
[Version]
Signature=$WindowsNT$
...
[DDInstall]
AddReg = AddReg.NewDigitalFormat
...
...
[AddReg.NewDigitalFormat]
HKLM, %My_SubKey%, "DisplayName",,"ABC Audio"
HKLM, %My_SubKey%, "CustomIcon",,"c:\Program Files\MyVendor\myicon.ico"
HKLM, %My_SubKey%, "TestFile",,"c:\Program Files\MyVendor\testfile.wav"
...
[Strings]
My_SubKey = "SOFTWARE\Microsoft\Windows\CurrentVersion\MMDevices\SPDIF_Formats\{00000682-0000-0010-8000-00aa00389b71}"
...
...
```

前の例に示すように GUID で、\[文字列\]セクションは、新しいデジタル形式用に定義した GUID の配置を示すために使用します。 HKLM は HKEY の標準の省略形として使用される\_ローカル\_マシン。

**重要な**  Mycion.ico と Testfile.wav の 2 つの HKLM 行エントリが必要です。 "C:\\Program Files\\MyVendor\\"フォルダーを使用して、ドライバーに関連するアイコンの適切なフォルダーを作成および wave ファイルをテストする必要があります。

 

 

 




