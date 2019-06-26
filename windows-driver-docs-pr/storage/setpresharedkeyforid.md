---
title: SetPresharedKeyForId
description: SetPresharedKeyForId
ms.assetid: d966fd05-31ac-4774-b970-e4ce3d02a5ba
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2baab8921ae1b1c04bf53f57d3c45281b0967695
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363965"
---
# <a name="setpresharedkeyforid"></a>SetPresharedKeyForId


**SetPresharedKeyForId**メソッドに特定の事前共有キーをイニシエーターを使用して、アグレッシブなまたはメイン モードのインターネット キーの第 1 フェーズ中に識別する識別子 (ID) に関連付ける管理アプリケーションを使用します。交換 (IKE)。

イニシエーター識別子 (および IP アドレスを含む)、キーに関連付けます、イニシエーターは、キー交換で事前共有キーを使用する場合、および識別パケットのデータ部分でターゲットに、識別子と関連付けられたキーを渡します (別名、「c0 >  *id ペイロード*)。 イニシエーター渡します、識別子と関連付けられたキーのアグレッシブなまたはメイン モードの IKE フェーズ 1」の説明に従って[RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)します。 Id ペイロードは、安全な方法でイニシエーターを識別するために、その特定の発信側との接続に適したセキュリティ ポリシーを選択するターゲットを許可します。

後に、 **SetPresharedKeyForId**メソッドは、事前共有キーを指定します。 イニシエーターする必要がありますに保存して、その不揮発性ストレージ不揮発性記憶域が使用可能な場合。 ただし、発信側も、IKE フェーズ 1 のネゴシエーション中にすばやく使用をすることができるように、作業メモリに事前共有キーを保持する必要があります。 これにより、キー交換の効率が向上します。 不揮発性メモリがイニシエーターを使用できない場合、発信側サービスはイニシエーター代わりにキーを格納します。

管理アプリケーションを使用できる、 **SetPresharedKeyForId**特定イニシエーター識別子と事前共有キーを関連付けるメソッド。 イニシエーターの識別子のすべての既定のキーを関連付ける、アプリケーションを呼び出すことができます、 [SetGroupPresharedKey](setgrouppresharedkey.md)メソッド。 識別子とキーの間の明示的な関連付けが存在する場合は、明示的な関連付けを指定するキーが、既定のキーよりも優先されます。

**SetPresharedKeyForId** 、パブリッシュされていないに属している[MSiSCSI\_SecurityConfigOperations WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)します。 パラメーターの説明については、 **SetPresharedKeyForId**メソッドのメンバーの説明を参照してください、 [ **SetPresharedKeyForId\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_setpresharedkeyforid_in)と[ **SetPresharedKeyForId\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_setpresharedkeyforid_out)構造体。

ミニポート ドライバー、MSiSCSI を実装する\_SecurityConfigOperations WMI クラスをサポートする必要があります**SetPresharedKeyForId**します。

 

 





