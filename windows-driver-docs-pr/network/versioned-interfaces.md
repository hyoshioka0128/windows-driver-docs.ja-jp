---
title: バージョン管理されたインターフェイス
description: バージョン管理されたインターフェイス
ms.assetid: 9512bfff-9225-45a3-b8c3-73469a1fe870
keywords:
- NDIS WDK、バージョン管理
- バージョン管理の WDK ネットワーク
- NDIS WDK、旧バージョンとの互換性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc90c6a997221f1f254d1ddd8718582dfe5d627a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559110"
---
# <a name="versioned-interfaces"></a>バージョン管理されたインターフェイス





NDIS 6.0 では、構造のキーのバージョン管理をサポートしています。 また、多くの以前の関数のパラメーターは、構造体に移動されます。 バージョン管理された構造体を関数のパラメーターを移動すると、以降のバージョンの NDIS 関数インターフェイスを変更することがなく変更する関数のパラメーターができます。

バージョン管理された構造体には、構造体のバージョンを指定するヘッダーが含まれます。 関数パラメーターまたはその他の構造体のメンバーのセットを変更する場合は、構造とそのバージョンが更新されます。

このバージョン管理は、旧バージョンとの互換性を簡略化し、NDIS 6.0 とそれ以降のドライバーの有効期限を延長します。 また、NDIS ドライバーでは、NDIS の 1 つ以上のバージョンをサポートできます。

詳細については、[ **NDIS\_オブジェクト\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff566588)を参照してください。

 

 





