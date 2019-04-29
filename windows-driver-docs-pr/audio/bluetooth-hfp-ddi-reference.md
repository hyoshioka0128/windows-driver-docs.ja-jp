---
title: Bluetooth HFP DDI 参照
description: Windows 8 には、GUID が導入\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_ハンド フリーの I/O 制御コード (Ioctl) と構造体を実装するインターフェイスを持つ、HCIBYPASS クラスプロファイル (HFP) は、オーディオ ドライバーをバイパスします。
ms.assetid: 980B7283-56C5-44FA-8992-6DA5BE263FCD
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5bee5b4f82889094e99f97b2105345088562ab0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333887"
---
# <a name="bluetooth-hfp-ddi-reference"></a>Bluetooth HFP DDI 参照


Windows 8 には、GUID が導入\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_ハンド フリーの I/O 制御コード (Ioctl) と構造体を実装するインターフェイスを持つ、HCIBYPASS クラスプロファイル (HFP) は、オーディオ ドライバーをバイパスします。

ペアになっている Bluetooth デバイス、HFP で各 HFP は、ドライバーは、このクラスでインターフェイスを登録します。 インターフェイスが登録され、デバイスがペアリング後 HFP ドライバーが実行されているを有効になっています。 ドライバーを停止する場合、インターフェイスが無効になり、登録が解除されました。

Bluetooth コント ローラー上でバイパス オーディオ接続用のドライバーを開発する際に、ドライバーは、Bluetooth オーディオ サポートを完全に実装するためにこれらのインターフェイスを使用できます。 HFP デバイスでは、1 つのファイル オブジェクトのみを使う guid\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS デバイス インターフェイス。

次のトピックでは、構造と Ioctl このクラスに対して定義されているについて説明します。

[Bluetooth HFP DDI 構造体](bluetooth-hfp-ddi-structures.md)

[Bluetooth HFP DDI Ioctl](bluetooth-hfp-ddi-ioctls.md)

 

 





