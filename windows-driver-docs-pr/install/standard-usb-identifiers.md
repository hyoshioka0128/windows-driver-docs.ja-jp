---
title: 標準の USB 識別子
description: 標準の USB 識別子
ms.assetid: 39acb62b-83f2-4d14-a678-c37817193f01
keywords:
- USB 識別子 WDK デバイスのインストール
- 単一インターフェイス デバイス WDK USB
- 複数インターフェイス デバイス WDK USB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 278434ff8936d3ecd3067defc3d817ffd5aac922
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573558"
---
# <a name="standard-usb-identifiers"></a>標準の USB 識別子





<a href="" id="the-set-of-identifiers-generated-for-usb-devices-depends-on-whether-the-device-is-a-single-interface-device-or-a-multiple-interface-device-"></a>USB デバイス用に生成された識別子のセットは、デバイスが 1 つインターフェイス デバイスまたは複数インターフェイス デバイスによって異なります。  

### <a name="single-interface-usb-devices"></a>単一インターフェイスの USB デバイス

新しい USB デバイスを接続、システム提供の USB ハブのドライバーは、デバイスのデバイスの記述子から抽出された情報を使用して、次のデバイス ID を作成します。

USB\\VID_v(4) & PID_d(4) REV_r(4)

各項目の意味は次のとおりです。

-   *v(4)* 仕入先に、USB 委員会を代入する 4 桁の仕入先のコードに示します。

-   *d(4)* 4 桁のプロダクト コードは、ベンダーがデバイスに割り当てます。

-   *r(4)* リビジョン コードに示します。

ハブのドライバーのベンダーと製品コードを抽出し、 *idVendor*と*idProduct*デバイス記述子のフィールドそれぞれします。

INF モデルのセクションでは、次のハードウェア ID も指定できます。

USB\\VID_v(4) & PID_d(4)

互換性のある次の Id。

USB\\CLASS_c(2) & SUBCLASS_s(2) PROT_p(2)

USB\\CLASS_c(2) & SUBCLASS_s(2)

USB\\CLASS_c(2)

各項目の意味は次のとおりです。

-   *c(2)* デバイス記述子から取得したデバイス クラスのコードに示します。

-   *s(2)* デバイス サブクラス コードに示します。

-   *p(2)* プロトコル コードに示します。

デバイス クラスのコード、サブクラス コード、およびプロトコルのコードによって決まりますが、 *bDeviceClass、bDeviceSubClass、* と*bDeviceProtocol*デバイス記述子のフィールドそれぞれします。 これらは、2 桁の数字です。

### <a name="multiple-interface-usb-devices"></a>複数のインターフェイスの USB デバイス

複数のインターフェイスを持つデバイスと呼ばれる*複合*デバイス。 以降では、Windows 2000 では、新しい[複合デバイスを USB](https://msdn.microsoft.com/library/windows/hardware/ff537109)が接続されているコンピューターに USB ハブのドライバーが物理デバイス オブジェクト (PDO) を作成し、オペレーティング システム、デバイスの子のセットが変更されたことを通知します。 新しい PDO に関連付けられているハードウェア識別子のハブのドライバーのクエリを実行するには後、は、オペレーティング システムは、識別子と一致するものを該当する INF ファイルを検索します。 他にも一致が見つかった場合*USB\\複合*、INF ファイルに示されているドライバーが読み込まれます。 ただし、他の一致が見つからない場合、オペレーティング システムを使用、互換性のある ID *USB\\複合*、どの it の一般的な親の USB ドライバーを読み込みます。 一般的な親ドライバーに、個別の PDO を作成し、複合デバイスの各インターフェイスのハードウェア識別子の別のセットを生成します。

各インターフェイスには、次の形式のデバイス ID があります。

USB\\ VID_v(4) & PID_d(4) MI_z(2)

各項目の意味は次のとおりです。

-   *v(4)* 仕入先に、USB 委員会を代入する 4 桁の仕入先のコードに示します。

-   *d(4)* 4 桁のプロダクト コードは、ベンダーがデバイスに割り当てます。

-   *z(2)* から抽出されたインターフェイスの数が、 *bInterfaceNumber*インターフェイス記述子フィールド。

INF モデルのセクションでは、次の互換性のある Id も指定できます。

USB\\CLASS_d(2) & SUBCLASS_s(2) PROT_p(2)

USB\\CLASS_d(2) & SUBCLASS_s(2)

USB\\CLASS_d(2)

USB\\複合

各項目の意味は次のとおりです。

-   *d(2)* デバイス記述子から取得したデバイス クラスのコードに示します。

-   *s(2)* サブクラス コードに示します。

-   *p(2)* プロトコル コードに示します。

デバイス クラスのコード、サブクラス コード、およびプロトコルのコードによって決まりますが、 *bInterfaceClass、bInterfaceSubClass、および bInterfaceProtocol*インターフェイス記述子のフィールドそれぞれします。 これらは、2 桁の数字です。

 

 





