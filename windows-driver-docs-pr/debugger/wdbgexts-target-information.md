---
title: WdbgExts ターゲットの情報
description: WdbgExts ターゲットの情報
ms.assetid: 70b26047-2f3a-4d35-861f-a9ca17d1d5f9
keywords:
- WdbgExts 拡張機能します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35aea6028bf91426673da3743f34991742e928ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532907"
---
# <a name="wdbgexts-target-information"></a>WdbgExts ターゲットの情報


ターゲットがメモリ アドレスの 32 ビットまたは 64 ビットのポインターを使用するかどうかを判断する関数を使用して[ **IsPtr64**](https://msdn.microsoft.com/library/windows/hardware/ff551094)します。

については、ターゲットのオペレーティング システムを使用、 [ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作[ **IG\_取得\_カーネル\_バージョン**](https://msdn.microsoft.com/library/windows/hardware/ff550918). 現在のプロセッサは、どれをご確認ください、ターゲットでプロセッサの合計数を取得する、関数を使用して[ **GetKdContext**](https://msdn.microsoft.com/library/windows/hardware/ff546962)します。

[ **GetDebuggerData** ](https://msdn.microsoft.com/library/windows/hardware/ff546573)返します、KDDEBUGGER\_DATA64 または KDDEBUGGER\_ターゲットに関する情報を含む DATA32 構造体を[デバッガー エンジン](introduction.md#debugger-engine)がクエリを実行したり、現在のセッション時に決定されます。 この情報には、特定のキーのターゲットの場所と特定の状態の値が含まれています。

デバッガーでは、ターゲットから取得したいくつかの情報をキャッシュします。 関数は、 [ **GetDebuggerCacheSize** ](https://msdn.microsoft.com/library/windows/hardware/ff546568)はこのキャッシュのサイズを返します。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

強力なターゲット API を参照してください。[ターゲット情報](target-information.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)このドキュメントの「します。

 

 





