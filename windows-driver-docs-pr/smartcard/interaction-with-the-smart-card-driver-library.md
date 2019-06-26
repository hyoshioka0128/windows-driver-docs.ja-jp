---
title: スマート カード ドライバー ライブラリとの相互作用
description: スマート カード ドライバー ライブラリとの相互作用
ms.assetid: 44cf41f4-bbff-4193-afad-6d4106ce50c3
keywords:
- Ioctl WDK のスマート カード
- ベンダーから提供されたドライバー WDK スマート カード、IOCTL 要求の管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e9f9ffcfca73558d1c0da2598d9d75e6c47af7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356721"
---
# <a name="interaction-with-the-smart-card-driver-library"></a>スマート カード ドライバー ライブラリとの相互作用


## <span id="_ntovr_interaction_with_the_smart_card_driver_library"></span><span id="_NTOVR_INTERACTION_WITH_THE_SMART_CARD_DRIVER_LIBRARY"></span>


次の図では、リーダーのドライバーと対話する方法、スマート カードのドライバー ライブラリ リソース マネージャーから受け取る IOCTL 要求を処理するためには示しています。

![リーダーのドライバーが ioctl 要求を処理するスマート カードのドライバー ライブラリと対話する方法を示す図 ](images/memnum3.png)

次の番号は、前の図の番号に対応します。 番号 1 から始めて、図に示します手順では、リーダーのドライバーは、IOCTL 要求を処理する (システムによって提供されるドライバー ライブラリ) と共に完了する必要があること。

1.  リーダーのドライバーのすべての IOCTL 要求を渡します、 [ **SmartcardDeviceControl (WDM)** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))ドライバー ライブラリ ルーチン。

2.  場合に、リーダーのドライバーが渡されるパラメーター [ **SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))が正しくない**SmartcardDeviceControl**エラー メッセージを返します。 **SmartcardDeviceControl** IOCTL 要求を完了することがなくを返します。 このような状況では、リーダーのドライバーが IOCTL 要求を完了する必要があります。

3.  パラメーターは、有効な場合[ **SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))可能な場合は、IOCTL 要求を処理します。

4.  [**SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))リーダーのドライバーが処理中の IOCTL 要求に対して定義されているコールバック ルーチンであるかどうかを確認します。 コールバックが存在する場合、 **SmartcardDeviceControl**は関数を呼び出します。

5.  コールバック ルーチンは、すべてのドライバーの IOCTL 要求の処理を完了するために必要なライブラリ ルーチンを呼び出します。

6.  IOCTL 要求を処理するには後、に、コールバック ルーチンに戻ります[ **SmartcardDeviceControl**](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))します。

7.  [**SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85)) IOCTL を持ち込むことの IRP が完了するとします。

8.  [**SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))リーダー ドライバー ディスパッチ ルーチンに制御を返します。

スマート カードのライブラリは、リーダーのドライバーへのアクセスを同期します。 2 つのコールバック関数はありませんが、同時に呼び出されます。 ただし、カードの挿入と削除の処理イベントを非同期的に処理する必要があります。

 

 





