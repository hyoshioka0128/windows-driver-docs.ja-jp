---
title: 接続指向ミニポート ドライバーの情報の設定
description: 接続指向ミニポート ドライバーの情報の設定
ms.assetid: e31d2054-5982-4ba5-a9e9-133c0d4ed875
keywords:
- 接続指向のドライバー WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2868e950c1d4ed4f4a1234638189144cbad9ed5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572105"
---
# <a name="setting-information-for-a-connection-oriented-miniport-driver"></a>接続指向ミニポート ドライバーの情報の設定





バインドされているプロトコルを呼び出し、接続指向のミニポート ドライバーを保持する OID を設定する[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)渡します、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造を照会して、オブジェクトを設定する必要があります値を格納しているバッファーを指すオブジェクト (OID) を指定します。 呼び出し**NdisCoOidRequest** NDIS ミニポート ドライバーを呼び出すと、 [ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)関数で、指定された値を持つオブジェクトを設定します。

呼び出し**NdisCoOidRequest**同期または非同期で完了できます。 ミニポート ドライバーを呼び出し、呼び出しを非同期的に完了する[ **NdisCoOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561716)します。 次の図は、接続指向のミニポート ドライバーの設定情報を示します。

![接続指向のミニポート ドライバーの設定情報を示す図](images/fig5-3.png)

 

 





