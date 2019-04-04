---
title: 同期 I/O のプログラミング
description: 同期 I/O のプログラミング
ms.assetid: ef021dd2-bd1d-4fb0-853f-014c62bda76b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a1150a71de7145522afdac9a7995caa5962ccda2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551270"
---
# <a name="synchronous-io-programming"></a>同期 I/O のプログラミング


同期のプログラミングは単に呼び出しが戻るまで待機します。 高速で、プログラマの観点からすると効率的になりますが、多くのプログラムが同時実行されている Windows のような環境では問題が発生します。 可能であればを使用して、 [I/O の非同期プログラミングの技法](asynchronous-i-o-programming.md)します。

**注**  ドライバー開発者は Microsoft Vista を使用して、これはほど深刻な問題になりません。 Vista での同期のプログラミングの詳細については、[Vista での待機を制限する](restricting-waits-in-vista.md)を参照してください。

 

 

 




