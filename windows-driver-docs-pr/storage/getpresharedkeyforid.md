---
title: GetPresharedKeyForId
description: GetPresharedKeyForId
ms.assetid: cd83d1dc-7aa8-4514-a108-50aee91d272b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 489eee3ebee6454f80c0b0fd79ac30faa9412174
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837562"
---
# <a name="getpresharedkeyforid"></a>GetPresharedKeyForId


**Getpresharedkeyforid**メソッドは、特定のイニシエーター ID (ID が事前共有キーを使用するように構成されている) のインターネットキー交換 (IKE) 識別ペイロードを報告します。

イニシエーターがキー交換で事前共有キーを使用すると、キーがイニシエーターの識別子に関連付けられ、識別子とそれに関連付けられたキーが識別パケットのデータ部分 (id とも呼ばれます) のターゲットに渡されます。 *ペイロード*)。 発信側は、 [RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)で説明されているように、アグレッシブまたはメインモードの IKE のフェーズ1で、識別子とそれに関連付けられているキーを渡します。 Id ペイロードでは、ターゲットがセキュリティで保護された方法でイニシエーターを識別し、特定のイニシエーターとの接続に適したセキュリティポリシーを選択できます。

ただし、すべての認証ネゴシエーションで事前共有キーが使用されるわけではありません。 **Getpresharedkeyforid**メソッドを使用すると、ユーザーモードサービスまたは管理アプリケーションは、特定の識別子の IKE 識別ペイロードが事前共有キーで構成されているかどうかを判断できます。

この WMI メソッドは、発行されていない[Msiscsi\_SecurityConfigOperations WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)に属しています。 **Getpresharedkeyforid**メソッドのパラメーターの説明については、「 [ **」の getpresharedkeyforid\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_getpresharedkeyforid_in)と[**getpresharedkeyforid\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_getpresharedkeyforid_out)構造体のメンバーの説明を参照してください。

 

 





