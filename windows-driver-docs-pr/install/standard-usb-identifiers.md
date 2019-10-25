---
title: 標準の USB 識別子
description: 標準の USB 識別子
ms.assetid: 39acb62b-83f2-4d14-a678-c37817193f01
keywords:
- USB 識別子 WDK デバイスのインストール
- 単一インターフェイスデバイス WDK USB
- 複数インターフェイスデバイス WDK USB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b96dee6e69ed2eef4deecde8c3de704acabf9aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837349"
---
# <a name="standard-usb-identifiers"></a>標準の USB 識別子





<a href="" id="the-set-of-identifiers-generated-for-usb-devices-depends-on-whether-the-device-is-a-single-interface-device-or-a-multiple-interface-device-"></a>USB デバイス用に生成される一連の識別子は、デバイスが単一インターフェイスデバイスであるか、またはマルチインターフェイスデバイスであるかによって異なります。  

### <a name="single-interface-usb-devices"></a>シングルインターフェイス USB デバイス

新しい USB デバイスが接続されている場合、システムによって提供される USB ハブドライバーは、デバイスのデバイス記述子から抽出された情報を使用して、次のデバイス ID を作成します。

USB\\VID_v (4) & PID_d (4) & REV_r (4)

各値の意味は次のとおりです。

-   *v (4)* は、USB 委員会がベンダーに割り当てる4桁のベンダーコードです。

-   *d (4)* は、ベンダーがデバイスに割り当てる4桁の製品コードです。

-   *r (4)* はリビジョンコードです。

ハブドライバーは、デバイス記述子の*Idvendor*フィールドと*idvendor*フィールドから、それぞれベンダーと製品コードを抽出します。

INF モデルセクションでは、次のハードウェア ID を指定することもできます。

USB\\VID_v (4) & PID_d (4)

互換性のある Id は次のとおりです。

USB\\CLASS_c (2) & SUBCLASS_s (2) & PROT_p (2)

USB\\CLASS_c (2) & SUBCLASS_s (2)

USB\\CLASS_c (2)

各値の意味は次のとおりです。

-   *c (2)* は、デバイス記述子から取得されたデバイスクラスコードです。

-   *s (2)* は、デバイスのサブクラスコードです。

-   *p (2)* はプロトコルコードです。

デバイスクラスコード、サブクラスコード、およびプロトコルコードは、デバイス記述子の*Bdeviceclass、bDeviceSubClass、* および*bdeviceclass*の各フィールドによって決定されます。 2桁の数字です。

### <a name="multiple-interface-usb-devices"></a>マルチインターフェイス USB デバイス

複数のインターフェイスを持つデバイスは、*複合*デバイスと呼ばれます。 Windows 2000 以降では、新しい[usb 複合デバイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)がコンピューターに接続されると、usb ハブドライバーは物理デバイスオブジェクト (PDO) を作成し、子デバイスのセットが変更されたことをオペレーティングシステムに通知します。 新しい PDO に関連付けられているハードウェア識別子のハブドライバを照会した後、オペレーティングシステムは適切な INF ファイルを検索して、識別子の一致を検索します。 [ *USB\\複合*] 以外の一致が見つかった場合は、INF ファイルに示されているドライバーが読み込まれます。 ただし、その他の一致が見つからない場合、オペレーティングシステムでは、互換性のある ID *usb\\コンポジット*が使用されます。これにより、Usb 汎用親ドライバーが読み込まれます。 次に、汎用の親ドライバーが個別の PDO を作成し、複合デバイスのインターフェイスごとに個別のハードウェア識別子のセットを生成します。

各インターフェイスには、次の形式のデバイス ID があります。

USB\\ VID_v (4) & PID_d (4) & MI_z (2)

各値の意味は次のとおりです。

-   *v (4)* は、USB 委員会がベンダーに割り当てる4桁のベンダーコードです。

-   *d (4)* は、ベンダーがデバイスに割り当てる4桁の製品コードです。

-   *z (2)* は、インターフェイス記述子の*bInterfaceNumber*フィールドから抽出されたインターフェイス番号です。

INF モデルセクションでは、次の互換性のある Id を指定することもできます。

USB\\CLASS_d (2) & SUBCLASS_s (2) & PROT_p (2)

USB\\CLASS_d (2) & SUBCLASS_s (2)

USB\\CLASS_d (2)

USB\\複合

各値の意味は次のとおりです。

-   *d (2)* は、デバイス記述子から取得されたデバイスクラスコードです。

-   *s (2)* はサブクラスコードです。

-   *p (2)* はプロトコルコードです。

デバイスクラスコード、サブクラスコード、およびプロトコルコードは、それぞれインターフェイス記述子の*bInterfaceClass、bInterfaceSubClass、および bInterfaceProtocol*フィールドによって決定されます。 2桁の数字です。

 

 





