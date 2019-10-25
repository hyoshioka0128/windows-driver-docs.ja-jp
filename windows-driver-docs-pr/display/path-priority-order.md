---
title: パスの優先順位
description: パスの優先順位
ms.assetid: 93f8f932-fc7b-4420-8b3e-27194937bed5
keywords:
- 接続すると、WDK Windows 7 のディスプレイ、CCD の概念、パスの優先順位が表示されます
- 接続すると、WDK Windows Server 2008 R2 の表示、CCD の概念、パスの優先順位が表示されます
- '構成: WDK Windows 7 ディスプレイ、CCD の概念、パスの優先順位'
- '構成: WDK Windows Server 2008 R2 ディスプレイ、CCD の概念、パスの優先順位'
- CCD の概念 WDK Windows 7 の表示、パスの優先順位
- CCD の概念 WDK Windows Server 2008 R2 の表示、パスの優先順位
- パスの優先順位 (WDK Windows 7 ディスプレイ)
- パスの優先順位 (WDK Windows Server 2008 R2 表示)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf8afd82379cee97f8ffe496211f1271f8a49d6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829859"
---
# <a name="path-priority-order"></a>パスの優先順位


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

[**Setdisplayconfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) CCD 関数は、 *patharray*パラメーターによって指定されたパス配列内のアクティブパスが順序付けされていることを確認します。これにより、 **setdisplayconfig**は、より優先順位の低い配列パス要素になります。 次の項目が順序付けに影響します。

-   [**Setdisplayconfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)が既存の表示構成を見つけられない場合、 **setdisplayconfig**は検索順序の最適モードロジックでパスの優先順位を使用します。 そのため、 **Setdisplayconfig**は、優先順位の低いパスよりもネイティブの解決で優先順位の高いパスを満たす可能性が高くなります。

-   複製されたパスでは、優先順位が最も高いパスが、フリップがスケジュールされているパスになります。 そのため、優先順位の低いパスは軽微な分裂の影響を受ける可能性があります。

-   DirectX グラフィックスのカーネルサブシステムでは、パスの優先順位 (GDI プライマリビューと共に) を使用して、サブシステムが存在する D3DKMDT\_VIDPN\_のメンバーに渡すパスの重要度の値を派生 [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)表示ミニポートドライバーの呼び出しのパス構造。 パスの重要度の値は、ドライバーがリソース割り当てに優先するパスを指定するなど、ドライバーの決定に影響します。 たとえば、下の序数のパスでは、オーバーレイへのアクセスや品質の高いコントローラーへのアクセスが向上している可能性があります。

[**Querydisplayconfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig) CCD 関数は、常に優先順位に従ってパスを返します。 QDC\_すべての\_PATHS フラグが**querydisplayconfig**の*Flags*パラメーターに設定されている場合、 **querydisplayconfig**は、PATHS 配列内のすべてのアクティブパスの組み合わせに続く非アクティブパスのすべての組み合わせを返します。*Ppathinfoarray*パラメーターはを指定します。

 

 





