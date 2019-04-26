---
title: Additive テンプレート ディレクティブ
description: Additive テンプレート ディレクティブ
ms.assetid: 94883a51-a3a6-492e-9597-6a2f913d40bc
keywords:
- 加法ディレクティブ WDK GDL
- テンプレート WDK GDL、定義の順序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78b313c5588761c01a6db6cef331ccb445236dcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342220"
---
# <a name="additive-template-directive"></a>Additive テンプレート ディレクティブ


\***加法**: ディレクティブがテンプレートの定義の順序を定義します。

**加法**ディレクティブは、次の値のいずれかであることができます。

-   ほとんど\_最近使ったものです。 最新の定義のみが表示されます。

-   最小\_最近使ったものです。 最新のもの (最初) の定義のみが表示されます。

-   ほとんど\_TO\_最小\_最近使ったものです。 最新のものを最もから順序付けられたすべての定義が表示されます。

-   最小\_TO\_ほとんど\_最近使ったものです。 順序付けられたすべての定義が表示される少なくとも最新にします。

このディレクティブが不在であれば、ほとんどの既定値が場合\_最近使ったものと見なされます。

このディレクティブは、自体の乗算、テンプレート内で定義されているまたは継承によって関連付けられた複数のテンプレートが表示されます、最派生テンプレートで定義されている最近ディレクティブだけが受け入れられます。

 

 




