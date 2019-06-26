---
title: D3dCreateSurfaceEx とバッキング サーフェス
description: D3dCreateSurfaceEx とバッキング サーフェス
ms.assetid: aad37654-616f-4cbd-9a9c-07458fb61947
keywords:
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- WDK の Direct3D サーフェイスのバックアップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e24557d2aeeca83c093b38e2b6d8b1bbde6b275
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370163"
---
# <a name="d3dcreatesurfaceex-and-backing-surfaces"></a>D3dCreateSurfaceEx とバッキング サーフェス


## <span id="ddk_d3dcreatesurfaceex_and_backing_surfaces_gg"></span><span id="DDK_D3DCREATESURFACEEX_AND_BACKING_SURFACES_GG"></span>


[**D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)用*サーフェスをバックアップ*をシステム メモリ マネージ サーフェスの永続的なコピーが作成されます。 これにより、サーフェイスでのドライバー側構造を割り当てると、D3DDP2OP 対応ドライバー\_TEXBLT トークン システムには、ビデオのテクスチャをダウンロードします。

[**D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)べきではない、形式やエミュレーション コードでしたをサポートし、画面を処理するため、要求されたバッキング サーフェイスの機能に基づいて失敗します。 ただし、失敗の他の条件は有効です。 たとえば、ドライバーが失敗することが**D3dCreateSurfaceEx**プライベート データ構造を保持し、メモリ領域が不足する場合。

ドライバーは失敗しません[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)のピクセル形式のできませんサーフェスの形式をバックアップします。 ソフトウェア ラスタライザーを使用するため、このような画面が作成されます。 ドライバーでは、バッキング サーフェスをサポートしていませんを無視するだけです。 (または、ドライバーはドライバー側構造を作成できますが、対応するハンドルがドライバーに送信されることはありません、その後)。

これらのバッキング サーフェスで[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)原因がアプリケーションに適用するのにはエラー コードにはドライバーがエミュレーションのみのモードでアプリケーションを可能性のある影響しことができます。 実行してこのような状況へのドライバーの応答をテストすることができます、 *ddtest.exe* DirectX 7.0 SDK 上にあるアプリケーション。 実行*ddtest.exe*ドライバーでサポートされていないが、(これらの形式の一覧は、DirectDraw SDK ドキュメントで見つかんだことができます)、DirectDraw エミュレーション層でサポートされている形式のバッキング表面のテクスチャを作成しようとします。

 

 





