---
title: WIA_IPS_MULTI_FEED_DETECT_METHOD
description: WIA_IPS_MULTI_FEED_DETECT_METHOD プロパティは、倍数フィードの条件を検出するために、デバイスによって使用される方法の構成に使用されます。
keywords:
- WIA_IPS_MULTI_FEED_DETECT_METHOD イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_MULTI_FEED_DETECT_METHOD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6f46c797489681e6de4a128c75da701ca79e301f
ms.sourcegitcommit: 2ddaca0dbaf96076ad54d39ac1e77d91e644de67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65958676"
---
# <a name="wiaipsmultifeeddetectmethod"></a>WIA\_IP\_マルチ\_フィード\_検出\_メソッド

**WIA\_IP\_マルチ\_フィード\_検出\_メソッド**プロパティは、複数のフィードの条件を検出するために、デバイスによって使用される方法を構成するために使用します。

このプロパティは初期化され、WIA ミニ ドライバーによって維持されます。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

## <a name="remarks"></a>注釈

このプロパティの有効な値は、次の表に表示されます。

| Value | 説明 |
| --- | --- |
| WIA_MULTI_FEED_DETECT_ METHOD_LENGTH | デバイスがスキャンされている元のページ サイズの長さで、スキャンしたページの長さを測定します。 |
| WIA_MULTI_FEED_DETECT_METHOD_OVERLAP | デバイスは、重複スキャンしたページを検出します。 |

ミニ ドライバーが別のセットをサポートできる[ **WIA\_IP\_マルチ\_フィード\_感度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-multi-feed-sensitivity)プロパティの値はそれぞれ**WIA\_IP\_マルチ\_フィード\_検出\_メソッド**プロパティの値。 ときに両方**WIA\_IP\_マルチ\_フィード\_検出\_メソッド**と**WIA\_IP\_マルチ\_フィード\_感度**プロパティがサポートされている、WIA アプリケーションを設定する必要があります最初、 **WIA\_IP\_マルチ\_フィード\_検出\_メソッド**プロパティを複数のフィードの検出方法を構成し、設定、 **WIA\_IP\_マルチ\_フィード\_感度**この検出方法の必要な区別を構成するプロパティです。

このプロパティは、フィーダー項目に対してのみ有効です (WIA\_カテゴリ\_フィーダー) は省略可能です。 プロパティがサポートされている場合、必要な既定値はありません。

## <a name="requirements"></a>必要条件

| &nbsp; | &nbsp; |
| --- |:--- |
| **ヘッダー** | Wiadef.h (Wiadef.h を含む) |
