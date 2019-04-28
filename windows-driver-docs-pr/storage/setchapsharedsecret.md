---
title: SetCHAPSharedSecret
description: SetCHAPSharedSecret
ms.assetid: d1f1d6f2-154e-4e41-8ebf-4071de4ceafe
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0f34130b17bfcd6a4f3434c538050b23717eca60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377212"
---
# <a name="setchapsharedsecret"></a>SetCHAPSharedSecret


**SetCHAPSharedSecret**メソッドは、共有シークレットをイニシエーターのチャレンジにターゲットの応答の確認に使用するイニシエーターを確立します。

イニシエーターは、チャレンジ ハンドシェイク認証プロトコル (CHAP) を実装するのに 2 つの異なる共有シークレットを使用します。

-   **SetCHAPSharedSecret**メソッドは、イニシエーターの課題に、ターゲットの応答を確認するイニシエーターを使用する共有シークレットを確立します。

-   [LoginToTarget](logintotarget.md)メソッドは、イニシエーターがターゲットのチャレンジに CHAP 応答の生成に使用する共有シークレットを確立します。

**SetCHAPSharedSecret** WMI メソッドは、パブリッシュされていないに属する[MSiSCSI\_操作 WMI クラス](msiscsi-operations-wmi-class.md)します。 パラメーターの説明については、 **SetCHAPSharedSecret**メソッドのメンバーの説明を参照してください、 [ **SetCHAPSharedSecret\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565595)と[**SetCHAPSharedSecret\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565600)構造体。

ミニポート ドライバー、MSiSCSI を実装する\_操作 WMI クラスがサポートする必要はありません**SetCHAPSharedSecret**します。

 

 





