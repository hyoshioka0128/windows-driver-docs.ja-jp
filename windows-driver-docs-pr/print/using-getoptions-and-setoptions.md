---
title: GetOptions と SetOptions の使用
description: GetOptions と SetOptions の使用
ms.assetid: c8b5c235-0b74-47c8-b6ba-eba810a8467b
keywords:
- GetOptions
- SetOptions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f75feac586ffc1d281ddafac7157d09e178c262d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374228"
---
# <a name="using-getoptions-and-setoptions"></a>GetOptions と SetOptions の使用





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

 

 




