---
title: デバイス オブジェクトへの排他アクセスの指定
description: デバイス オブジェクトへの排他アクセスの指定
ms.assetid: b492251b-55b0-4323-a508-b395bb3da0ef
keywords:
- 排他的アクセス WDK デバイスオブジェクト
- デバイスオブジェクト WDK カーネル、排他アクセス
- 単一アクセス WDK デバイスオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa00699bf03fcc685374d1fe771b4522e042db3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836267"
---
# <a name="specifying-exclusive-access-to-device-objects"></a>デバイス オブジェクトへの排他アクセスの指定





デバイスへの排他アクセスが有効になっている場合、デバイスへのハンドルは一度に1つしか開くことができません。 I/o マネージャーがデバイスへの排他アクセスを適用するには、デバイススタック内の名前付きデバイスオブジェクトに対して排他的なプロパティを設定する必要があります。

PDO と FDO の両方がある WDM デバイススタックの場合、inf [**AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使用して、その排他プロパティを inf ファイルによってのみ設定できます。 PDO はスタック内の名前付きオブジェクトですが、関数ドライバーに代わって (関数ドライバー自体ではなく) バスドライバーが PDO を作成します。 バスドライバーが PDO の排他フラグを設定するように指示する唯一の方法は、クラスまたはデバイスの INF ファイルです。 ( [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)ルーチンを呼び出すと、FDO が作成されます。 FDO に対して排他フラグを設定しても効果はありません)。

非 WDM ドライバーや raw モードで動作するデバイスなど、デバイスオブジェクトがスタックされていないドライバーは、 [**Iocreatedevices ec生物**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)ルーチンを使用して、名前付きデバイスオブジェクトの排他プロパティを設定できます。

I/o マネージャーは、名前付きデバイスオブジェクトに対して、名前の後ろに排他性を適用します。 たとえば、デバイスオブジェクトの名前が "\\Device\\DeviceName" であるとします。 次に、i/o マネージャーは、"\\Device\\DeviceName\\*Filename1*" の後に "\\デバイス\\Devicename\\*Filename2*" を開くように要求するために排他性を適用します。 デバイススタック内の2つのオブジェクトに名前が付けられている場合 (推奨されません)、i/o マネージャーでは、オブジェクトごとに1つのハンドルを開くことができます。 このような状況では、ドライバーは[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)コールバック関数内で排他性自体を強制する必要があります。 また、i/o マネージャーでは、別のファイルハンドルに対して排他性のオープンが強制されることもありません。 デバイスの名前空間でのファイルオープン要求の詳細については、「[デバイスの名前空間へのアクセスの制御](controlling-device-namespace-access.md)」を参照してください。

 

 




