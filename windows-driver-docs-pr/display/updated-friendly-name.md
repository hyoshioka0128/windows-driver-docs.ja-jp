---
title: WDDM 1.2 の更新済みのフレンドリ名
description: このトピックでは、グラフィックス INF の更新のフレンドリ名を示します。 これは、すべての Windows 8 インボックス ディスプレイ ドライバーの Inf のローカライズ可能な文字列名要件です。
ms.assetid: 26AE24C4-3C0D-4712-B66A-0B93FAD8043C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71c829989273bec11a093693ab75ad8d70fc7ea8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580678"
---
# <a name="updated-friendly-name-for-wddm-12"></a>WDDM 1.2 の更新済みのフレンドリ名


このトピックでは、グラフィックス INF の更新のフレンドリ名を示します。 これは、すべての Windows 8 インボックス ディスプレイ ドライバーの Inf のローカライズ可能な文字列名要件です。

すべての Windows 8 のインボックス ドライバーは、わかりやすい名前に関係なく、E3 特徴のスコアを使用する必要があります。 ここで説明されている INF でサポートされているドライバー モデルは、フレンドリ名が反映されます。

Windows 8 でテストされていると、Windows 8 で (Microsoft Corporation の WDDM v1.2) ボックスに含まれる Windows Display Driver Model (WDDM) 1.2 ドライバーのこの例で示すように、デバイス名に追加する必要があります。

``` syntax
;
; Localizable Strings
;
IHV_DeviceName.XXX = "My Device Name (Microsoft Corporation - WDDM v1.2)"
```

**注**  入力であるユーザーを容易に判断できるように、次をお勧めのみ、テスト用の Windows 8 用に最適化された Windows 8 固有の省略可能な機能を有効にされるドライバーを簡単に強調表示にします。標準の Windows 8 ドライバー。 (これも簡素化するバグをトリアージ)。

 

以下に例を示します。WDDM 1.2 特定の作業

``` syntax
IHV_DeviceName.XXX = "My Device Name (Engineering Sample - WDDM v1.2)"
```

Windows 8 でテストされていると、Windows 8、(Microsoft Corporation の WDDM v1.1) には、ボックスに含まれる、WDDM 1.1 ドライバーのこの例で示すように、デバイス名に追加する必要があります。

``` syntax
;
; Localizable Strings
;
IHV_DeviceName.XXX = "My Device Name (Microsoft Corporation - WDDM v1.1)"
```

Windows 8 でテストされていると、Windows 8 で (Microsoft Corporation の WDDM v1.0) ボックスに含まれる、WDDM 1.0 ドライバーのこの例で示すように、デバイス名に追加する必要があります。

``` syntax
;
; Localizable Strings
;
IHV_DeviceName.XXX = "My Device Name (Microsoft Corporation - WDDM v1.0)"
```

 

 





