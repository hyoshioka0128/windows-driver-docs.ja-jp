---
title: オフロード低電力のプロトコルの現在のパラメーター設定を取得します。
description: オフロード低電力のプロトコルの現在のパラメーター設定を取得します。
ms.assetid: 53d8535f-0615-4ba2-92f4-1c20a7d12c8d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 951a7a6ec544544a248b7684b2ede5eb7471f5be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536323"
---
# <a name="obtaining-the-current-parameter-settings-of-low-power-protocol-offloads"></a>オフロード低電力のプロトコルの現在のパラメーター設定を取得します。





プロトコル ドライバーを使用して[OID\_PM\_プロトコル\_オフロード\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff569769)ネットワーク アダプターでは、そのプロトコルがオフロードされているすべてのプロトコルの一覧を取得する OID クエリ。 で、クエリから正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、一覧へのポインター [ **NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)現在アクティブなプロトコルを記述する構造体の負荷を軽減します。 内容については、 **NDIS\_PM\_プロトコル\_オフロード**構造体は、「[の追加および削除する低電力プロトコルをオフロード](adding-and-deleting-low-power-protocol-offloads.md)します。

NDIS ハンドル[OID\_PM\_プロトコル\_オフロード\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff569769)OID と GUID\_PM\_プロトコル\_オフロード\_一覧 WMIミニポート ドライバーの代わりに要求します。 そのため、NDIS ミニポート ドライバーは、OID をサポートする必要はありません\_PM\_プロトコル\_オフロード\_一覧 OID 要求。

後続のドライバーを使用できます、 [OID\_PM\_取得\_プロトコル\_オフロード](https://msdn.microsoft.com/library/windows/hardware/ff569766)メソッド低電力プロトコル パラメーター設定を取得する OID のミニポート ドライバーから負荷を軽減します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体には最初にプロトコル オフロードへのポインターが含まれています識別子です。 メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 **NDIS\_OID\_要求**構造体にはへのポインターが含まれています、 [**NDIS\_PM\_プロトコル\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566760)構造体。

 

 





