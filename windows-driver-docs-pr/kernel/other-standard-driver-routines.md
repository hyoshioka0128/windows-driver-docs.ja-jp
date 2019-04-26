---
title: その他の標準ドライバー ルーチン
description: その他の標準ドライバー ルーチン
ms.assetid: 3dada9cc-7239-47de-8940-bc4cef8be4ca
keywords:
- ドライバー オブジェクトの WDK カーネル
- 標準のドライバー ルーチン WDK カーネル ドライバー オブジェクト
- ドライバー ルーチン WDK カーネル ドライバー オブジェクト
- ルーチン WDK カーネル ドライバー オブジェクト
- WDK ドライバー オブジェクトのオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55176b65ea228ee474a8057cef082b8e10fdea1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352033"
---
# <a name="other-standard-driver-routines"></a>その他の標準ドライバー ルーチン





として、[ドライバー オブジェクトの図](introduction-to-driver-objects.md#driver-object-illustration)、カーネル モード ドライバーがあると合わせて、それぞれのドライバー オブジェクトのエントリ ポイントを設定する他の標準的な手順を示します。 ほとんどの標準のドライバー ルーチンといくつか、構成に依存するオブジェクトを使用するは、I/O マネージャーによって定義されます。 ISR、 *SynchCritSection*ルーチンと NT カーネルが"custom"が定義という単語を含む名前を持つドライバー オブジェクトの図に示すものです。

ほとんどのドライバーを使用して、[デバイス拡張機能](device-extensions.md)各デバイス オブジェクトの I/O 操作のデバイス固有の状態を維持するために、その他の標準を確保するために割り当てる必要があります、すべてのシステム リソースへのポインターを格納して作成します。ルーチン。 たとえば、 **DDCustomTimerDpc**ドライバー オブジェクトの図に示すルーチンには、タイマーのカーネル定義と DPC オブジェクト用のストレージを提供するドライバーが必要です。

最下位レベルのドライバーで左側のような標準のドライバーのルーチンのセット、[ドライバー オブジェクトの図](introduction-to-driver-objects.md#driver-object-illustration)より高度なドライバーのセットとは異なるとは限りません。 この図に示すように、ルーチンの一部は、要件をデバイスに依存する、または構成に依存します。 他のユーザーは省略可能: ドライバーの設計を性質や、ドライバーのデバイスの構成によっては、このようなルーチンを実装することができますおよびドライバーののチェーン内の位置階層型ドライバー。

 

 




