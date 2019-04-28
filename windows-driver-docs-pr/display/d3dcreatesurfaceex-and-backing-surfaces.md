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
ms.openlocfilehash: 2d9afd6f955c1a8c5eea51e406eba2490bd3cb3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370877"
---
# <a name="d3dcreatesurfaceex-and-backing-surfaces"></a>D3dCreateSurfaceEx とバッキング サーフェス


## <span id="ddk_d3dcreatesurfaceex_and_backing_surfaces_gg"></span><span id="DDK_D3DCREATESURFACEEX_AND_BACKING_SURFACES_GG"></span>


[**D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)用*サーフェスをバックアップ*をシステム メモリ マネージ サーフェスの永続的なコピーが作成されます。 これにより、サーフェイスでのドライバー側構造を割り当てると、D3DDP2OP 対応ドライバー\_TEXBLT トークン システムには、ビデオのテクスチャをダウンロードします。

[**D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)べきではない、形式やエミュレーション コードでしたをサポートし、画面を処理するため、要求されたバッキング サーフェイスの機能に基づいて失敗します。 ただし、失敗の他の条件は有効です。 たとえば、ドライバーが失敗することが**D3dCreateSurfaceEx**プライベート データ構造を保持し、メモリ領域が不足する場合。

ドライバーは失敗しません[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)のピクセル形式のできませんサーフェスの形式をバックアップします。 ソフトウェア ラスタライザーを使用するため、このような画面が作成されます。 ドライバーでは、バッキング サーフェスをサポートしていませんを無視するだけです。 (または、ドライバーはドライバー側構造を作成できますが、対応するハンドルがドライバーに送信されることはありません、その後)。

これらのバッキング サーフェスで[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)原因がアプリケーションに適用するのにはエラー コードにはドライバーがエミュレーションのみのモードでアプリケーションを可能性のある影響しことができます。 実行してこのような状況へのドライバーの応答をテストすることができます、 *ddtest.exe* DirectX 7.0 SDK 上にあるアプリケーション。 実行*ddtest.exe*ドライバーでサポートされていないが、(これらの形式の一覧は、DirectDraw SDK ドキュメントで見つかんだことができます)、DirectDraw エミュレーション層でサポートされている形式のバッキング表面のテクスチャを作成しようとします。

 

 





