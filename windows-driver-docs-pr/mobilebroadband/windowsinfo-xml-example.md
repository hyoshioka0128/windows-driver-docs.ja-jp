---
title: WindowsInfo XML の例
description: WindowsInfo XML の例
ms.assetid: 5933512e-d2bf-437f-abd8-dc3486e07be0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4acfab86a850273fa47fab1b2f4b72f7a13601f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578669"
---
# <a name="windowsinfo-xml-example"></a>WindowsInfo XML の例

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

次の XML ドキュメントを使用して、 [WindowsInfo XML スキーマ](windowsinfo-xml-schema.md)メタデータ パッケージ内で指定されているサービスの表示動作を指定します。

``` syntax
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<WindowsInfo xmlns="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/"
             xmlns:v2="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/WindowsInfov2">
  <ShowDeviceInDisconnectedState>false</ShowDeviceInDisconnectedState>
</WindowsInfo>
```

 

 





