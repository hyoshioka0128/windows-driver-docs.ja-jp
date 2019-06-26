---
title: SetGenerationalGuid
description: SetGenerationalGuid
ms.assetid: cf8e57e5-afdf-4bc2-9849-5df3fbbdd6c5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0c4f6288b8742f2e19357ef830bdb412b1ecdf5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384659"
---
# <a name="setgenerationalguid"></a>SetGenerationalGuid


**SetGenerationalGuid**メソッド新しい GUID 値に割り当てます、開始側の情報は、HBA のキャッシュ。

イニシエーターの Hba は、多くの場合、特定のイニシエーター id、キー、および CHAP シークレットがないイニシエーター id に既定で関連付けられているグループ キーに関連付けられている事前共有キーなどの認証情報をキャッシュします。 イニシエーターは、現在、キャッシュされている情報のバージョンを識別する GUID を保持します。

ISCSI の探索サービスと発信側のキャッシュされた情報を更新する管理アプリケーションなどのサービスでは、キャッシュが変更されたことを示すには、この GUID を変更しないでください。 ISCSI サービスまたは管理アプリケーションを再起動すると、発信側でキャッシュされた情報でそのキャッシュされた情報が同期されていることを確認するイニシエーター HBA の GUID を確認できます。

アプリケーションとサービスは、イニシエーターのキャッシュされた構成データを管理するのに次の iSCSI WMI メソッドを使用できます。

[ClearCache](clearcache.md)

[GetPresharedKeyForId](getpresharedkeyforid.md)

[SetGroupPresharedKey](setgrouppresharedkey.md)

[SetPresharedKeyForId](setpresharedkeyforid.md)

[SetTunnelModeOuterAddress](settunnelmodeouteraddress.md)

**SetGenerationalGuid**メソッドは、パブリッシュされていないに属する[MSiSCSI\_SecurityConfigOperations WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)します。 パラメーターの説明については、 **SetGenerationalGuid**メソッドのメンバーの説明を参照してください、 [ **SetGenerationalGuid\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_setgenerationalguid_in)と[**SetGenerationalGuid\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_setgenerationalguid_out)構造体。 ミニポート ドライバー、MSiSCSI を実装する\_SecurityConfigOperations WMI クラスが、HBA 情報をキャッシュする場合にこのメソッドをサポートする必要があります。

 

 





