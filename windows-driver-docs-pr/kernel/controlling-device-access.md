---
title: デバイス アクセスの制御
description: デバイス アクセスの制御
ms.assetid: b5e562ad-573b-4b0f-9d85-2410fda16e4e
keywords:
- デバイス オブジェクトの WDK カーネル、セキュリティ
- WDK デバイス オブジェクトのセキュリティ
- デバイスへのアクセス制御の WDK カーネル
- 非 WDM ドライバー デバイス アクセス WDK カーネル
- WDK のデバイス オブジェクトのセキュリティ記述子
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3d54ab5ccbfe4537b2ce651edfad5fde3ecdc87
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377203"
---
# <a name="controlling-device-access"></a>デバイス アクセスの制御





セキュリティ記述子によってデバイスへのアクセスが制御されます (および、ACL が含まれています)。 デバイス オブジェクトを作成、またはレジストリの設定時、デバイス オブジェクトのセキュリティ記述子を指定できます。

### <a name="controlling-device-access-for-wdm-drivers"></a>WDM ドライバーのデバイスへのアクセスを制御します。

(特定のバス ドライバー) を除く WDM ドライバーでは、デバイス オブジェクトを作成するとき、プラグ アンド プレイ マネージャーは、デバイスのセキュリティ記述子を決定します。 操作の順序は次のとおりです。

1.  PnP マネージャーには、ドライバーの[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。

2.  ドライバーの*AddDevice*ルーチンの呼び出し[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)デバイス オブジェクトを作成し、デバイス オブジェクトのスタックにアタッチします。

3.  PnP マネージャーでは、新しく作成したデバイス オブジェクトのセキュリティ記述子を更新します。

WDM ドライバーの場合は、PnP マネージャーは、デバイス オブジェクトのセキュリティ記述子を次のように決定します。

1.  デバイスでは、レジストリにセキュリティ記述子の設定が含まれる場合、デバイス スタック内のすべてのオブジェクトに適用されます。

2.  それ以外の場合、デバイスのセットアップ クラスでは、レジストリにセキュリティ記述子の設定が含まれる場合、デバイス スタック内のすべてのオブジェクトに適用されます。

3.  それ以外の場合、PnP マネージャーは、各オブジェクトの未変更の既定のセキュリティ記述子を残します。 この場合、スタックの既定のセキュリティ記述子は、デバイスの種類と、PDO のデバイスの特性によって決まります。

ほとんどのデバイスの種類と特性は、既定のセキュリティ記述子ではフル アクセス (ジェネリック\_すべて) 管理者、および読み取り、書き込み、および実行アクセス権 (ジェネリック\_読み取り |ジェネリック\_書き込み |ジェネリック\_EXECUTE) その他のユーザーへのアクセス。

レジストリにデバイスまたはデバイス セットアップ クラスのセキュリティ記述子を設定する方法の詳細については、次を参照してください。[レジストリにデバイス オブジェクト プロパティの設定](setting-device-object-properties-in-the-registry.md)します。

場合は、デバイスは、raw モードで運用される、PnP マネージャーは、デバイス オブジェクトのセキュリティ記述子を判断できません。 この場合は、バス ドライバーが; のセキュリティ記述子を指定する必要があります。以下をご覧ください。

### <a name="controlling-device-access-for-wdm-bus-drivers"></a>WDM バス ドライバーのデバイスへのアクセスを制御します。

WDM バス ドライバーでは、raw モードで操作できるすべてのデバイスの PDO のセキュリティ記述子を提供する必要があります。 使用[ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)セキュリティ記述子を持つデバイス オブジェクトを作成します。

バス ドライバーが raw モードでのデバイスを動作しない場合は、セキュリティ記述子を指定する必要はありません。 PnP マネージャーでは、前述のように、セキュリティ記述子が決定します。 場合は、Pdo のより厳密なセキュリティ設定の既定の記述子であることを確認する必要があります、バス ドライバーでは、セキュリティ記述子を指定できます。 バス ドライバーで指定された任意の記述子は、レジストリの設定によってオーバーライドされます。

デバイス オブジェクトの作成方法の詳細については、次を参照してください。[デバイス オブジェクトを作成する](creating-a-device-object.md)します。

### <a name="controlling-device-access-for-non-wdm-drivers"></a>非 WDM ドライバーのデバイスへのアクセスを制御します。

非 WDM ドライバーには、既定のセキュリティ記述子とクラス GUID を作成する任意の名前付きのデバイス オブジェクトを指定する必要があります。

使用して、 **IoCreateDeviceSecure**ルーチン名前付きのデバイス オブジェクトを作成して、既定のセキュリティ記述子を指定し、そのデバイス クラス GUID をします。 セキュリティ記述子は、サブセットの SDDL で指定されます。 詳細については、次を参照してください。[デバイス オブジェクトの SDDL](sddl-for-device-objects.md)します。

システムでは、既定のセキュリティ記述子で指定されたクラス GUID のレジストリのセキュリティ設定をオーバーライドします。 ドライバーは、デバイスの独自の一意の GUID を指定する必要があります。 GuidGen ツールを使用すると、一意の GUID を生成できます。 (GuidGen は、Microsoft Windows SDK に含まれます)。

 

 




