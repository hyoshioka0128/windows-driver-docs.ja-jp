---
title: カーネルの COM
description: カーネルの COM
ms.assetid: 2ce13ef1-9868-4f6d-9c42-b71f9e3d5615
keywords:
- オーディオのミニポート ドライバー WDK、COM
- COM のミニポート ドライバー WDK オーディオ
- COM インターフェイスの WDK オーディオ
- IUnknown インターフェイス
- ポート クラス ドライバー WDK オーディオ
- PortCls WDK オーディオ、COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf62cac5151f7c102eb29a7f0252bdfe2c772100
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333879"
---
# <a name="com-in-the-kernel"></a>カーネルの COM


## <span id="com_in_the_kernel"></span><span id="COM_IN_THE_KERNEL"></span>


オーディオのポートおよびミニポート ドライバーでは、コンポーネント オブジェクト モデル (COM) に準拠するデバイス ドライバー インターフェイス (Ddi) をエクスポートします。 COM インターフェイスに関する背景情報は、Microsoft Windows SDK ドキュメントの [COM] セクションを参照してください。

すべての COM インターフェイスの継承、 **IUnknown**インターフェイス メソッドを**AddRef**、 **QueryInterface**、および**リリース**します。 これらのメソッドは、すべての COM インターフェイスに共通であるため、WDM オーディオ ドライバー インターフェイスのリファレンス ページに明示的には説明しませんに。

このセクションでは、次のトピックについて説明します。

[関数のテーブルなミニポート ドライバー](function-tables-for-miniport-drivers.md)

[オーディオ ドライバー オブジェクトを作成します。](creating-audio-driver-objects.md)

[COM オブジェクトの参照カウントの規則](reference-counting-conventions-for-com-objects.md)

 

 




