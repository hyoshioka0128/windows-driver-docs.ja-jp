---
title: 現在のヘッダー データ分割構成の設定
description: 現在のヘッダー データ分割構成の設定
ms.assetid: b5b20ce8-1522-4729-8d0a-bc2d2c5afff2
keywords:
- ヘッダー データの分割 WDK、構成
- 現在のヘッダー データの分割 WDK ネットワークの構成
- ステータス情報 WDK ヘッダー以外のデータの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13c7b9060bdb950f2036363a83f4c3ace7fecd49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539371"
---
# <a name="setting-the-current-header-data-split-configuration"></a>現在のヘッダー データ分割構成の設定





NDIS と関連付けたドライバーまたはユーザー モード アプリケーションを使用して、 [OID\_GEN\_HD\_分割\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569587)現在のヘッダー データを設定する OID ミニポート アダプターの設定を分割します。 NDIS 6.1 と以降のミニポート ドライバー ヘッダー データの分割サービスを提供するには、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

システム管理者は、WMI インターフェイスを通じてこの OID に関連付けられている GUID を使用できます。 ヘッダー データの詳細については、WMI の Guid を分割するを参照してください。[ヘッダー データの分割のサポートを WMI](wmi-support-for-header-data-split.md)します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、 [ **NDIS\_HD\_分割\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565701)構造体。

場合は、NDIS\_HD\_分割\_結合\_すべて\_ヘッダー フラグ、 **HDSplitCombineFlags** NDIS のメンバー\_HD\_分割\_パラメーターの設定、ミニポート アダプターが分割のすべてのフレームを結合する必要があります。 ヘッダー データの分割が有効で、ハードウェアの場合、ミニポート ドライバーは必要ドライバー NDIS するフレームまで、ヘッダーとデータと組み合わせる必要があります。

たとえば、NDIS は可能性があります、OID を使用して\_GEN\_HD\_分割\_NDIS を設定するパラメーターの OID\_HD\_分割\_結合\_すべて\_ヘッダーは、ときに、NDIS 5 フラグです。*x*プロトコル ドライバーが 6.1 の NDIS ミニポート アダプターにバインドします。 ミニポート ドライバーに OID を渡し、ミニポート アダプターの更新前に、NDIS 処理この OID  **\*HeaderDataSplit**必要な場合は、キーワードを標準化します。 ヘッダー データの分割が無効になっている場合は、NDIS はミニポート アダプターにこの OID を送信しません。

 

 





