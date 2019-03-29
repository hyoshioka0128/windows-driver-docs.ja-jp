---
title: ストリーム ポインターの紹介
description: ストリーム ポインターの紹介
ms.assetid: 2682b145-5148-4301-b382-9811bb5e8fa6
keywords:
- ストリーム ポインター WDK AVStream、ストリーム ポインターの概要
- WDK AVStream のストリーム ポインターを進める
- ストリーム ポインターを進める WDK AVStream
- フレームの参照は、WDK AVStream をカウントします。
- 参照カウント ストリーム ポインターを WDK
- WDK ストリーム ポインターの参照をカウント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e240abc6a03c7fb4ff0d25b00cc47bf44880ca45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573757"
---
# <a name="introduction-to-stream-pointers"></a>ストリーム ポインターの紹介





以前のストリーム クラス モデルで、ミニドライバーは、独自のデータ ストリーム要求のブロック (SRB) キューの保守を担当します。 AVStream はストリーム ポインターの抽象化を通じてこの機能を提供します。 ストリーム ポインターは、特定の AVStream データ フレームに参照です。

使用して、ミニドライバー[暗証番号 (pin) を中心とした処理](pin-centric-processing.md)(ほとんどのハードウェア ドライバー) は、暗証番号 (pin) のキューを管理するストリーム ポインターを使用します。 各ピンには、データ バッファーの独立した、キューがあります。 ピン (いずれかに対して読み取りまたは書き込み要求) のデータ パケットが到着すると、AVStream パケットをキューに追加し、ピン留めのプロセスのディスパッチを呼び出すことができます。

フィルターを中心とした処理を使用するミニドライバーはストリーム ポインターを直接使用しないでください。 参照してください[フィルターを中心とした処理](filter-centric-processing.md)詳細についてはします。

既定では、各キューは、最先端のストリーム ポインターを持っています。 必要に応じて、トレーリング エッジのフラグが指定されている場合のトレーリング エッジ ストリーム ポインターができます。 呼び出して新しいストリーム ポインターを作成できます、ミニドライバー [ **KsStreamPointerClone**](https://msdn.microsoft.com/library/windows/hardware/ff567129)します。

ストリーム ポインターを移動するには一方向のみ: 新しいフレームにします。 これには、先行するストリーム ポインターが呼び出されます。

### <a name="advancing-a-stream-pointer"></a>Stream のポインターを進める

ストリーム ポインターが進むと、新しいフレームに移動または、昇格するいくつかの現在のフレーム内のバイト数。 たとえば、ミニドライバーは、2 つ目のフレームの到着、最初のフレームの到着からストリーム ポインターを進めることができます。

ストリーム ポインターを進めるには、いずれかの呼び出し、暗証番号 (pin) を中心としたフィルターすることができます[ **KsStreamPointerAdvance** ](https://msdn.microsoft.com/library/windows/hardware/ff567125)または[ **KsStreamPointerUnlock** ](https://msdn.microsoft.com/library/windows/hardware/ff567137)で。*取り出し*パラメーターに設定**TRUE**します。

### <a name="frame-reference-counts"></a>フレームの参照カウント

リードとトレーリング エッジの間のウィンドウでは、フレームにはこれらを指すストリーム ポインターを持つフレームは、カウントされた参照。

呼び出すことができます必要に応じて、ミニドライバーのストリーム ポインターを使用して完了時に、 [ **KsStreamPointerSetStatusCode** ](https://msdn.microsoft.com/library/windows/hardware/ff567136)を特定の I/O 要求パケット (IRP) を完了させるエラー コードを指定します。 ミニドライバーは呼び出す必要がありますし、 [ **KsStreamPointerDelete**](https://msdn.microsoft.com/library/windows/hardware/ff567130)します。 AVStream し、以前に削除されたストリーム ポインターが参照されているフレームの参照カウントをデクリメントします。 リーディング エッジと末尾のエッジ ストリーム ポインターを削除できません。

 

 




