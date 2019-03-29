---
Description: Interfaces on a composite USB device can be grouped in collections or represent one USB function individually.
title: USB 複合デバイス上のインターフェイスの列挙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbf80573b7a1b02012e13216d1215a8bf6b90e30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573323"
---
# <a name="enumeration-of-interfaces-on-usb-composite-devices"></a>USB 複合デバイス上のインターフェイスの列挙


複合 USB デバイス上のインターフェイスは、個別に 1 つの USB 関数を表すこともコレクションにグループ化することができます。 インターフェイスは、コレクションにグループ分けされていない、ときに一般的な親ドライバーは各インターフェイスの PDO を作成し、各 PDO のハードウェア Id のセットを生成します。

*デバイス ID* PDO インターフェイスが、次の形式。

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

これらの id。

-   *v(4)* 仕入先に、USB 標準委員会を代入する 4 桁の仕入先のコードに示します。
-   *p(4)* 4 桁の製品コードは、ベンダーがデバイスに割り当てます。
-   *z(2)* から抽出されたインターフェイスの数が、 **bInterfaceNumber**インターフェイス記述子フィールド。

一般的な親ドライバー インターフェイス記述子から情報を使用して次の互換性のある Id も生成されます ([**USB\_インターフェイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff540065))。

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



