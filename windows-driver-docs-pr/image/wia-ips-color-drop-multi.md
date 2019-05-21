---
title: WIA_IPS_COLOR_DROP_MULTI
description: WIA_IPS_COLOR_DROP_MULTI プロパティは、同時に 1 つ以上の 1 つの色削除できるときに、レポートに使用されます。
keywords:
- WIA_IPS_COLOR_DROP_MULTI イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_COLOR_DROP_MULTI
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 54be1817c00b1d4338084efd1bb8f307f751793e
ms.sourcegitcommit: 2ddaca0dbaf96076ad54d39ac1e77d91e644de67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65958678"
---
# <a name="wiaipscolordropmulti"></a>WIA\_IP\_色\_ドロップ\_マルチ

**WIA\_IP\_色\_ドロップ\_マルチ**プロパティを使用して報告するときに 1 つ以上同時に 1 つの色削除できます。 たとえば、このプロパティの値が 2 の場合は、アプリケーション設定できます、 **WIA\_IP\_色\_ドロップ\_RED**、 **WIA\_IP\_色\_ドロップ\_緑**、および**WIA\_IP\_色\_青い**プロパティをそれぞれ 2 つの値を格納している列挙体削除する 2 つの色を記述します。

このプロパティは初期化され、WIA ミニ ドライバーによって維持されます。

プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

## <a name="remarks"></a>注釈

このプロパティは、フラット ベッドを含むすべてプログラミング可能なイメージのデータ ソース アイテムの有効な (WIA\_カテゴリ\_ベッド) とフィーダー (WIA\_カテゴリ\_フィーダー) 場合にのみ、 [ **WIA\_IP\_色\_ドロップ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-color-drop)プロパティがサポートされています。

## <a name="requirements"></a>要件

| &nbsp; | &nbsp; |
| --- |:--- |
| **ヘッダー** | Wiadef.h (Wiadef.h を含む) |
