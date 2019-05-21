---
title: WIA_IPS_BLANK_PAGES_SENSITIVITY
description: WIA_IPS_BLANK_PAGES_SENSITIVITY プロパティを使用して、デバイスでサポートされている最低と最高の感度下位または上位の値を空白のページ検出のトリガーを変更できます。
keywords:
- WIA_IPS_BLANK_PAGES_SENSITIVITY イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_BLANK_PAGES_SENSITIVITY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3d4c904d592713d7f398ef7c7c4ce458d70f9bc6
ms.sourcegitcommit: 2ddaca0dbaf96076ad54d39ac1e77d91e644de67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65958682"
---
# <a name="wiaipsblankpagessensitivity"></a>WIA\_IP\_空白\_ページ\_と小文字の区別

**WIA\_IP\_空白\_ページ\_感度**最低と最高の感度下位または上位の値を空白のページ検出のトリガーを変更するプロパティを使用デバイスでサポートされています。

WIA ミニ ドライバーごとに個別の秘密度値を使用できます内部的に[ **WIA\_IPA\_データ\_型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)と[ **WIA\_IPA\_深さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)色モードの組み合わせをサポートします。

このプロパティは初期化され、WIA ミニ ドライバーによって維持されます。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

## <a name="remarks"></a>注釈

このプロパティは省略可能で、フィーダー項目に対してのみ有効です (WIA\_カテゴリ\_フィーダー) 場合にのみ、 [ **WIA\_IP\_空白\_ページ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-blank-pages)に少なくとも 1 つの別の値よりもサポートされて**WIA\_空白\_ページ\_検出\_無効**します。

## <a name="requirements"></a>必要条件

| &nbsp; | &nbsp; |
| --- |:--- |
| **ヘッダー** | Wiadef.h (Wiadef.h を含む) |
