---
title: SetCHAPSharedSecret
description: SetCHAPSharedSecret
ms.assetid: d1f1d6f2-154e-4e41-8ebf-4071de4ceafe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e53529e1e7095f638e5c4f208d967324e617bcc2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845044"
---
# <a name="setchapsharedsecret"></a>SetCHAPSharedSecret


**SetCHAPSharedSecret**メソッドは、イニシエーターがイニシエーターのチャレンジに対するターゲットの応答を検証するときに使用する、イニシエーターの共有シークレットを確立します。

イニシエーターは、2つの異なる共有シークレットを使用してチャレンジハンドシェイク認証プロトコル (CHAP) を実装します。

-   **SetCHAPSharedSecret**メソッドは、イニシエーターがイニシエーターのチャレンジに対するターゲットの応答を確認するために使用する共有シークレットを確立します。

-   [Log、target](logintotarget.md)メソッドは、イニシエーターがターゲットのチャレンジへの CHAP 応答を生成するために使用する共有シークレットを確立します。

**SetCHAPSharedSecret** wmi メソッドは、発行されていない[Msiscsi\_Operations WMI クラス](msiscsi-operations-wmi-class.md)に属しています。 **SetCHAPSharedSecret**メソッドのパラメーターの説明については、「」および「 [**SetCHAPSharedSecret\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setchapsharedsecret_out)構造体」の「メンバーの[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setchapsharedsecret_in)説明」を参照してください。

MSiSCSI\_Operations WMI クラスを実装するミニポートドライバーは、 **SetCHAPSharedSecret**をサポートするためには必要ありません。

 

 





