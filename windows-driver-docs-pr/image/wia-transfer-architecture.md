---
title: WIA 転送のアーキテクチャ
description: WIA 転送のアーキテクチャ
ms.assetid: d8a11440-efdb-4590-9261-2b424c11186d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4f0b79d4cb13965bd10b63444ffae490ce48ef3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537926"
---
# <a name="wia-transfer-architecture"></a>WIA 転送のアーキテクチャ


Stream ベースの転送には、ドライバーとドライバー開発者向けの転送が簡略化します。 メモリ内およびファイル転送では、呼び出し元は転送の種類を使用して、ドライバーは、種類を選択したどの転送に応じて異なるアクションを実行する必要があるを指定する必要があります。 ストリーム ベースの転送では、呼び出し元はメモリまたはファイルの転送を指定する必要ありません。呼び出し元を使用するストリームのみを指定し、このストリームは、ファイル ストリームまたはメモリ ストリームかどうか、ドライバーが同様に動作します。 ストリームを使用すると簡単に統合を提供しても、 [WIA イメージ処理フィルター](wia-image-processing-filter.md)します。

その他の WIA アプリケーション プログラミング インターフェイス (Api) と、デバイス ドライバー インターフェイス (Ddi) と同様に**IStream**コンポーネント オブジェクト モデル (COM) に基づきます。 ストリームの転送が他のストリームと互換性があることを確認する、 **IWiaTransfer**インターフェイスを公開する必要があります。

**IWiaTransfer**インターフェイスの転送、転送の取り消し、エラーと状態がレポートの統合中に進行状況の表示を有効にする方法がありますとアップロード、およびデバイスからデータをダウンロードします。 **IWiaTransfer**インターフェイスはを通じてしか利用できませんが、 **IWiaItem2**インターフェイス。 詳細については、 **IWiaItem2**または**IWiaTransfer**インターフェイスとそのメソッドは、Microsoft Windows SDK のマニュアルを参照してください。

このセクションの内容:

[IStream データ転送のドライバーの変更](istream-data-transfer-driver-changes.md)

[IStream 転送のドライバーの例](istream-transfer-driver-example.md)

 

 




