---
title: MSiSCSI\_SecurityConfigOperations WMI クラス
description: MSiSCSI\_SecurityConfigOperations WMI クラス
ms.assetid: 27056bae-ba73-409f-b55e-453ed46a61d2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 19e6e2cb79b5b218e1b90cb0046aff755f685e10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559285"
---
# <a name="msiscsisecurityconfigoperations-wmi-class"></a>MSiSCSI\_SecurityConfigOperations WMI クラス


## <span id="ddk_msiscsi_securityconfigoperations_wmi_class_kr"></span><span id="DDK_MSISCSI_SECURITYCONFIGOPERATIONS_WMI_CLASS_KR"></span>


MSiSCSI\_SecurityConfigOperations WMI クラスのセキュリティ構成メソッドを定義しますかインターネット プロトコル セキュリティ (IPsec) をサポートしたり、チャレンジ ハンドシェイク認証プロトコル (CHAP) イニシエーターを実装する必要があります。

さらに、事前共有キーを持つインターネット キー交換 (IKE) をサポートするイニシエーターは、次のメソッドを実装する必要があります。

-   [SetPresharedKeyForId](setpresharedkeyforid.md)

-   [GetPresharedKeyForId](getpresharedkeyforid.md)

-   [SetGroupPresharedKey](setgrouppresharedkey.md)

イニシエーターの IPsec の事前共有キーと iSCSI の認証資格情報 (つまり、ユーザー名とパスワード) を実装する必要があります、不揮発性のキャッシュをサポートする、 [ClearCache](clearcache.md)メソッド。 イニシエーターがで適切なフラグを設定してキャッシュを使用することを示す必要がありますも、 [MSiSCSI\_HBAInformation WMI クラス](msiscsi-hbainformation-wmi-class.md)します。 具体的には、イニシエーターが事前共有キーをキャッシュする場合にする必要があります設定 ISCSI\_HBA\_PRESHARED\_キー\_キャッシュ フラグ、 **FunctionalitySupported**クラスのメンバーISCSI を設定する必要があります、イニシエーターが iSCSI 認証データをキャッシュする場合と\_HBA\_ISCSI\_認証\_キャッシュ フラグ。

MSiSCSI\_SecurityConfigOperations クラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付け、ミニポート ドライバーは、特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要がありますミニポートドライバーを管理します。

イニシエーターが iSCSI 探索サービスと互換性があるには、それを実装する必要があります、 [SetGenerationalGuid](setgenerationalguid.md)メソッド。

メソッドのリファレンス ページは、このクラスに属している各メソッドの管理オブジェクト フォーマット (MOF) 構文を説明します。 次のトピックでは、これらのメソッドとそれらに付随する構造体について説明します。

[ClearCache](clearcache.md)

[GetPresharedKeyForId](getpresharedkeyforid.md)

[SetGenerationalGuid](setgenerationalguid.md)

[SetGroupPresharedKey](setgrouppresharedkey.md)

[SetPresharedKeyForId](setpresharedkeyforid.md)

[SetTunnelModeOuterAddress](settunnelmodeouteraddress.md)

 

 





