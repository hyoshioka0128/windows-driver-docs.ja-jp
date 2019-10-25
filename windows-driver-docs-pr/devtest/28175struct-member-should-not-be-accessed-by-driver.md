---
title: C28175
description: 警告 C28175 構造体のメンバーにドライバーからアクセスすることはできません。
ms.assetid: 259a90d7-29ef-4a27-a921-8fff93b325bd
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28175
ms.openlocfilehash: ad7e951940569535e83044217f9968385f12868a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840311"
---
# <a name="c28175"></a>C28175


警告 C28175: 構造体のメンバーにドライバーからアクセスすることはできません

この警告は、ドライバーがアクセスすることができない、ドキュメント化されていない構造体のメンバーにドライバーがアクセスしたことを示します。

ドライバーは、指定された非公開の構造体のメンバーにアクセスすることはできません。 不透明な、または部分的に不透明な構造体のほとんどのドキュメントに記載されていないメンバーの場合、この禁止は absolute です。 ただし、ドライバーは、特定のルーチン内から、非公開の構造体のメンバーにアクセスする場合があります。 たとえば、ドライバーは、部分的に不透明になっているドライバー [ **\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)構造の一部が非透過的なメンバーにアクセスすることがあります\_INITIALIZE またはドライバー\_のアンロードルーチン。

この規則が特定のメンバーに適用される理由がすぐに明確ではない場合があります。 たとえば、このような状況が発生する1つのインスタンスは、 **\_デバイス\_オブジェクト**の**nextdevice**メンバーです。 この場合、このリンクリストに安全にアクセスするためにロックを使用する必要がありますが、そのロックをドライバーで使用することはできません。 この場合、この規則に違反すると、発生頻度が低いが、診断が困難になります。 関連するデバイスにアクセスする適切な方法は、 [**IoEnumerateDeviceObjectList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioenumeratedeviceobjectlist)関数を使用することです。

 

 





