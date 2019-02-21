---
title: GetPresharedKeyForId
description: GetPresharedKeyForId
ms.assetid: cd83d1dc-7aa8-4514-a108-50aee91d272b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d86bdb59a5f3fce3b826d1e86eda5dfd57adba4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535540"
---
# <a name="getpresharedkeyforid"></a>GetPresharedKeyForId


**GetPresharedKeyForId**メソッド レポート インターネット キー交換の特定のイニシエーター識別子 (IKE) id ペイロードでかどうか (事前共有キーを使用する ID を構成します。

イニシエーター識別子で、キーを関連付けるし、識別パケットのデータ部分でターゲットに、識別子と関連付けられたキーを渡しますイニシエーターは、キー交換で事前共有キーを使用する場合 (とも呼ばれる、 *id ペイロード*)。 イニシエーター渡します、識別子と関連付けられたキーのアグレッシブなまたはメイン モードの IKE フェーズ 1」の説明に従って[RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)します。 Id ペイロードは、安全な方法でイニシエーターを識別するために、その特定の発信側との接続に適したセキュリティ ポリシーを選択するターゲットを許可します。

ただし、すべて認証のネゴシエーションでは、事前共有キーが使用されます。 **GetPresharedKeyForId**メソッドにより、ユーザー モード サービスまたは管理アプリケーションを事前共有キーを持つ特定の識別子の IKE id ペイロードが構成されているかどうかを判断します。

この WMI メソッドは、パブリッシュされていないに属する[MSiSCSI\_SecurityConfigOperations WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)します。 パラメーターの説明については、 **GetPresharedKeyForId**メソッドのメンバーの説明を参照してください、 [ **GetPresharedKeyForId\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff554973)と[ **GetPresharedKeyForId\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff554975)構造体。

 

 





