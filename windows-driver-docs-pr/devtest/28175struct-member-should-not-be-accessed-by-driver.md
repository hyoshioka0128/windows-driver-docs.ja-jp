---
title: C28175
description: 警告 C28175 が構造体のメンバーをドライバーによってアクセスはできません。
ms.assetid: 259a90d7-29ef-4a27-a921-8fff93b325bd
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28175
ms.openlocfilehash: 43377d72e9ead2717eaab983993ddfe8ecc2df58
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371480"
---
# <a name="c28175"></a>C28175


C28175 を警告します。構造体のメンバーをドライバーによってアクセスはできません。

この警告は、ドライバーがドライバーにアクセスする必要がありますしないを文書化されていない構造体メンバーをアクセスすることを示します。

ドライバーでは、指定されたドキュメントに未記載の構造体のメンバーはアクセスしないでください。 非透過または部分的に非透過構造体のメンバーの最も文書化されていない場合は、この禁止は絶対です。 ただし、ドライバーは、特定するルーチン内から特定のドキュメントに未記載の構造体メンバーをアクセスすることがあります。 ドライバーが部分的に非透過のドキュメントに未記載のメンバーにアクセスなど、 [**ドライバー\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_driver_object)ドライバー内でのみ構造\_の初期化またはドライバー\_アンロード ルーチン。

このルールは、特定のメンバーに適用される理由はすぐに明らかではありません。 たとえば、これが 1 つのインスタンスはでは、 **NextDevice**のメンバー **\_デバイス\_オブジェクト**します。 このインスタンスではロックは、ドライバーを使用できませんにロックにこのリンクのリストを安全にアクセスする使用する必要があります。 この場合、この規則に違反する頻度の低いが、診断が難しいとエラーが発生します。 関連するデバイスにアクセスする適切な方法は使用する、 [ **IoEnumerateDeviceObjectList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ioenumeratedeviceobjectlist)関数。

 

 





