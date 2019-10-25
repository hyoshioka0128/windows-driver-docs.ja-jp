---
title: デバイスの特性の指定
description: デバイスの特性の指定
ms.assetid: 8b73ed62-d611-4515-b9d0-8e0a37555a1a
keywords:
- デバイスオブジェクト WDK カーネル、デバイスの特性
- デバイス特性 (WDK デバイスオブジェクト)
- WDK デバイスオブジェクトにフラグをかける
- デバイススタック WDK カーネル、デバイスの特性
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: becb41a82fae8da5fb35dab78380fd0c183e8bcb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836293"
---
# <a name="specifying-device-characteristics"></a>デバイスの特性の指定





各デバイスオブジェクトは、1つまたは複数のデバイスの特性を持つことができます。 デバイスの特性は、デバイスオブジェクトの[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の**特性**メンバーにフラグとして格納されます。

ほとんどのドライバーでは、ファイル\_デバイス\_セキュリティで保護された\_オープン特性のみが指定されています。 これにより、デバイスの名前空間に対して、開いている要求に同じセキュリティ設定が適用されます。 詳細については、「[デバイスの名前空間へのアクセスの制御](controlling-device-namespace-access.md)」を参照してください。

デバイス\_名\_自動生成されたファイル\_は、PDOs にのみ使用されます。 ファイル\_フロッピー\_フロッピーディスク、ファイル\_リムーバブル\_メディア、ファイル\_書き込み\_、メディア特性は記憶装置に固有です。 使用可能なデバイス特性フラグの説明については、[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)の**特性**メンバーの説明を参照してください。

デバイス\_名\_自動生成されたファイル\_などの特定のデバイスの特性は、個々のデバイスオブジェクトにのみ適用されます。 ドライバーは、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)または[**iocreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)を呼び出すことによってデバイスオブジェクトを作成するときに、個々のデバイスオブジェクトのデバイス特性の設定を指定できます。

次の特性は、デバイススタック全体に適用されます。

ファイル\_デバイス\_セキュリティで保護された\_開く

フロッピー\_フロッピー\_ファイル

ファイル\_読み取り\_\_デバイスのみ

ファイル\_リムーバブル\_メディア

ファイル\_\_\_メディアに一度書き込み

ドライバーは、 **IoCreateDevice**または**iocreate**を呼び出すことによって、デバイススタック全体に適用されるデバイスの特性を設定できます。 または、デバイススタック全体に適用されるデバイスの特性を、デバイスまたはデバイスのセットアップクラスのレジストリに設定できます。 (詳細については、「[レジストリにデバイスオブジェクトプロパティを設定](setting-device-object-properties-in-the-registry.md)する」を参照してください)。

PnP マネージャーは、次のようにデバイスの特性のレジストリ設定を決定します。

-   個々のデバイスに値が指定されている場合、PnP マネージャーはその値を使用します。

-   それ以外の場合、デバイスセットアップクラスに値を指定すると、PnP マネージャーはその値を使用します。

-   それ以外の場合、PnP マネージャーはレジストリ設定として0の値を使用します。

デバイススタック全体に適用されるデバイスの特性がレジストリで設定されている場合、またはスタック内の FDO またはフィルターに設定されている場合は、PnP マネージャーによって、スタック内のすべてのデバイスオブジェクトに対して設定されます。 (デバイスが*raw モード*に対応していて、FDO がない場合は、代わりに、PnP マネージャーが PDO を使用します)。

 

 




