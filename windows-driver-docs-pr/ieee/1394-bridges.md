---
title: 1394 ブリッジ
description: 1394 ブリッジ
ms.assetid: 208cceaa-dd26-46f9-b015-723c5940b02b
keywords:
- ブリッジの IEEE 1394 WDK バス
- 1394 WDK バス、ブリッジ
- ブリッジ WDK IEEE 1394 バス
- 1394 ブリッジ WDK IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8486fb5725f43b19db5761816d8b6be6f2947942
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376716"
---
# <a name="1394-bridges"></a>1394 ブリッジ





1394 基底スタック (*ohci1394.sys*と*1394bus.sys*) 1394 ブリッジ デバイスまたは複数の 1394 バス間のブリッジをサポートしません。 1394 ベース スタックが複数のバス番号を許可しないためにです。 バス番号 0x3FF バスのすべての操作を使用します。 これは、IEEE 1394 1995 仕様で定義されたローカル バス番号の場合、合意された標準です。

ブリッジでは、オペレーティング システムが正常に機能するために複数のバス番号をサポートすることが必要なため Microsoft は、ブリッジにアタッチされているデバイスが動作する保証はされません。

 

 




