---
title: C28176
description: 警告 C28176 構造体のメンバーは、ドライバーによって変更されてはなりません。
ms.assetid: 837b2dcd-0682-460f-a3ae-ebd82bcc451b
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28176
ms.openlocfilehash: 2e0e2ea1ae7d3e8360fac0755b9b18f4371bf1c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839591"
---
# <a name="c28176"></a>C28176


警告 C28176: 構造体のメンバーはドライバーによって変更されないようにする必要があります

この警告は、ドライバーによって変更されないように、ドキュメント化されていない構造体のメンバーが変更されたことを示します

ドライバーは、指定された非公開の構造体のメンバーに書き込むことはできません。 不透明な、または部分的に不透明な構造体のほとんどのドキュメントに記載されていないメンバーの場合、この禁止は absolute です。 ただし、ドライバーは、特定のルーチン内から、ドキュメントに記載されていない構造体のメンバーを書き込む場合があります。 たとえば、[**デバイス\_オブジェクトなどです。NextDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)メンバーを書き込むことができるのは、初期化またはドライバー\_のアンロードルーチン\_ドライバー内に限られています。

 

 





