---
title: シーケンスの要件
description: シーケンスの要件
ms.assetid: ee716286-f455-463d-906d-6f1b9fb8f227
keywords:
- ビデオのデコード WDK DirectX va なので、シーケンスの要件
- ビデオの WDK DirectX va なので、シーケンスの要件をデコード
- WDK の DirectX va なので、シーケンスの要件をデコードする画像
- WDK DirectX VA の要件をシーケンス処理します。
- 圧縮されたバッファー WDK DirectX VA
- WDK DirectX VA をバッファー処理します。
- 連続して要件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc36cb08f887ad46e599aa32267e5cea72bc035b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570474"
---
# <a name="sequence-requirements"></a>シーケンスの要件


## <span id="ddk_sequence_requirements_gg"></span><span id="DDK_SEQUENCE_REQUIREMENTS_GG"></span>


アクセラレータとデコーダーのシーケンスの要件は、競合状態とデコードの処理中に、デコーダーとアクセラレータの不適切な操作を回避するために従う必要があります。

### <a name="span-idacceleratorspanspan-idacceleratorspanspan-idacceleratorspanaccelerator"></a><span id="Accelerator"></span><span id="accelerator"></span><span id="ACCELERATOR"></span>アクセラレータ

クエリを実行すると、圧縮されていないサーフェイスの表示が保留中または進行中かどうかと、要求された操作が完了した場合、ハードウェア アクセラレータを報告します。 ただし、その競合状態がデコード処理中に望ましくない動作を発生しないことを確認するのにはホスト ソフトウェア デコーダー (アクセラレータではありません) の必要があります。

### <a name="span-iddecoderspanspan-iddecoderspanspan-iddecoderspandecoder"></a><span id="Decoder"></span><span id="decoder"></span><span id="DECODER"></span>デコーダー

デコーダーは、正しくデコードし、圧縮されていない画面を表示する 2 つの規則に従う必要があります。

1.  経過していない限り表示用に送信された任意の画像を上書きしないでください、ディスプレイに表示され、表示からも削除されます。

2.  まだ作成されていないその他の画像を作成するための参照として必要とされる任意の画像を上書きしません。

これらの規則に従って、により、デコード処理で、シーケンシャルな操作が正常に動作し、ディスプレイ上の成果物の分裂を回避できます。 基本ルールは、します。*参照するか、表示の必要なものを上書きしないようにし競合状態を避けます。*

競合状態を避けるためには、ソフトウェア デコーダーは、アクセラレータの状態を照会する必要があります。 デコーダーは、十分な数の画像の圧縮されていないサーフェスを使用して、領域が必要なすべての操作に使用できることを確認する必要がありますも。 これは、結果、B、I から成るビデオ ストリームのデコードに少なくとも 4 つの画像の圧縮されていないサーフェスの必要性、および P 画像。 4 つを超えるサーフェスを使用して、通常お勧めし、フロント エンドのアルファ ブレンディングなど、一部の操作の必要があります。 (追加のサーフェスを使用して大幅に短縮できます操作の依存関係を解決するを待機する必要がある。)

デコード従来は、B、およびビデオ フレームの P 構造 (deblocking フィルターを使用して) なしを示す例が記載[を使用して 4 つ非圧縮サーフェス デコードの](using-four-uncompressed-surfaces-for-decoding.md)と[を使用して 5 つまたは複数デコードのサーフェスを非圧縮](using-five-or-more-uncompressed-surfaces-for-decoding.md)します。

**注**   、圧縮されたバッファーのも、圧縮されていないサーフェスの場合と通常はお勧めを割り当てられ、使用可能なバッファーを順番にではなく同じバッファー、または同じのサブセットを再利用するには、バッファーが割り当てられています。 これは、不要な依存関係を待機しているによる遅延が、追加の可能性を削減できます。 二重またはトリプル バッファリングのこれらのバッファー間で循環が動作して、アーティファクトを回避するためには、適切な方法など、一時的な画像がフリーズすることを表す、ドライバーによって複数のバッファーの割り当てを実行する必要があります。 これは、アルファ ブレンド データ読み込みを具体的に適用されます。

 

 

 





