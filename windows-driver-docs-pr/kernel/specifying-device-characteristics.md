---
title: デバイスの特性の指定
description: デバイスの特性の指定
ms.assetid: 8b73ed62-d611-4515-b9d0-8e0a37555a1a
keywords:
- デバイス オブジェクトの WDK カーネル、デバイスの特性
- デバイスの特性 WDK デバイス オブジェクト
- WDK のデバイス オブジェクトのフラグ
- デバイス履歴の WDK カーネル、デバイスの特性
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b19d5cb4f7f61d73ee556ad352b2b46503291f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383005"
---
# <a name="specifying-device-characteristics"></a>デバイスの特性の指定





各デバイス オブジェクトには、1 つまたは複数のデバイスの特性を設定できます。 デバイスの特性が flags でフラグとして格納されている、**特性**デバイス オブジェクトのメンバー [**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)構造体。

ほとんどのドライバー ファイルのみを指定する\_デバイス\_SECURE\_特性を開きます。 これにより、デバイスの名前空間に同じセキュリティ設定が開いているすべての要求に適用されることができます。 詳細については、次を参照してください。[デバイス Namespace のアクセスを制御する](controlling-device-namespace-access.md)します。

ファイル\_自動生成された\_デバイス\_名は Pdo のみ使用します。 ファイル\_フロッピー\_フロッピー ディスク、ファイル\_リムーバブル\_メディア、およびファイル\_書き込み\_1 回\_メディアの特性は記憶域デバイスに固有です。 可能なデバイスの特性フラグの説明は、の説明を参照して、**特性**のメンバー [**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)します。

ファイルなど、特定のデバイスの特性\_自動生成された\_デバイス\_名、個々 のデバイス オブジェクトにのみ適用されます。 呼び出すことによって、デバイス オブジェクトを作成するとき、ドライバーは、デバイスの特性の個々 のデバイス オブジェクトの設定を指定できます[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)または[ **IoCreateDeviceSecure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)します。

次の特性は、デバイス全体のスタックに適用されます。

ファイル\_デバイス\_SECURE\_開く

ファイル\_フロッピー\_フロッピー ディスク

ファイル\_読み取り\_のみ\_デバイス

ファイル\_リムーバブル\_メディア

ファイル\_書き込み\_1 回\_メディア

ドライバーは、呼び出すことによって、デバイス全体のスタックに適用されるデバイスの特性を設定できる**IoCreateDevice**または**IoCreateDeviceSecure**します。 または、レジストリで、いずれかのデバイスまたはデバイスのセットアップ クラスに対するデバイス全体のスタックに適用されるデバイスの特性を設定できます。 (詳細については、次を参照してください[レジストリにデバイス オブジェクト プロパティの設定](setting-device-object-properties-in-the-registry.md)。)。

PnP マネージャーでは、次のように、デバイスの特性のレジストリ設定を決定します。

-   PnP マネージャーがその値を使用して個々 のデバイスの値を指定すると場合、

-   それ以外の場合、デバイス セットアップ クラスの値を指定すると場合、PnP マネージャーが使用する値です。

-   それ以外の場合、PnP マネージャーは、レジストリ設定としてゼロの値を使用します。

レジストリで、デバイス全体のスタックに適用されるデバイスの特性が設定されている場合、または任意 FDO に設定されているか、スタックのフィルターを行う場合は、し、PnP マネージャー設定、スタック内のすべてのデバイス オブジェクト。 (デバイスの場合*raw モード*対応、いないので、FDO PnP マネージャーが代わりに、PDO を使用しと)。

 

 




