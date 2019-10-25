---
Description: 複合 USB デバイスのインターフェイスは、コレクション内にグループ化することも、1つの USB 機能を個別に表すこともできます。
title: USB 複合デバイス上のインターフェイスの列挙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38145018b08f977bb0aa862a2980e1b8fa3dc2c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845011"
---
# <a name="enumeration-of-interfaces-on-usb-composite-devices"></a>USB 複合デバイス上のインターフェイスの列挙


複合 USB デバイスのインターフェイスは、コレクション内にグループ化することも、1つの USB 機能を個別に表すこともできます。 インターフェイスがコレクション内でグループ化されていない場合、汎用の親ドライバーは、各インターフェイスに対して PDO を作成し、各 PDO に対して一連のハードウェア Id を生成します。

インターフェイス PDO の*デバイス ID*には、次の形式があります。

`USB\VID_v(4)&PID_p(4)&MI_z(2)`

次の Id の場合:

-   *v (4)* は、USB 標準委員会がベンダーに割り当てる4桁のベンダーコードです。
-   *p (4)* は、ベンダーがデバイスに割り当てる4桁の製品コードです。
-   *z (2)* は、インターフェイス記述子の**bInterfaceNumber**フィールドから抽出されたインターフェイス番号です。

汎用の親ドライバーも、インターフェイス記述子 ([**USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)) からの情報を使用して、次の互換性のある id を生成します。

`USB\CLASS_d(2)&SUBCLASS_s(2)&PROT_p(2)`

`USB\CLASS_d(2)&SUBCLASS_s(2)`

`USB\CLASS_d(2)`

次の Id の場合:

-   *d (2)* はクラスコード (**bInterfaceClass**) です。
-   *s (2)* はサブクラスコード (**bInterfaceSubClass**) です。
-   *p (2)* はプロトコルコード (**binterfaceprotocol**) です。

これらの各コードは4桁の数字です。

## <a name="related-topics"></a>関連トピック
[USB 複合デバイス上のインターフェイスコレクションの列挙](support-for-interface-collections.md)  
[USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



