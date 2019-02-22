---
title: WDI TLV 以外のバージョン管理
description: このセクションでは、WDI TLV 以外のバージョン管理を説明します。
ms.assetid: 19B5BEE1-BE17-40E3-99FA-D9BF4492D020
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f20fcb50c29d382567b79765e70bb631a90f483
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532724"
---
# <a name="wdi-non-tlv-versioning"></a>WDI TLV 以外のバージョン管理


WDI および IHV ミニポート間で渡され、含まれているデータ構造を[ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588) (など[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://msdn.microsoft.com/library/windows/hardware/mt297617)) 標準の NDIS バージョン管理モデルに従います。 ミニポートを確認する必要があります、**リビジョン**と**サイズ**フィールドを関連するフィールドが存在することを確認し、余分なフィールドやエラーのないデータを無視します。 新しいバージョンまたはより大きなこのような構造のサイズが除外されていないことを確認します。

せず、すべてのデータ構造、 [ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588) (など[ **WDI\_フレーム\_メタデータ**](https://msdn.microsoft.com/library/windows/hardware/dn897827)) WDI およびミニポートが低い方によって決まりますサイズ/リビジョン使用して、TLV バージョン管理モデルに従ってください**WdiVersion**値から[ **NDIS\_WDI\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/mt297621)と[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://msdn.microsoft.com/library/windows/hardware/mt297617).

たとえば、WDI 設定**WdiVersion**で[ **NDIS\_WDI\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/mt297621)に**WDI\_バージョン\_1\_0**、およびミニポート セット**WdiVersion**で[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://msdn.microsoft.com/library/windows/hardware/mt297617)に**WDI\_バージョン\_2\_0**、WDI およびミニポートの両方が、構造体のサイズを使用する必要があり、定義と互換性のある**WDI\_バージョン\_1\_0**ことがなくすべての構造体[ **NDIS\_オブジェクト\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566588)フィールド。 ただし、同じ状況が構造体を持つ、 **NDIS\_オブジェクト\_ヘッダー**フィールド、WDI およびミニポート限り大きくまたは新しい構造体を使用できます、**リビジョン**と**サイズ**フィールドが正しく設定されています。

 

 





