---
title: パスの優先順位
description: パスの優先順位
ms.assetid: 93f8f932-fc7b-4420-8b3e-27194937bed5
keywords:
- Windows 7 の WDK の表示、CCD 概念、パスの優先順位の接続が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD 概念、パスの優先順位の接続が表示されます。
- Windows 7 の WDK の表示、CCD 概念、パスの優先順位の構成が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD 概念、パスの優先順位の構成が表示されます。
- CCD WDK Windows 7 の概念の表示、パスの優先順位
- CCD 概念 WDK Windows Server 2008 R2 の表示、パスの優先順位
- パスの優先度の表示順序 WDK Windows 7
- パスの優先順位 WDK Windows Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98dcd5a41c8a2f98d02eb6077554d2920402d1b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549799"
---
# <a name="path-priority-order"></a>パスの優先順位


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533) CCD 関数の決定、パス内のアクティブ パス配列で指定された、 *pathArray*パラメーターには、このような順序がその**SetDisplayConfig**配列パス要素の数を削減するより高い優先順位を設定します。 次の項目に影響を与える、順序付け。

-   場合[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)既存の表示構成が見つからない**SetDisplayConfig**検索の順序で最適なモード ロジックの中にパスの優先度を使用します。 そのため、 **SetDisplayConfig**はより低い優先度のパスもネイティブの解像度でより高い優先度のパスを満たすために可能性が高くなります。

-   複製されたパスには、最高の優先度のパスは、反転がスケジュールされているパスです。 そのため、低い優先度のパスはマイナー分裂されることができます。

-   DirectX グラフィックスのカーネル サブシステム サブシステムからに渡されるパス-重要度の値を導出する (GDI プライマリ ビュー) およびパスの優先度を使用して、 **ImportanceOrdinal**のメンバー、 [ **D3DKMDT\_VIDPN\_存在\_パス**](https://msdn.microsoft.com/library/windows/hardware/ff546647)ディスプレイのミニポート ドライバーへの呼び出しで構造体。 パス-重要度の値に影響を与えますドライバーの決定など、どのパスに、ドライバーは、リソース割り当ての優先順位を与えする必要があります。 などの通算の下位パスには、オーバーレイにまたはより高い品質のコント ローラーに簡単にアクセスがあります。

[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215) CCD 関数は常に優先順位で、パスを返します。 場合、QDC\_すべて\_パス フラグに設定されて、*フラグ*パラメーターの**QueryDisplayConfig**、 **QueryDisplayConfig**のすべてを返します、配列の非アクティブなパスの組み合わせが次のパスにすべてのアクティブなパスの組み合わせ、 *pPathInfoArray*パラメーターを指定します。

 

 





