---
title: バージョン管理されたインターフェイス
description: バージョン管理されたインターフェイス
ms.assetid: 9512bfff-9225-45a3-b8c3-73469a1fe870
keywords:
- NDIS WDK、バージョン管理
- WDK ネットワークのバージョン管理
- NDIS WDK、旧バージョンとの互換性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed40ae34f3075cdc73661ada8d43e8aec212c778
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842955"
---
# <a name="versioned-interfaces"></a>バージョン管理されたインターフェイス





NDIS 6.0 では、キー構造のバージョン管理がサポートされています。 また、以前の多くの関数パラメーターは構造体に移動されます。 関数のパラメーターをバージョン付きの構造に移動すると、関数のインターフェイスを変更することなく、以降のバージョンの NDIS で関数のパラメーターを変更できるようになります。

バージョン付き構造体には、構造体のバージョンを指定するヘッダーが含まれています。 関数パラメーターまたはその他の構造体メンバーのセットが変更されると、構造体とそのバージョンが更新されます。

このバージョン管理により、下位互換性が簡略化され、NDIS 6.0 以降のドライバーの有効期間が延長されます。 また、NDIS ドライバーでは、複数のバージョンの NDIS をサポートできます。

詳細については、「 [**NDIS\_オブジェクト\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)」を参照してください。

 

 





