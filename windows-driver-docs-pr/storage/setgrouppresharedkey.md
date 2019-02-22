---
title: SetGroupPresharedKey
description: SetGroupPresharedKey
ms.assetid: 7dedcc62-4ad6-42d5-a461-b0a69c9c97cd
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1e357d03f819bdc5d10c6ac35c6e645749d272cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549690"
---
# <a name="setgrouppresharedkey"></a>SetGroupPresharedKey


**SetGroupPresharedKey**メソッドは、キーが必要ですが、セッションの識別子 (ID) と現在関連付けられているキーがないときに、指定された事前共有キーを使用する HBA イニシエーターを構成する管理アプリケーションを使用します。

イニシエーター識別子で、キーを関連付けるし、識別パケットのデータ部分でターゲットに、識別子と関連付けられたキーを渡しますイニシエーターは、キー交換で事前共有キーを使用する場合 (とも呼ばれる、 *id ペイロード*)。 イニシエーター渡します、識別子と関連付けられたキーまたはメイン モードの積極的なインターネット キー交換 (IKE) の第 1 フェーズ中に」の説明に従って[RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)します。 Id ペイロードは、安全な方法でイニシエーターを識別するために、その特定の発信側との接続に適したセキュリティ ポリシーを選択するターゲットを許可します。

**SetGroupPresharedKey**メソッドは、キーに関連付けられていない識別子の既定の事前共有キーを使用するイニシエーターを構成します。 管理アプリケーションを呼び出す必要があります、キーと、特定のイニシエーター id 間の明示的な関連付けを確立するために、 [SetPresharedKeyForId](setpresharedkeyforid.md)メソッド。 場合は、識別子と、キー、キーのあるアソシエーションよりも優先、既定のキーの間の明示的な関連付けが存在します。

後に、 **SetGroupPresharedKey**メソッドは、既定のキーを指定します、イニシエーターは、不揮発性記憶域が使用可能な場合に、不揮発性記憶域でのこのキーを格納する必要があります。 ただし、発信側も、IKE フェーズ 1 のネゴシエーション中にすばやく使用をすることができるように、作業メモリにキーを保持する必要があります。 これにより、キー交換の効率が向上します。

**SetGroupPresharedKey** 、パブリッシュされていないに属している[MSiSCSI\_SecurityConfigOperations WMI クラス](msiscsi-securityconfigoperations-wmi-class.md)します。 パラメーターの説明については、 **SetGroupPresharedKey**メソッドのメンバーの説明を参照してください、 [ **SetGroupPresharedKey\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565695)と[ **SetGroupPresharedKey\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565697)構造体。

ミニポート ドライバー、MSiSCSI を実装する\_SecurityConfigOperations WMI クラスをサポートする必要があります**SetGroupPresharedKey**します。

 

 





