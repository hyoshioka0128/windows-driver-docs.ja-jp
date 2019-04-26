---
title: 同期 I/O のプログラミング
description: 同期 I/O のプログラミング
ms.assetid: ef021dd2-bd1d-4fb0-853f-014c62bda76b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a1150a71de7145522afdac9a7995caa5962ccda2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345428"
---
# <a name="synchronous-io-programming"></a>同期 I/O のプログラミング


同期のプログラミングは単に呼び出しが戻るまで待機します。 高速で、プログラマの観点からすると効率的になりますが、多くのプログラムが同時実行されている Windows のような環境では問題が発生します。 可能であればを使用して、 [I/O の非同期プログラミングの技法](asynchronous-i-o-programming.md)します。

**注**  ドライバー開発者は Microsoft Vista を使用して、これはほど深刻な問題になりません。 Vista での同期のプログラミングの詳細については、次を参照してください。 [Vista での待機を制限する](restricting-waits-in-vista.md)します。

 

 

 




