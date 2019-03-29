---
title: sAPOs と Windows Vista のオーディオのアーキテクチャ
description: sAPOs と Windows Vista のオーディオのアーキテクチャ
ms.assetid: b2effc05-5d5c-4209-b2b3-b91d9f1519e2
keywords:
- LFX WDK
- GFX WDK
- オーディオ グラフ WDK
- オーディオ エンジン WDK
- ネゴシエーション WDK オーディオの設定
- IsInputFormatSupported WDK
- LockForProcess WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cad644a04ff20596a6bb187c224885379d01ed33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571991"
---
# <a name="sapos-and-the-windows-vista-audio-architecture"></a>sAPOs と Windows Vista のオーディオのアーキテクチャ


Windows Server 2003 および Windows XP の 32 ビット バージョンでは、グローバル効果フィルター (GFX フィルター) を使用してシステム エフェクトのデジタル オーディオ データを処理します。

オペレーティング システムは、Windows XP スタイル GFX フィルターをサポートしていません。 代わりに、Windows Vista には、既定でインストールされているいくつかのユーザー モード プロセスで COM オブジェクトが含まれています。 システム エフェクト オーディオ処理オブジェクト (sAPOs) と呼ばれるこれらのオブジェクトは、Windows Vista のオーディオ ストリームのデジタル信号処理を提供します。 SAPO は、基本的に、特定のデジタル信号処理 (DSP) 効果を提供に書き込まれるアルゴリズムを含むホスト オブジェクトです。

次の図は、Windows Vista のオーディオ アーキテクチャの簡略化された表現です。 矢印は、オーディオ データのストリームのパスを表示します。

![基本的な windows vista のオーディオ アーキテクチャを示す図](images/sysfxapo-ms-components.png)

図に示すよう、Windows Vista のオーディオ アーキテクチャはユーザー モードおよびカーネル モード コンポーネントで構成されます。 オーディオ エンジンは、システム提供のオーディオ処理オブジェクト (APOs) および sAPOs から組み込まれているストリームとデバイスのパイプで構成されます。

カーネル モード コンポーネントには、各コンポーネントに分離される明確に定義された機能があります。

オーディオのエンドポイントは、まとめて loudspeakers ヘッドホンなどのコンポーネントを指します。 図に示すように、アプリケーション エンドポイント バッファー、ストリーム、デバイスのパイプ、およびカーネル モード ドライバーのスタックを使用してオーディオのエンドポイントと通信します。

パイプ、画像、および sAPOs の概念がで詳しく説明、 [Windows Vista のオーディオ エンジンが調べる](exploring-the-windows-vista-audio-engine.md)トピック。 システム提供の sAPOs の詳細については、次を参照してください。、 [Windows 既定 APOs](windows-default-apos.md)トピック。

 

 




