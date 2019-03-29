---
title: サムネイル データの保存と転送
description: サムネイル データの保存と転送
ms.assetid: 4c27f93f-859e-42e3-95ea-9bfd8d0329d6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8540474be5b15f301e73573472db93faccb9fefb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571470"
---
# <a name="storing-and-transferring-thumbnail-data"></a>サムネイル データの保存と転送





WIA サムネイルの情報は、3 つの WIA プロパティによって制御されます。[**WIA\_IPC\_サムネイル**](https://msdn.microsoft.com/library/windows/hardware/ff552550)、 [ **WIA\_IPC\_サムネイル\_幅**](https://msdn.microsoft.com/library/windows/hardware/ff552558)、および[ **WIA\_IPC\_サムネイル\_高さ**](https://msdn.microsoft.com/library/windows/hardware/ff552552)します。 Windows Me で、Windows XP 以降で、サムネイルのデータは 24 ビット/ピクセルのみです。

<a href="" id="wia-ipc-thumbnail"></a>WIA\_IPC\_サムネイル  
プロパティは、RGB 形式、ピクセルあたり 24 ビットのサムネイルのデータを含む、32 ビットの境界にアラインされます。

<a href="" id="wia-ipc-thumb-width"></a>WIA\_IPC\_THUMB\_幅  
プロパティには、サムネイル画像の幅 (ピクセル単位) が含まれています。

<a href="" id="wia-ipc-thumbnail-height"></a>WIA\_IPC\_サムネイル\_高さ  
プロパティには、サムネイル イメージの高さ (ピクセル単位) が含まれています。

アプリケーションの読み取り、WIA\_IPC\_THUMB\_幅と WIA\_IPC\_THUMB\_高さのプロパティ (Microsoft で説明されているプロパティ BITMAPINFOHEADER 構造を作成するにはWindows SDK ドキュメント)。 その後、アプリケーションの読み取り、WIA\_IPC\_サムネイルの実際のデータのサムネイルのプロパティ。 サムネイルのデータは圧縮できません 24 ビットごとのピクセル データは、32 ビットの境界にアラインします。

 

 




