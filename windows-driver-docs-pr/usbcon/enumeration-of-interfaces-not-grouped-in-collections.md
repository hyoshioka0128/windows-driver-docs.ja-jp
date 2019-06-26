---
Description: 複合 USB デバイス上のインターフェイスは、個別に 1 つの USB 関数を表すこともコレクションにグループ化することができます。
title: USB 複合デバイス上のインターフェイスの列挙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d6f815574f91886c2e9427fe6947bffe8df628f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386270"
---
# <a name="enumeration-of-interfaces-on-usb-composite-devices"></a>USB 複合デバイス上のインターフェイスの列挙


複合 USB デバイス上のインターフェイスは、個別に 1 つの USB 関数を表すこともコレクションにグループ化することができます。 インターフェイスは、コレクションにグループ分けされていない、ときに一般的な親ドライバーは各インターフェイスの PDO を作成し、各 PDO のハードウェア Id のセットを生成します。

*デバイス ID* PDO インターフェイスが、次の形式。

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

これらの id。

-   *v(4)* 仕入先に、USB 標準委員会を代入する 4 桁の仕入先のコードに示します。
-   *p(4)* 4 桁の製品コードは、ベンダーがデバイスに割り当てます。
-   *z(2)* から抽出されたインターフェイスの数が、 **bInterfaceNumber**インターフェイス記述子フィールド。

一般的な親ドライバー インターフェイス記述子から情報を使用して次の互換性のある Id も生成されます ([**USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_interface_descriptor))。

`USB\CLASS_d(2)&SUBCLASS_s(2)&PROT_p(2)`

`USB\CLASS_d(2)&SUBCLASS_s(2)`

`USB\CLASS_d(2)`

これらの id。

-   *d(2)* クラスのコードは、(**bInterfaceClass**)
-   *s(2)* サブクラス コード (**bInterfaceSubClass**)
-   *p(2)* プロトコルのコードは、(**bInterfaceProtocol**)

これらのコードの各は、4 桁の数字です。

## <a name="related-topics"></a>関連トピック
[複合の USB デバイスのインターフェイスのコレクションの列挙](support-for-interface-collections.md)  
[一般的な親の USB ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



