---
title: コネクションレス ミニポート ドライバーの情報の設定
description: コネクションレス ミニポート ドライバーの情報の設定
ms.assetid: 406d844a-cc83-4cd6-a2d2-78e614aab900
keywords:
- コネクションレス ドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b67eba5962b1b688da35ef22f167b84565dba4a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578077"
---
# <a name="setting-information-for-a-connectionless-miniport-driver"></a>コネクションレス ミニポート ドライバーの情報の設定





バインドされているプロトコルを呼び出すコネクションレス ミニポート ドライバーを保持する OID を設定する[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)渡します、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造を照会して、オブジェクトを設定する必要があります値を格納しているバッファーを指すオブジェクト (OID) を指定します。 呼び出し**NdisOidRequest** NDIS ミニポート ドライバーを呼び出すと、 [ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数で、指定された値を持つオブジェクトを設定します。

呼び出し*MiniportOidRequest*同期または非同期で完了できます。 ミニポート ドライバーを呼び出し、呼び出しを非同期的に完了する[ **NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)します。 次の図は、(バインド) ごとのコネクションレス ミニポート ドライバーでの設定情報を示します。

![(バインド) ごとのコネクションレス ミニポート ドライバーでの設定情報を示す図](images/fig5-4.png)

 

 





