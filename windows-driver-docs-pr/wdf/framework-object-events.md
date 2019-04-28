---
title: フレームワーク オブジェクトのイベント
description: フレームワーク オブジェクトのイベント
ms.assetid: 1bccdd47-8ad6-4607-947f-18c5d2e03038
keywords:
- framework オブジェクト WDK KMDF、イベント
- WDK KMDF イベント
- WDK KMDF、framework のオブジェクトのイベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 691ce0769e5cf35364a5e453ce02f4b2ed0326b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370993"
---
# <a name="framework-object-events"></a>フレームワーク オブジェクトのイベント





一部のフレームワーク オブジェクトには、イベントを生成できます。 フレームワーク ベースのドライバーは、すべての通知を受信登録できます some、またはオブジェクトのイベントのいずれもします。 イベントを登録するには、ドライバーは、イベントのコールバック関数を提供します。 フレームワークは、イベントの発生時に、コールバック関数を呼び出します。

たとえば、ドライバーが登録できる、 [ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757) I/O キューのコールバック関数。 フレームワークによりはこのコールバック関数は、framework が I/O キューから、I/O 要求を削除し、ドライバーに配信するたびに呼び出します。

 

 





