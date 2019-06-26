---
title: 簡易両面印刷対応のドキュメント フィーダー
description: 簡易両面印刷対応のドキュメント フィーダー
ms.assetid: 0807f02a-5bbf-4ed1-b381-63e1f37a0e2e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: febcb9324b0953de9e8ab3871a46dd9b72016fa5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377329"
---
# <a name="simple-duplex-capable-document-feeder"></a>簡易両面印刷対応のドキュメント フィーダー





フロント エンドとバックエンドの両方のページの同じページの設定を使用する単純な双方向のスキャンします。 両面印刷をサポートするスキャナーが双方向のフラグを設定する必要がありますで、 [ **WIA\_DPS\_ドキュメント\_処理\_選択**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)プロパティ。

次の図は、単純な二重モード対応ドキュメント フィーダーのスキャンをサポートしているフラット ベッド スキャナーの WIA 項目のツリーを示しています。

![単純な二重モード対応ドキュメント フィーダー付きのスキャンをサポートするフラット ベッド スキャナーの項目のツリーを示す図](images/wia-feeder-tree3.png)

項目のツリー内の別の子アイテムが前面と背面のスキャンが実行されているページが表されることに注意してください。 このようなには別のカテゴリが含まれています、 [ **WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)プロパティ。WIA\_カテゴリ\_フロント ポストと WIA\_カテゴリ\_戻ります。 基本的な双方向のスキャンを実行する、スキャナーでフロント エンドとバックエンドの項目は設定されませんとは別にします。これらは、正確な値が同じに設定されます。

### <a name="scanning"></a>スキャン

アプリケーションは、ドキュメント フィーダー付きのスキャンを実行するフィーダー項目に移動します。 この項目は構成をスキャンし、各ページの設定ページの数と設定の場所は、 [ **WIA\_DPS\_ドキュメント\_処理\_選択**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)双方向の設定にします。 ページは、ドキュメントの 1 つの側に対応します。 2 つのドキュメントをスキャンする 4 つのページで結果に注意してください。

### <a name="image-acquisition"></a>Image Acquisition

標準の取得とフォルダーの取得、WIA フィーダー項目プロパティの設定は、フロント エンドとバックエンドの両方のページに使用されます。 標準の取得とフォルダーの取得の詳細については、次を参照してください。[二重モード対応ドキュメント フィーダー付きの高度な](advanced-duplex-capable-document-feeder.md)します。

 

 




