---
title: GetOptions と SetOptions を使用してください。
description: GetOptions と SetOptions を使用してください。
ms.assetid: c8b5c235-0b74-47c8-b6ba-eba810a8467b
keywords:
- GetOptions
- SetOptions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f75feac586ffc1d281ddafac7157d09e178c262d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528981"
---
# <a name="using-getoptions-and-setoptions"></a>GetOptions と SetOptions を使用してください。





**GetOptions**によって指し示されるバッファー内のキーワードが表示されている機能のドライバーの現在の設定の取得を呼び出すことができます、 *pmszFeaturesRequested*入力パラメーター。

呼び出しなどで**GetOptions**を*pmszFeaturesRequested*入力バッファーには、この文字列が含まれています (マルチで\_SZ 形式)。

```cpp
"PageSize\0Duplex\0Resolution\0\0"
```

後に、 **GetOptions**メソッドが返される出力*pmszFeatureOptionBuf* 、次の文字列を含めることができます (複数でも\_SZ 形式)。

```cpp
"PageSize\0Letter\0Duplex\0DuplexTumble\0Resolution\0300dpi\0\0"
```

この例では**GetOptions** PageSize (文字)、二重 (DuplexTumble)、および解決 (300 dpi) のオプションのキーワードを取得します。

**SetOptions**で機能またはオプションのキーワードの組み合わせに基づいて、ドライバーの現在の設定を変更するということができます、 *pmszFeatureOptionBuf*入力バッファー。

サポートされている機能の 2 つのカテゴリがあります。

[PPD 機能](ppd-features.md)

[ドライバーの機能](driver-features.md)

 

 




