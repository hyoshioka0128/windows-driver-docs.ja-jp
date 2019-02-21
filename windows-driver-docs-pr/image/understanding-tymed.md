---
title: TYMED を理解します。
description: TYMED を理解します。
ms.assetid: 36110923-c346-4367-8b7d-ef4d003ed88c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02afa4eaa3596bddcea5677c26acc942e8784412
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549774"
---
# <a name="understanding-tymed"></a>TYMED を理解します。





TYMED では、データ転送の種類を指定します。 このメンバーの値がから派生した、 [ **WIA\_IPA\_TYMED** ](https://msdn.microsoft.com/library/windows/hardware/ff551656)一般的な項目のプロパティ。 指定されたデータ転送には、メモリ コールバック転送またはファイル転送のいずれかを指定できます。 TYMED の詳細については、Microsoft Windows SDK ドキュメントを参照して\_XXX 定数。

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

 

 




