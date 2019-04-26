---
title: デインターレース用のデインターレース コンテナー デバイス
description: デインターレース用のデインターレース コンテナー デバイス
ms.assetid: e14db243-46e5-4ab3-b134-8aadfa99e614
keywords:
- コンテナーのデバイスの WDK DirectX VA インター レースを解除します。
- コンテナー デバイス WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 157b49a4e111a86084baff0668ed45c1b079e2b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348918"
---
# <a name="deinterlace-container-device-for-deinterlacing"></a>デインターレース用のデインターレース コンテナー デバイス


## <span id="ddk_deinterlace_container_device_for_deinterlacing_gg"></span><span id="DDK_DEINTERLACE_CONTAINER_DEVICE_FOR_DEINTERLACING_GG"></span>


[デインター レースの関数のサンプル](sample-functions-for-deinterlacing.md)のため、最初に定義し、インター コンテナー デバイスを作成する必要がありますのみ、DirectX VA デバイスのコンテキスト内に使用できます。

ドライバーでは、VMR によって開始されたときに、圧縮されたビデオの高速デコードをサポートする場合、ドライバーも 2 つの DirectX VA デバイスを作成します。 ビデオの作業とインター レース解除操作を実行する 1 つのデコードを実行する 1 つ。

**注**  インター コンテナー デバイスはソフトウェア コンス トラクターのみで、デバイス上に含まれている機能、ハードウェアを表していません。

 

 

 





