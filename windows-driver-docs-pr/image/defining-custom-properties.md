---
title: カスタム プロパティの定義
description: カスタム プロパティの定義
ms.assetid: c3b69482-12ad-4b9f-8c0c-5ce315032d51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0926f362cde777d51dc12336a2ea92d97380f110
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570306"
---
# <a name="defining-custom-properties"></a>カスタム プロパティの定義





カスタム プロパティを WIA を定義する WIA ミニドライバーの必要がある場合\_プライベート\_カスタム ルート項目のプロパティ、および、WIA DEVPROP プロパティを使用する必要があります\_プライベート\_ITEMPROP プロパティにする必要がありますその他のアイテムのプロパティを使用します。 これらの定数が定義されている*wiadef.h*します。

次のコード例では、次の 3 つのルート項目のプロパティの定義を示します。 最初のカスタム ルート項目プロパティ、カスタムのプロパティ ID\_ルート\_PROP\_WIA の観点から、1 が定義されている\_プライベート\_DEVPROP します。 WIA の観点から別のルート項目のプロパティのプロパティ Id が定義されている\_プライベート\_DEVPROP + 1 の場合、WIA\_プライベート\_DEVPROP + 2、という具合です。 追加のカスタム ルート項目のプロパティが必要な場合、パターンを続行できます。

```cpp
#define CUSTOM_ROOT_PROP_1 WIA_PRIVATE_DEVPROP
#define CUSTOM_ROOT_PROP_2 (WIA_PRIVATE_DEVPROP + 1) 
#define CUSTOM_ROOT_PROP_3 (WIA_PRIVATE_DEVPROP + 2) 
```

次の例では、次の 3 つのカスタムの子項目のプロパティおよびプロパティ Id の定義を示します。 最初のカスタムの子項目プロパティ、カスタムのプロパティ ID\_子\_PROP\_WIA の観点から、1 が定義されている\_プライベート\_ITEMPROP します。 WIA の観点からの他の子アイテムのプロパティのプロパティ Id が定義されている\_プライベート\_ITEMPROP + 1、という具合です。 として、前に、パターンを続行できますのカスタムの子項目プロパティが必要な場合。

```cpp
#define CUSTOM_CHILD_PROP_1 WIA_PRIVATE_ITEMPROP
#define CUSTOM_CHILD_PROP_2 (WIA_PRIVATE_ITEMPROP + 1) 
#define CUSTOM_CHILD_PROP_3 (WIA_PRIVATE_ITEMPROP + 2)
```

WIA のカスタム プロパティは、カスタム プロパティ Id に関連付けられているカスタム プロパティ名をいる必要があります。 次のコード例では、次の 3 つのカスタム ルート項目のプロパティ名の定義を示します。 (カスタムのカスタム プロパティの名前が含まれているカスタム プロパティの前の例で作成された Id を使用してこれらのプロパティ名は使用\_ルート\_PROP\_1\_STR は、カスタム ルートを関連付けるitem プロパティ ID カスタム\_ルート\_PROP\_1)。

```cpp
#define CUSTOM_ROOT_PROP_1_STR L"My First Custom Root Item Property"
#define CUSTOM_ROOT_PROP_2_STR L"My Second Custom Root Item Property"
#define CUSTOM_ROOT_PROP_3_STR L"My Third Custom Root Item Property"
```

**注**   WIA プロパティ名は*いない*複数の言語でローカライズされました。 WIA プロパティがプロパティ ID またはプロパティ名を使用してアプリケーションが読み取れるためにです。 名前が使用されている場合は、定数の場合、ID がプロパティとしてだけがあります。
