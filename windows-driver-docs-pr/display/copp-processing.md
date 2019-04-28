---
title: COPP の処理
description: COPP の処理
ms.assetid: c9ff0fd3-c063-4450-ae66-54153b3dc53c
keywords:
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示、COPP
- ビデオ アクセラレータ WDK DirectX、COPP
- VA WDK DirectX、COPP
- 出力保護プロトコル WDK DirectX VA の認定
- コピー防止 WDK COPP
- ビデオのコピー防止 WDK COPP
- COPP WDK DirectX VA
- 保護されたビデオの WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53caf237ebf422fbaf0036ad77ada0613fd6624e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361942"
---
# <a name="copp-processing"></a>COPP の処理


## <span id="ddk_certified_output_protection_protocol_processing_gg"></span><span id="DDK_CERTIFIED_OUTPUT_PROTECTION_PROTOCOL_PROCESSING_GG"></span>


このセクションでは、Microsoft Windows Server 2003 Service Pack 1 (SP1) 以降、および Windows XP Service Pack 2 (SP2) 以降にのみ適用されます。

認定の出力保護プロトコル (COPP) デバイス ドライバー インターフェイス (DDI) では、DirectX ビデオ アクセラレータ (VA) グラフィックス アダプターのさまざまなコネクタによって出力されるビデオのコピー防止をサポートするためには拡張します。 COPP DDI はビデオの混在レンダラー間のインターフェイス (*VMR*) とビデオのミニポート ドライバー。 既存の DirectDraw と DirectX VA DDI COPP DDI にマップします。 DDI 経由でアクセスできますが、 **IAMVideoAccelerator**インターフェイス。 DDI を使用してアプリケーションにアクセスできる、 **IAMCertifiedOutputProtection**インターフェイス。

詳細については、 **IAMCertifiedOutputProtection**と**IAMVideoAccelerator**インターフェイス、最新の DirectX ソフトウェア開発キット (SDK) ドキュメントを参照してください。

ビデオのミニポート ドライバーでは、アプリケーションとドライバーの間の保護されているコマンドと状態の受け渡しをサポートする場合、VMR VA COPP の DirectX デバイスを作成するには、ドライバーに呼び出しが開始されます。

次のトピックでは、COPP DDI と COPP をサポートする方法について説明します。

[COPP の概要](introduction-to-copp.md)

[DirectDraw を DirectX VA COPP DDI のマッピング](mapping-the-copp-ddi-to-directdraw-and-directx-va.md)

[COPP のサンプル関数](sample-functions-for-copp.md)

[COPP 関数から返されるエラー コード](returning-error-codes-from-copp-functions.md)

[COPP 操作を実行します。](performing-copp-operations.md)

[実装のヒントと COPP の要件](implementation-tips-and-requirements-for-copp.md)

 

 





