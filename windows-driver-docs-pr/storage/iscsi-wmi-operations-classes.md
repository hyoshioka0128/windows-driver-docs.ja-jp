---
title: iSCSI の操作の WMI クラス
description: iSCSI の操作の WMI クラス
ms.assetid: de8b31f8-e5dc-4ac0-8bd4-6912868310a0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 71698517b723b0a01eed4ac533443250a6dd7620
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560484"
---
# <a name="iscsi-wmi-operations-classes"></a>iSCSI の操作の WMI クラス


## <span id="ddk_iscsi_wmi_classes_that_define_the_interface_between_the_iscsi_disc"></span><span id="DDK_ISCSI_WMI_CLASSES_THAT_DEFINE_THE_INTERFACE_BETWEEN_THE_ISCSI_DISC"></span>


ISCSI 操作のクラスは、iSCSI イニシエーター サービスが iSCSI イニシエーターとの通信に使用する内部、非公開の WMI クラスです。 ストレージ ミニポート ドライバーでは、iSCSI 検出ライブラリとの通信にこれらのクラスを実装する必要があります。 ミニポート ドライバーでこれらのクラスをサポートするために必要なものの詳細については、クラスに関連付けられている構造のリファレンス ページを参照してください。 これらの構造が定義されている*Iscsiop.h*します。

ISCSI の操作クラスは、ユーザー モードの WMI スキーマの一部ではないと、WMI 管理アプリケーションは、直接のメソッドを呼び出そうとする必要があります。

イニシエーターのミニポート ドライバーでは、次の WMI ツール クラスをサポートする必要があります。

[ISCSI\_永続的な\_Login WMI クラス](iscsi-persistent-login-wmi-class.md)

[MSiSCSI\_AdapterEvent WMI クラス](msiscsi-adapterevent-wmi-class.md)

[MSiSCSI\_BootInformation WMI クラス](msiscsi-bootinformation-wmi-class.md)

[MSiSCSI\_LUNMappingInformation WMI クラス](msiscsi-lunmappinginformation-wmi-class.md)

[MSiSCSI\_操作 WMI クラス](msiscsi-operations-wmi-class.md)

[MSiSCSI\_PersistentLogins WMI クラス](msiscsi-persistentlogins-wmi-class.md)

[MSiSCSI\_SecurityConfigOperations WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)

[MSiSCSI\_TargetMappings WMI クラス](msiscsi-targetmappings-wmi-class.md)

 

 





