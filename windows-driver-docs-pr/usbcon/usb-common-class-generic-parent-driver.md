---
Description: このセクションでは、複合デバイス用に Microsoft によって提供されるので、Usbccgp.sys ドライバーについて説明します。
title: USB 汎用親ドライバー (Usbccgp.sys)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0ecd4e815027c763921b339e3c0fb20b4f41867
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355040"
---
# <a name="usb-generic-parent-driver-usbccgpsys"></a>USB 汎用親ドライバー (Usbccgp.sys)


このセクションでは、複合デバイス用に Microsoft によって提供されるので、Usbccgp.sys ドライバーについて説明します。

多くの USB デバイスの公開複数*USB インターフェイス*します。 USB 用語では、これらのデバイスと呼ばれる*複合デバイス*します。 Microsoft Windows 2000 および Windows 98 オペレーティング システムには、別のデバイスとして複合デバイスの各インターフェイスを公開する USB バス ドライバー (Usbhub.sys) での一般的な親機能が含まれます。 この機能の簡素化し、向上と呼ばれる独立した、ドライバーに転送する Microsoft Windows XP と Windows Me、*一般的な親の USB ドライバー* (Usbccgp.sys)。 一般的な親ドライバーの機能を使用して、デバイス ベンダーは Microsoft によって提供されるドライバーのサポートの一部のインターフェイスの選択的に使用を行うことができます。

いくつかの複合デバイスのインターフェイスは独立して動作します。 たとえば、電源ボタンを持つ複合 USB キーボードには、キーボードの場合、1 つのインターフェイスと電源ボタンの別のインターフェイスがあります。 一般的な親の USB ドライバーでは、別のデバイスとしてこれらの各インターフェイスを列挙します。 オペレーティング システムは、キーボード インターフェイスを管理する Microsoft 提供のキーボード ドライバーと電源キー インターフェイスを管理する Microsoft 提供の電源キー ドライバーを読み込みます。

複合デバイスにネイティブの Windows ドライバーによってサポートされていないインターフェイスがある場合は、デバイスのベンダーは、インターフェイスと INF ファイルのドライバーを提供する必要があります。 INF ファイルの有効期限があります、INF *DDInstall*インターフェイスのデバイス ID と一致するセクション。 INF ファイルの読み込みを一般的な親ドライバーのため複合デバイス自体のデバイス ID に一致する必要があります。 オペレーティング システムが汎用的な親の USB ドライバーを読み込む方法の詳細については、次を参照してください。 [USB の複合デバイスの列挙体](enumeration-of-the-composite-parent-device.md)します。

一部のデバイス グループのインターフェイスに*コレクション インターフェイス*を使用する特定の実行と*関数*します。 インターフェイスのコレクションにグループ化しているインターフェイス、一般的な親ドライバーはそれぞれ個別のインターフェイスではなく、各コレクションは、デバイスとして扱います。 一般的な親ドライバー インターフェイスのコレクションを管理する方法の詳細については、次を参照してください。[複合デバイスを USB でインターフェイス コレクションの列挙体](support-for-interface-collections.md)します。

オペレーティング システムに複合デバイスのインターフェイス用のクライアント ドライバーが読み込まれた後、一般的な親ドライバーには、複合デバイスの 1 つのデータ ストリームにこれらの個別の相互作用を組み合わせることで、クライアント ドライバーからのデータ フローが多重化します。 一般的な親は、複合デバイス全体とそのインターフェイスのすべての電源ポリシーの所有者です。 また、同期と PnP 要求も管理します。

一般的な親ドライバーを簡単に複合のハードウェアのベンダーの場合、一部のインターフェイスが、Microsoft から提供されたドライバーがサポートします。 このようなデバイスのベンダーは、一般的な親ドライバーが Microsoft から提供されたドライバーのサポートされているインターフェイスの使用を容易にするためのインターフェイスでサポートされていない、ドライバーを提供する必要がありますのみ。

次のセクションでは、一般的な親ドライバーの機能をについて説明します。

[複合の USB デバイスの列挙体](enumeration-of-the-composite-parent-device.md)

[複合の USB デバイス上の記述子](descriptors-on-composite-usb-devices.md)

[複合の USB デバイス上のインターフェイスの列挙体](enumeration-of-interfaces-not-grouped-in-collections.md)

[複合の USB デバイスのインターフェイスのコレクションの列挙](support-for-interface-collections.md)

[Usbccgp.sys のコンテンツのセキュリティ機能](content-security-features-in-the-composite-client-generic-parent-drive.md)

## <a name="related-topics"></a>関連トピック
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



