---
title: 無人 Windows セットアップの設定を実装します。
description: このトピックでは、無人 Windows セットアップ コンポーネントの設定を設定する方法について説明します。
ms.assetid: 593F8E05-F886-45FE-83EB-8DDD204F7900
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 392db897c42d4a96d02874f84e0a54e286a8ca12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552343"
---
# <a name="implement-the-unattended-windows-setup-setting"></a>無人 Windows セットアップの設定を実装します。


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

 

 




