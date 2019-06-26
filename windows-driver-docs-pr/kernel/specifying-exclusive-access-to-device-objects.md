---
title: デバイス オブジェクトへの排他アクセスの指定
description: デバイス オブジェクトへの排他アクセスの指定
ms.assetid: b492251b-55b0-4323-a508-b395bb3da0ef
keywords:
- WDK デバイス オブジェクトの排他アクセス
- デバイス オブジェクトの WDK カーネル、排他アクセス
- WDK デバイス オブジェクトの 1 つのアクセス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38073af8b8b1a76febd38a073ba5daa770e58d5a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383015"
---
# <a name="specifying-exclusive-access-to-device-objects"></a>デバイス オブジェクトへの排他アクセスの指定





デバイスへの排他アクセスが有効になっている場合は、デバイスへのハンドルの 1 つだけ開くことができる、時にします。 デバイスへの排他アクセスを強制する I/O マネージャーには、デバイス スタック内の名前付きのデバイス オブジェクトの排他のプロパティを設定する必要があります。

WDM デバイス スタックを両方 PDO を持つ、FDO 排他プロパティ設定できます、INF ファイルでのみを使用して、 [ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)します。 PDO はスタックでは、名前付きオブジェクトですが、バス ドライバー (関数ドライバーではなく自体) が関数ドライバーに代わって、PDO を作成します。 クラスまたはデバイスの INF ファイルでは、PDO の排他フラグを設定するバス ドライバーに指示するしかありません。 (への呼び出し、 [ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)ルーチン、FDO を作成しますは、FDO を排他フラグを設定しても効果はありません。)。

ドライバーを持つデバイス オブジェクトが積み上げ縦棒グラフで、非 WDM ドライバーと raw モードで動作するデバイスなどを使用して、 [ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)ルーチンの名前付きの排他的なプロパティを設定するにはデバイス オブジェクト。

I/O マネージャーは、排他的に末尾の名前に関係なく、名前付きのデバイス オブジェクトを名前ごとに実行を強制します。 たとえば、デバイス オブジェクトが名前"\\デバイス\\DeviceName"。 I/O マネージャーの排他性を開く要求を適用し、"\\デバイス\\DeviceName\\*Filename1*「の後に」\\デバイス\\DeviceName\\ *Filename2*"。 デバイス スタックの 2 つのオブジェクトは、(これは推奨されません) という名前は、I/O マネージャーが各オブジェクト用に開かれる単一のハンドル。 このような場合は、ドライバー適用する必要がある排他的自体内でその[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)コールバック関数。 また、I/O マネージャーでは、排他性を開くもう 1 つのファイル ハンドルを基準は適用されません。 デバイスの名前空間内のファイル オープン要求の詳細については、次を参照してください。[デバイス Namespace のアクセスを制御する](controlling-device-namespace-access.md)します。

 

 




