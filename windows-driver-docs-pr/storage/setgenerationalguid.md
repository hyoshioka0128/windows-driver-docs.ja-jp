---
title: SetGenerationalGuid
description: SetGenerationalGuid
ms.assetid: cf8e57e5-afdf-4bc2-9849-5df3fbbdd6c5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ceffd229204dfacd5d21179e3a38ad6b3cb30bd7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838028"
---
# <a name="setgenerationalguid"></a>SetGenerationalGuid


**SetGenerationalGuid**メソッドは、イニシエーター HBA のキャッシュ内の情報に新しい GUID 値を割り当てます。

多くの場合、イニシエーター Hba は、特定のイニシエーター識別子に関連付けられている事前共有キーなどの認証情報、キーを持たないイニシエーター識別子に関連付けられているグループキー、および CHAP シークレットをキャッシュします。 イニシエーターは、現在キャッシュに格納されている情報のバージョンを識別する GUID を保持します。

ISCSI discovery サービスや、イニシエーターのキャッシュされた情報を更新する管理アプリケーションなどのサービスは、キャッシュが変更されたことを示すためにこの GUID を変更する必要があります。 ISCSI サービスまたは管理アプリケーションを再起動すると、イニシエーター HBA の GUID を確認して、キャッシュされた情報がイニシエーターのキャッシュされた情報と同期されていることを確認できます。

アプリケーションとサービスは、次の iSCSI WMI メソッドを使用して、イニシエーターのキャッシュされた構成データを管理できます。

[ClearCache](clearcache.md)

[GetPresharedKeyForId](getpresharedkeyforid.md)

[SetGroupPresharedKey](setgrouppresharedkey.md)

[SetPresharedKeyForId](setpresharedkeyforid.md)

[SetTunnelModeOuterAddress](settunnelmodeouteraddress.md)

**SetGenerationalGuid**メソッドは、発行されていない[Msiscsi\_SECURITYCONFIGOPERATIONS WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)に属しています。 **SetGenerationalGuid**メソッドのパラメーターの説明については、「」および「 [**SetGenerationalGuid\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setgenerationalguid_out)構造体」の「メンバーの[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setgenerationalguid_in)説明」を参照してください。 MSiSCSI\_SecurityConfigOperations WMI クラスを実装するミニポートドライバーは、HBA で情報がキャッシュされている場合、このメソッドをサポートする必要があります。

 

 





