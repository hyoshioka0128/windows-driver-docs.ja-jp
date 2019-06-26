---
title: サムネイル データの保存と転送
description: サムネイル データの保存と転送
ms.assetid: 4c27f93f-859e-42e3-95ea-9bfd8d0329d6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f335c71319863582f9477e1c619a075cfcc6217
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358239"
---
# <a name="storing-and-transferring-thumbnail-data"></a>サムネイル データの保存と転送





WIA サムネイルの情報は、3 つの WIA プロパティによって制御されます。[**WIA\_IPC\_サムネイル**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipc-thumbnail)、 [ **WIA\_IPC\_サムネイル\_幅**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipc-thumbnail-width)、および[ **WIA\_IPC\_サムネイル\_高さ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipc-thumbnail-height)します。 Windows Me で、Windows XP 以降で、サムネイルのデータは 24 ビット/ピクセルのみです。

<a href="" id="wia-ipc-thumbnail"></a>WIA\_IPC\_サムネイル  
プロパティは、RGB 形式、ピクセルあたり 24 ビットのサムネイルのデータを含む、32 ビットの境界にアラインされます。

<a href="" id="wia-ipc-thumb-width"></a>WIA\_IPC\_THUMB\_幅  
プロパティには、サムネイル画像の幅 (ピクセル単位) が含まれています。

<a href="" id="wia-ipc-thumbnail-height"></a>WIA\_IPC\_サムネイル\_高さ  
プロパティには、サムネイル イメージの高さ (ピクセル単位) が含まれています。

アプリケーションの読み取り、WIA\_IPC\_THUMB\_幅と WIA\_IPC\_THUMB\_高さのプロパティ (Microsoft で説明されているプロパティ BITMAPINFOHEADER 構造を作成するにはWindows SDK ドキュメント)。 その後、アプリケーションの読み取り、WIA\_IPC\_サムネイルの実際のデータのサムネイルのプロパティ。 サムネイルのデータは圧縮できません 24 ビットごとのピクセル データは、32 ビットの境界にアラインします。

 

 




