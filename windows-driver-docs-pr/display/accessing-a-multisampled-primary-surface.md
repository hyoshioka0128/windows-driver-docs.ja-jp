---
title: マルチサンプリングされたプライマリ サーフェスへのアクセス
description: マルチサンプリングされたプライマリ サーフェスへのアクセス
ms.assetid: 5d83699c-45ae-46d1-8804-1a18bfbc203f
keywords:
- DirectX 8.0 リリース ノート Windows 2000 の WDK 表示、マルチ サンプリングがレンダリング、プライマリの画面にアクセスします。
- マルチ サンプリング WDK DirectX 8.0 のレンダリング、プライマリの画面にアクセスします。
- プライマリの画面にアクセスする multisamples の WDK DirectX 8.0 のレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4727dbc6abfb2807c7e1628eb4870ce523046c96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375401"
---
# <a name="accessing-a-multisampled-primary-surface"></a>マルチサンプリングされたプライマリ サーフェスへのアクセス


## <span id="ddk_accessing_a_multisampled_primary_surface_gg"></span><span id="DDK_ACCESSING_A_MULTISAMPLED_PRIMARY_SURFACE_GG"></span>


Direct3D ランタイムは、マルチ サンプリングされたバッファーに高性能な CPU へのアクセスを防ぎます。 ただし、ランタイムは、ドライバーを呼び出すことができます[ *DdLock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)スクリーン ショットのおよびテストのシナリオでのイメージの検証などの低パフォーマンスへのマルチ サンプリングされたバッファーは、機能します。

形式、およびドライバーのドライバーを変換する必要があります、ランタイムでは、マルチ サンプリングされたバッファーのサンプルのレイアウトを処理できないため、 [ *DdLock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)関数が含まれるデータのバッファーを返す必要があります、1 つのピクセルあたりのサンプル形式で画面の内容。 Direct3D ランタイムが、ドライバーを呼び出すアプリケーションのマルチ サンプリングされたフリッピング チェーン フロント バッファーのコピーを取得する IDirect3DDevice8::GetFrontBuffer を呼び出す場合*DdLock*フロント バッファーをロックする関数。 このバッファーには、プライマリのサーフェイスの標準の幅、高さ、ピクセル形式に解決されるフロント バッファーの現在のバージョンが含まれています。

そのようなバッファーをデバイスのメモリで使用できる場合、ドライバーはそのバッファーにポインターを返すことができます。 (マルチ サンプリングのバッファーを解決するにはスキャン アウト時にデバイスの場合と同様) には、このようなバッファーがデバイスのメモリでは使用できないかどうか、ドライバーがシステム メモリ内でバッファーを割り当てるし、マルチ サンプリングされたフロント バッファーを解決するにはこのシステムのバッファーにする必要があります。 ランタイムでは、ドライバーのマルチ サンプリングされたフロント バッファーをこのシステムのバッファーに解決するために必要なだけ時間がかかることができます。

ランタイムが、DDLOCK を設定するかどうかに関係なく\_ドライバーを呼び出すときに、読み取り専用フラグ[ *DdLock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)関数では、ランタイム処理をこれらのバッファーとして読み取り専用です。 そのため、ドライバーは、いずれかをコピーする必要はありませんシステム メモリからのデータがデバイスのメモリに表面化します。 さらに、ドライバーの[ *DdUnlock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)関数が 1 つのサンプル-ピクセル形式をプライマリ サーフェスのマルチ サンプリングされた形式に変換する必要はありません。

アプリケーションのカーソルのメソッドを呼び出し、 **IDirect3DDevice8**インターフェイスも増加[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)マルチ サンプリングされたプライマリを対象とする呼び出し。 これら*DdBlt*呼び出しが 1 つのサンプル-ピクセルあたりのカーソルのデータから、マルチ サンプリングされたプライマリへの変換を処理する必要があります。

詳細については**IDirect3DDevice8**、DirectX 8.0 SDK ドキュメントを参照してください。

 

 





