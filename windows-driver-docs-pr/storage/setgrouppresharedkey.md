---
title: SetGroupPresharedKey
description: SetGroupPresharedKey
ms.assetid: 7dedcc62-4ad6-42d5-a461-b0a69c9c97cd
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ee495d2f460678762b628b9f65596f684b5ed326
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838025"
---
# <a name="setgrouppresharedkey"></a>SetGroupPresharedKey


**Setgrouppresharedkey**メソッドを使用すると、管理アプリケーションは、指定された事前共有キーを使用するようにイニシエーター HBA を構成できますが、セッションの識別子 (id) に現在関連付けられているキーはありません。

イニシエーターがキー交換で事前共有キーを使用すると、キーがイニシエーターの識別子に関連付けられ、識別子とそれに関連付けられたキーが識別パケットのデータ部分 (id とも呼ばれます) のターゲットに渡されます。 *ペイロード*)。 発信側は、 [RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)で説明されているように、アグレッシブまたはメインモードのインターネットキー交換 (IKE) のフェーズ1で、識別子とそれに関連付けられているキーを渡します。 Id ペイロードでは、ターゲットがセキュリティで保護された方法でイニシエーターを識別し、特定のイニシエーターとの接続に適したセキュリティポリシーを選択できます。

**Setgrouppresharedkey**メソッドは、既にキーに関連付けられていない識別子に既定の事前共有キーを使用するようにイニシエーターを構成します。 キーと特定のイニシエーター識別子の間の明示的な関連付けを確立するには、管理アプリケーションで[Setpresharedkeyforid](setpresharedkeyforid.md)メソッドを呼び出す必要があります。 識別子とキーの間に明示的なアソシエーションが存在する場合、アソシエーションが既定のキーよりも優先されるキー。

**Setgrouppresharedkey**メソッドで既定のキーを指定した後、不揮発性ストレージが使用可能な場合、イニシエーターはこのキーを不揮発性ストレージに格納する必要があります。 ただし、イニシエーターはキーを作業メモリに保持する必要があります。これにより、IKE フェーズ1のネゴシエーション中にすぐに使用できるようになります。 これにより、キー交換の効率が向上します。

**Setgrouppresharedkey**は、発行されていない[Msiscsi\_SECURITYCONFIGOPERATIONS WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)に属しています。 **Setgrouppresharedkey**メソッドのパラメーターの説明については、「 [ **」の setgrouppresharedkey\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setgrouppresharedkey_in) 、および[**setgrouppresharedkey\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setgrouppresharedkey_out)構造体のメンバーの説明を参照してください。

MSiSCSI\_SecurityConfigOperations WMI クラスを実装するミニポートドライバーは、 **Setgrouppresharedkey**をサポートしている必要があります。

 

 





