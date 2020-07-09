---
title: デバイスアクセスの制御 (WDM)
description: デバイス アクセスの制御
ms.assetid: b5e562ad-573b-4b0f-9d85-2410fda16e4e
keywords:
- デバイスオブジェクト WDK カーネル、セキュリティ
- セキュリティ WDK デバイスオブジェクト
- デバイスアクセス制御 WDK カーネル
- 非 WDM ドライバーデバイスアクセス WDK カーネル
- セキュリティ記述子 WDK デバイスオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: df64a4461f4768aab2c73b358b60274eae0b974e
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141270"
---
# <a name="controlling-device-access-wdm"></a>デバイスアクセスの制御 (WDM)





デバイスへのアクセスは、セキュリティ記述子 (およびそれに含まれる ACL) によって制御されます。 デバイスオブジェクトのセキュリティ記述子は、デバイスオブジェクトを作成するとき、またはレジストリで設定するときに指定できます。

### <a name="controlling-device-access-for-wdm-drivers"></a>WDM ドライバーのデバイスアクセスの制御

WDM ドライバー (特定のバスドライバー以外) がデバイスオブジェクトを作成すると、プラグアンドプレイ manager によってデバイスのセキュリティ記述子が決定されます。 操作の順序は次のとおりです。

1.  PnP マネージャーは、ドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出します。

2.  ドライバーの*AddDevice*ルーチンは、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)を呼び出してデバイスオブジェクトを作成し、デバイスオブジェクトスタックにアタッチします。

3.  PnP マネージャーは、新しく作成されたデバイスオブジェクトのセキュリティ記述子を更新します。

WDM ドライバーの場合、PnP マネージャーによって、デバイスオブジェクトのセキュリティ記述子が次のように決定されます。

1.  デバイスのセキュリティ記述子設定がレジストリに設定されている場合は、デバイススタック内のすべてのオブジェクトに適用されます。

2.  そうしないと、デバイスのセットアップクラスのセキュリティ記述子がレジストリに設定されている場合、デバイススタック内のすべてのオブジェクトに適用されます。

3.  それ以外の場合、PnP マネージャーは、各オブジェクトの既定のセキュリティ記述子を変更せずに残します。 この場合、スタックの既定のセキュリティ記述子は、PDO のデバイスの種類とデバイスの特性によって決まります。

ほとんどのデバイスの種類と特性において、既定のセキュリティ記述子は、 \_ 管理者、読み取り、書き込み、実行アクセス (一般 \_ 読み取り |) へのフルアクセス (汎用すべて) を付与します。一般的な \_ 書き込み |汎用 \_ 実行) 他のすべてのユーザーにアクセスします。

レジストリでデバイスまたはデバイスのセットアップクラスのセキュリティ記述子を設定する方法の詳細については、「[レジストリにデバイスオブジェクトのプロパティを設定](setting-device-object-properties-in-the-registry.md)する」を参照してください。

デバイスが raw モードで操作されている場合、PnP マネージャーはデバイスオブジェクトのセキュリティ記述子を特定できません。 その場合、バスドライバーはセキュリティ記述子を提供する必要があります。以下を参照してください。

### <a name="controlling-device-access-for-wdm-bus-drivers"></a>WDM バスドライバーのデバイスアクセスの制御

WDM バスドライバーは、raw モードで運用できるすべてのデバイスの PDO のセキュリティ記述子を提供する必要があります。 [**Iocreateデバイス ecを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)使用して、セキュリティ記述子を持つデバイスオブジェクトを作成します。

バスドライバーが raw モードでデバイスを操作しない場合、セキュリティ記述子を指定する必要はありません。 前に説明したように、PnP マネージャーによってセキュリティ記述子が決定されます。 バスドライバーは、PDOs が既定の記述子よりも厳密なセキュリティ設定を持つようにする必要がある場合、セキュリティ記述子を提供できます。 バスドライバーによって指定された記述子は、レジストリの設定によって上書きされます。

デバイスオブジェクトの作成の詳細については、「[デバイスオブジェクトの作成](creating-a-device-object.md)」を参照してください。

### <a name="controlling-device-access-for-non-wdm-drivers"></a>WDM 以外のドライバーのデバイスアクセスを制御する

WDM 以外のドライバーでは、作成する任意の名前付きデバイスオブジェクトの既定のセキュリティ記述子とクラス GUID を指定する必要があります。

**Iocreateデバイス ecの**ルーチンを使用して、名前付きデバイスオブジェクトを作成し、そのデバイスの既定のセキュリティ記述子とクラス GUID を指定します。 セキュリティ記述子は、SDDL のサブセットに指定されています。 詳細については、「[デバイスオブジェクトの SDDL](sddl-for-device-objects.md)」を参照してください。

システムは、指定されたクラス GUID のレジストリのセキュリティ設定を使用して、既定のセキュリティ記述子を上書きします。 ドライバーは、デバイスに固有の一意の GUID を指定する必要があります。 一意の GUID を生成するには、Guidgen.exe ツールを使用します。 (Guidgen.exe は Microsoft Windows SDK に含まれています)。

 

 




