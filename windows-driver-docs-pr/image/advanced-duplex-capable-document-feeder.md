---
title: 詳細両面印刷対応のドキュメント フィーダー
description: 詳細両面印刷対応のドキュメント フィーダー
ms.assetid: 05b91864-7573-4d99-8a03-701d6cdd650b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70129c94c45d4b7ee62c664b660c6f8eeffe4a8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372620"
---
# <a name="advanced-duplex-capable-document-feeder"></a>詳細両面印刷対応のドキュメント フィーダー





高度な双方向のスキャンにより、アプリケーションとは独立して前面を構成し、ページの設定をバックアップします。

次の図は、高度な双方向とドキュメント フィーダー付きのスキャンをサポートするフラット ベッド スキャナーの WIA 項目のツリーを示しています。

![高度な双方向とドキュメント フィーダー付きのスキャンをサポートするフラット ベッド スキャナーの項目のツリーを示す図](images/wia-feeder-tree3.png)

項目のツリー内の別の子アイテムが前面と背面のスキャンが実行されているページが表されることに注意してください。 このようなには別のカテゴリが含まれています、 [ **WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)プロパティ。WIA\_カテゴリ\_フロント ポストと WIA\_カテゴリ\_戻ります。 高度な双方向のスキャンを実行する、スキャナーでフロント エンドとバックエンドの項目を個別に設定します。これらは、さまざまな値に設定可能性があります。 ただし、詳細な双方向のスキャンができる、スキャナーの場合でも存在することはできません前または後ろのアイテムのみです。前面または背面の項目が、その他の項目は、存在するある必要があります。

ドライバーは、フロント エンドとバックエンドの項目の独立した設定があることを示します (を実行する、高度な双方向のスキャンは、)、[詳細設定] を設定して\_フィーダーの DUP フラグ[ **WIA\_DPS\_ドキュメント\_処理\_機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)プロパティ。

### <a name="scanning"></a>スキャン

アプリケーションは、ドキュメント フィーダー付きのスキャンを実行するフィーダー項目に移動します。 フィーダー アイテム、WIA プロパティは、フロント エンドとバックエンドの両方のページに共通するプロパティがサポートされている値のサブセットである必要があります。 アプリケーションは、2 つの種類 (標準的な画像を取得またはフォルダーの取得) で使用するドキュメント フィーダーの設定に影響を与えるデータ転送の使用を選択できます。

### <a name="standard-image-acquisition"></a>標準イメージの取得

標準購入またはフォルダー以外の取得、WIA フィーダー項目プロパティの設定はフロント エンドとバックエンドの両方のページ (双方向と双方向以外の単純なスキャナーのモデルと同じ) 使用されます。

### <a name="folder-image-acquisition"></a>フォルダーの Image Acquisition

フォルダーの取得、WIA フィーダー項目のイメージの設定は無視され、フロント エンドとバックエンドの項目の設定が代わりに使用されます。 高度なアプリケーションでは、ドキュメント フィーダー付きの転送に個々 の構成可能な設定を使用します。 フィーダー スキャナーでは、イメージ データは常に取得フィーダー付きの項目をオフ (フロント エンドとバックエンドの項目) の子項目がある場合でもです。

 

 




