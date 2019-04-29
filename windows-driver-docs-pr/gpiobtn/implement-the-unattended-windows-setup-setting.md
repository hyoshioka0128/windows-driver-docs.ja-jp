---
title: Windows 無人セットアップ設定の実装
description: このトピックでは、無人 Windows セットアップ コンポーネントの設定を設定する方法について説明します。
ms.assetid: 593F8E05-F886-45FE-83EB-8DDD204F7900
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 392db897c42d4a96d02874f84e0a54e286a8ca12
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323417"
---
# <a name="implement-the-unattended-windows-setup-setting"></a>Windows 無人セットアップ設定の実装


このトピックでは、無人 Windows セットアップ コンポーネントの設定を設定する方法について説明します。

使用することを強くお勧め[Windows System Image Manager](https://go.microsoft.com/fwlink/p/?linkid=324691) Windows セットアップの無人ファイルを編集します。

出力ファイルのサンプルを次に示します。

``` syntax
<unattend xmlns="urn:schemas-microsoft-com:unattend">
  <settings pass="specialize">
    <component
        name="Microsoft-Windows-GPIOButtons"
        processorArchitecture="x86"> <!-- ... Additional component attributes-->
      <ConvertibleSlateMode>1</ConvertibleSlateMode> <!-- Values: {0 (slate); 1 (laptop)}-->
    </component>
  </settings>
</unattend>
```

 

 




