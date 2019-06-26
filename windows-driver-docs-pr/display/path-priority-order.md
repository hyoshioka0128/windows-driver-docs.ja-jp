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
ms.openlocfilehash: 69f64657ca0fed20fa28bd3afff5053b63791d2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385590"
---
# <a name="path-priority-order"></a>パスの優先順位


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) CCD 関数の決定、パス内のアクティブ パス配列で指定された、 *pathArray*パラメーターには、このような順序がその**SetDisplayConfig**配列パス要素の数を削減するより高い優先順位を設定します。 次の項目に影響を与える、順序付け。

-   場合[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)既存の表示構成が見つからない**SetDisplayConfig**検索の順序で最適なモード ロジックの中にパスの優先度を使用します。 そのため、 **SetDisplayConfig**はより低い優先度のパスもネイティブの解像度でより高い優先度のパスを満たすために可能性が高くなります。

-   複製されたパスには、最高の優先度のパスは、反転がスケジュールされているパスです。 そのため、低い優先度のパスはマイナー分裂されることができます。

-   DirectX グラフィックスのカーネル サブシステム サブシステムからに渡されるパス-重要度の値を導出する (GDI プライマリ ビュー) およびパスの優先度を使用して、 **ImportanceOrdinal**のメンバー、 [ **D3DKMDT\_VIDPN\_存在\_パス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)ディスプレイのミニポート ドライバーへの呼び出しで構造体。 パス-重要度の値に影響を与えますドライバーの決定など、どのパスに、ドライバーは、リソース割り当ての優先順位を与えする必要があります。 などの通算の下位パスには、オーバーレイにまたはより高い品質のコント ローラーに簡単にアクセスがあります。

[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig) CCD 関数は常に優先順位で、パスを返します。 場合、QDC\_すべて\_パス フラグに設定されて、*フラグ*パラメーターの**QueryDisplayConfig**、 **QueryDisplayConfig**のすべてを返します、配列の非アクティブなパスの組み合わせが次のパスにすべてのアクティブなパスの組み合わせ、 *pPathInfoArray*パラメーターを指定します。

 

 





