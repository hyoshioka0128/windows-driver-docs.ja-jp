---
title: SetPresharedKeyForId
description: SetPresharedKeyForId
ms.assetid: d966fd05-31ac-4774-b970-e4ce3d02a5ba
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0b42a5f4e8f341aead0928483e68a6542e179f14
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842430"
---
# <a name="setpresharedkeyforid"></a>SetPresharedKeyForId


**Setpresharedkeyforid**メソッドを使用すると、管理アプリケーションは特定の事前共有キーを ID (id) に関連付けることができます。この識別子は、発信側がアグレッシブまたはメインモードのインターネットキー交換 (IKE) のフェーズ1で自身を識別するために使用します。

イニシエーターがキー交換で事前共有キーを使用すると、キーがイニシエーターの識別子 (および IP アドレス) に関連付けられ、識別子とそれに関連付けられたキーが、id パケットのデータ部分のターゲットに渡されます (これは、id とも呼ばれます)。0 > 識別ペイロード)。 発信側は、 [RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)で説明されているように、アグレッシブまたはメインモードの IKE のフェーズ1で、識別子とそれに関連付けられているキーを渡します。 Id ペイロードでは、ターゲットがセキュリティで保護された方法でイニシエーターを識別し、特定のイニシエーターとの接続に適したセキュリティポリシーを選択できます。

**Setpresharedkeyforid**メソッドで事前共有キーを指定した後、不揮発性ストレージが使用可能な場合、イニシエーターは不揮発性ストレージにそのキーを格納する必要があります。 ただし、イニシエーターは、IKE フェーズ1のネゴシエーション中に迅速に使用できるように、作業メモリに事前共有キーを保持する必要もあります。 これにより、キー交換の効率が向上します。 不揮発性メモリをイニシエーターが使用できない場合、イニシエーターサービスは、イニシエーターに代わってキーを格納します。

管理アプリケーションは、 **Setpresharedkeyforid**メソッドを使用して、事前共有キーと特定のイニシエーター識別子を関連付けることができます。 既定のキーをすべてのイニシエーターの識別子に関連付けるために、アプリケーションは[Setgrouppresharedkey](setgrouppresharedkey.md)メソッドを呼び出すことができます。 識別子とキーの間に明示的なアソシエーションが存在する場合は、明示的な関連付けによって指定されたキーが既定のキーよりも優先されます。

**Setpresharedkeyforid**は、発行されていない[Msiscsi\_SECURITYCONFIGOPERATIONS WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)に属しています。 **Setpresharedkeyforid**メソッドのパラメーターの説明については、「 [ **」の setpresharedkeyforid\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setpresharedkeyforid_in)と[**setpresharedkeyforid\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setpresharedkeyforid_out)構造体のメンバーの説明を参照してください。

MSiSCSI\_SecurityConfigOperations WMI クラスを実装するミニポートドライバーは、 **Setpresharedkeyforid**をサポートしている必要があります。

 

 





