---
title: WDI_TLV_OFFLOAD_SCOPE
description: WDI_TLV_OFFLOAD_SCOPE は、Rx を含む TLV coalesce オフロード機能です。
ms.assetid: 2E00659F-4A41-4907-AEA6-92EAFBFF2149
ms.date: 10/05/2017
keywords:
- WDI_TLV_OFFLOAD_SCOPE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 62fde916cdec2dd2a9041c67461e7a3f8f8531a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385257"
---
# <a name="wditlvoffloadscope"></a>WDI_TLV_OFFLOAD_SCOPE


WDI_TLV_OFFLOAD_SCOPE は、ネットワークのスコープを含む TLV の負荷を軽減します。

## <a name="tlv-type"></a>TLV 型


0x143

## <a name="length"></a>長さ


サイズ (バイト単位) で、以下の値。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT8 | チェックサム オフロード パラメーターがすべてのポートに適用できるかどうかを指定します。 <p>設定可能な値:</p> <ul><li>0:該当なし</li><li>1:適用できます</li></ul> |
| UINT8 | すべてのポートで LsoV1 オフロード パラメーターが該当するかどうかを指定します。 <p>設定可能な値:</p> <ul><li>0:該当なし</li><li>1:適用できます</li></ul> |
| UINT8 | すべてのポートで LsoV2 オフロード パラメーターが該当するかどうかを指定します。 <p>設定可能な値:</p> <ul><li>0:該当なし</li><li>1:適用できます</li></ul> |
| UINT8 | RSC オフロード パラメーターがすべてのポートに適用できるかどうかを指定します。 <p>設定可能な値:</p> <ul><li>0:該当なし</li><li>1:適用できます</li></ul> |
 

## <a name="requirements"></a>要件

| | |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1709 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |



