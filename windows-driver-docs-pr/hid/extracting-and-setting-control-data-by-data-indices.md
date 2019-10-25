---
title: データインデックスによるコントロールデータの抽出と設定
description: データインデックスによるコントロールデータの抽出と設定
ms.assetid: d26d169f-4116-4d81-94c7-63c92d22877d
keywords:
- HID レポート WDK、コントロールデータの設定
- WDK HID を報告し、コントロールデータを設定します
- HID レポート WDK、抽出 (コントロールデータを)
- WDK HID を報告し、コントロールデータを抽出します
- HID コントロールデータの抽出
- データインデックス WDK HID
- WDK HID データのインデックス作成
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 20779e7442951eed81462b2b7239021330bca3d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824835"
---
# <a name="extracting-and-setting-control-data-by-data-indices"></a>データインデックスによるコントロールデータの抽出と設定





[データインデックス](data-indices.md)を使用して hid レポートのコントロールデータを抽出して設定するために、アプリケーションまたはドライバーは次の hid サポートルーチンを使用できます。

[**HidP\_GetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getdata)

[**HidP\_SetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setdata)

これらのルーチンは、"付加価値" サービスを提供するアプリケーションまたはドライバーに特に役立ちます。 たとえば、HIDClass デバイスでサポートされているすべてのコントロールにカスタムインターフェイスを提供するとします。 Microsoft DirectInput は1つの例です。

これらのルーチンを呼び出すことにより、アプリケーションまたはドライバーは、レポート内のすべての値を効率的に取得および設定できます。 たとえば、 [HID の使用](hid-usages.md)法によってすべての値データを取得するには、使用するごとに[**Hidp\_getの値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)を呼び出す必要があります。 ただし、データインデックスによってすべての値データを取得するには、 **Hidp\_GetData**を1回だけ呼び出す必要があります。

アプリケーションまたはドライバーは、コレクションの[ボタン機能配列](button-capability-arrays.md)および[値機能配列](value-capability-arrays.md)で指定されたデータインデックスを使用して、HID の使用状況を識別します。

 

 




