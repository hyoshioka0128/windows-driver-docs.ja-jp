---
title: モーション補正コード テンプレート
description: モーション補正コード テンプレート
ms.assetid: 2632f84d-7ebb-4c55-9ba7-996f0cb891bd
keywords:
- 動き補正コード テンプレート WDK DirectX VA
- ProcAmp の WDK DirectX va なので、動き補正コード テンプレート
- デインター レースの WDK DirectX va なので、動き補正コード テンプレート
- COPP WDK DirectX va なので、動き補正コード テンプレート
- 保護 WDK COPP、動き補正コード テンプレートのコピーします。
- ビデオのコピー防止 WDK COPP、動き補正コード テンプレート
- ビデオの WDK COPP 動き補正コード テンプレートの保護
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1130c01796ab6bafc43c7a775df37a4983b4f29a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353028"
---
# <a name="motion-compensation-code-template"></a>モーション補正コード テンプレート


## <span id="ddk_motion_compensation_code_template_gg"></span><span id="DDK_MOTION_COMPENSATION_CODE_TEMPLATE_GG"></span>


このセクションのサンプル コードの実装を示しています、[動き補正](motion-compensation-callbacks.md)ProcAmp コントロール、デインター レース、および認定出力保護プロトコル (COPP) 機能にアクセスするために使用するコード テンプレート。 このテンプレートを使用すると、ディスプレイ ドライバーの開発が簡略化できます。 ただし、正常に動作する、ディスプレイ ドライバーについてこの方法で ProcAmp コントロール、デインター レース、および COPP 機能へのアクセスを実装する必要はありません。

ドライバーは、mpeg-2 ビデオ ストリームのデコードなどの他の DirectX VA 関数をサポートしている場合は、次に含める追加の DirectX VA Guid の処理のコード例を拡張します。

このセクションの内容:

[DirectX VA デバイス クラスを定義します。](defining-directx-va-device-classes.md)

[DirectX VA デバイスの取得](retrieving-directx-va-devices.md)

[DirectX VA デバイス オブジェクトのインスタンスを作成します。](creating-instances-of-directx-va-device-objects.md)

[ProcAmp 制御を実行して、操作をデインター レース](performing-procamp-control-and-deinterlacing-operations.md)

[サブストリーム合成の操作でデインター レースを実行します。](performing-deinterlacing-with-substream-compositing-operations.md)

[COPP 操作を実行します。](performing-copp-operations-example.md)

[DirectX VA デバイス オブジェクトのインスタンスを削除します。](deleting-instances-of-directx-va-device-objects.md)

 

 





