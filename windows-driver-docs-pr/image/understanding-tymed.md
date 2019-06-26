---
title: TYMED とは
description: TYMED とは
ms.assetid: 36110923-c346-4367-8b7d-ef4d003ed88c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e9fdba50a40960fc459ae0479b275c870d7e2a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358206"
---
# <a name="understanding-tymed"></a>TYMED とは





TYMED では、データ転送の種類を指定します。 このメンバーの値がから派生した、 [ **WIA\_IPA\_TYMED** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)一般的な項目のプロパティ。 指定されたデータ転送には、メモリ コールバック転送またはファイル転送のいずれかを指定できます。 TYMED の詳細については、Microsoft Windows SDK ドキュメントを参照して\_XXX 定数。

### <a name="file-transfer-tymed"></a>ファイル転送 TYMED

ファイル転送では、次の値が使用されます。

<a href="" id="tymed-file"></a>TYMED\_ファイル  
1 つのイメージを格納している 1 つのファイルを示します。

<a href="" id="tymed-multipage-file"></a>TYMED\_マルチページ\_ファイル  
マルチページ TIF と似たような形式など、複数のイメージを格納している 1 つのファイルを示します。 これは、主にドキュメント フィーダー付きの取得で使用されます。

### <a name="memory-transfer-tymed"></a>メモリ転送 TYMED

メモリの転送で、次の値が使用されます。

<a href="" id="tymed-callback"></a>TYMED\_コールバック  
1 つのイメージまたはで区切られた複数のイメージを含む 1 つのバッファーを示します IT\_MSG\_新規\_ページ メッセージ。

<a href="" id="tymed-multipage-callback"></a>TYMED\_マルチページ\_コールバック  
区切られた複数のイメージを格納している 1 つのバッファーを示します IT\_MSG\_新規\_ページ メッセージ。 これにより、複数のイメージを格納している 1 つのファイル。 これは、主にドキュメント フィーダー付きの取得で使用されます。

 

 




